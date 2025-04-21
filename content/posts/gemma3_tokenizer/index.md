{
  "title": "(Re)building Gemma tokenizer in Python",
  "date": "2025-04-21T09:05:38Z",
  "lastmod": "2025-04-21T09:05:38Z"
}


> [!NOTE]  This is not a tutorial type blog. Think of this as my notes as I was going through the building tokenizer phase.

First thing first, let's download the model files. I mean tokenizer files. But, they end with `.model`. These are serialized using ProtoBuf. You can find the specification of the file [here](https://github.com/google/sentencepiece/blob/master/src/sentencepiece_model.proto). You can download the model file from [here](https://huggingface.co/google/gemma-3-27b-it/blob/main/tokenizer.model).

Gemma-3 tokenizer is different than Gemma-2. Algorithm remains same, vocabulary size is also more or less similar (256K vs ~262K). Within gemma3 variants, the same tokenizers are used. 


```python
!md5sum ../models/gemma*.model

```
f9e2445870ec741aa6346bbd75531bb4  ../models/gemma2.model
00d2276cbec4474f6cf3df98fbc18cbb  ../models/gemma3-4b-it.model
00d2276cbec4474f6cf3df98fbc18cbb  ../models/gemma3-27b-it.model
00d2276cbec4474f6cf3df98fbc18cbb  ../models/gemma3.model



```python
import sentencepiece as sp
g2 = sp.SentencePieceProcessor(model_file="../models/gemma2.model")
print(g2.vocab_size())

```
256000



```python
g3 = sp.SentencePieceProcessor(model_file="../models/gemma3-4b-it.model")
print(g3.vocab_size())

```
262144



Let's have a list of toy strings to keep track how our tokenizer is doing as we progress.


```python
txt_emojis1 = "🫩 🥲 🩵"
txt_emojis2 = "🗽⃢⃢🗿"
txt_life = "🤔➡️🌱🌎✨➡️🚶‍♂️🚶‍♀️❓➡️🌅🌄🌌➡️💭💡🧠➡️🤝❤️🤗➡️📚📜🏛️"
txt_gibberish = "Hello've world23 HOW's HOW'S how's are yous?"
txts = [txt_emojis1, txt_emojis2, txt_life, txt_gibberish]

```


## Let's play with the binary file.

You will need proto file I was talking about earlier. And also, you should install `protoc` [https://protobuf.dev/installation/](https://protobuf.dev/installation/). That will generate a file which you can use to read model files in Python.


```python
!protoc --proto_path=./ --python_out=./ ./sentencepiece_model.proto


```


```python
import sentencepiece_model_pb2 as model_pb

g3_pb = model_pb.ModelProto()
with open("../models/gemma3-4b-it.model", "rb") as f:
    g3_pb.ParseFromString(f.read())

g2_pb = model_pb.ModelProto()
with open("../models/gemma2.model", "rb") as f:
    g2_pb.ParseFromString(f.read())

```


## Control Tokens

Let's see what control tokens we have.


```python
for i, p in enumerate(g3_pb.pieces):
    if p.type == 3:
        print(i, p.piece)

```
0 <pad>
1 <eos>
2 <bos>



BTW, when you tokenize, you have to add bos yourself. `<bos>` is not tokenized. They talk about this in [the technical report](https://storage.googleapis.com/deepmind-media/gemma/Gemma3Report.pdf). `<bos>` is not tokenized, because it is control token. Other special tokens, like `<start_of_turn>` automatically get tokenized correctly. 


```python
g3.encode_as_pieces("<bos>Heyllo", add_bos=True, add_eos=True)

```
```text
['<bos>', '<', 'bos', '>', 'Hey', 'llo', '<eos>']

```


You see, `<bos>` got splitted into `<`, `bos`, `>`.


```python
g3.encode_as_pieces("""<start_of_turn>user
Who are you?<end_of_turn>
<start_of_turn>model""")

```
```text
['<start_of_turn>',
 'user',
 '\n',
 'Who',
 '▁are',
 '▁you',
 '?',
 '<end_of_turn>',
 '\n',
 '<start_of_turn>',
 'model']

```


```python
piece_to_id = {p.piece: i for i,p in enumerate(g3_pb.pieces)}
print(piece_to_id["<start_of_turn>"])

```
105



```python
g3_pb.pieces[105]

```
```text
piece: "<start_of_turn>"
score: 0
type: USER_DEFINED

```


Why then did `<start_of_turn>` got tokenized properly? Because, it is something we call user defined token. Like when you pretrain the model, your corpus will probably not have such tokens. Or even if they have, they may not be frequent enough to get BPEd. 


By the looks of it, Gemma3 has lot more user defined tokens than Gemma2. I am not sure why is this the case though. Though, I am curious, what do you gain by making it a control token instead of user defined token like `<start_of_turn>`.


Let's look at the protocol specification to understand this `type` better. 


```python
from collections import Counter

# Just copying some fields from proto specification of the model.

NORMAL = 1;        # normal symbol
UNKNOWN = 2;       # unknown symbol. only <unk> for now.
CONTROL = 3;       # control symbols. </s>, <s>, <2ja> etc.
USER_DEFINED = 4;  # user defined symbols.
                   # Typical usage of USER_DEFINED symbol
                   # is placeholder.
BYTE = 6;          # byte symbols. Used when `byte_fallback` is true.
UNUSED = 5;        # this piece is not used.


Counter([None, "Normal", "Unknown", "Control", "User Defined", "Unused", "Byte"][p.type] for p in g3_pb.pieces)

```
```text
Counter({'Normal': 255474,
         'User Defined': 6410,
         'Byte': 256,
         'Control': 3,
         'Unknown': 1})

```


```python
Counter([None, "Normal", "Unknown", "Control", "User Defined", "Unused", "Byte"][p.type] for p in g2_pb.pieces)

```
```text
Counter({'Normal': 255495,
         'Byte': 256,
         'User Defined': 245,
         'Control': 3,
         'Unknown': 1})

```


They have lots of "unused" tokens than Gemma2. I wonder why they added "unused" tokens, thousands of them, if they were unusable. Never the less, since it is user defined, it is treated specially, even if it was not in the training corpus.


```python
g3.encode_as_pieces("<unused10> blahblahblah")

```
```text
['<unused10>', '▁blah', 'blah', 'blah']

```


Now enough of playing with their tokenizer. 

## Let's build tokenizer

I'll assume you know little bit of BPE. If you don't, YouTube "Andrej Karpathy Tokenizer". You won't be disappointed. 

Speaking of assumptions, SentencePiece assumes that you don't use "▁" in your words. What SentencePiece does is it replaces spaces by this "▁". Then it runs BPE (not actually Byte Pair, but unicode pairs, will come there, hold on.)


```python
g3.decode(g3.encode_as_pieces("He▁llo▁ World")) # Yikes

```
```text
'He llo  World'

```


Anyway, after replacing space with '▁' (U+2581), SentencePiece finds all the tokens that are user defined. Thus `"<start_of_turn>Hello▁World!▁🩵"` becomes `["<start_of_turn>", "H", "e", "l", "l", "o", "▁", "W", "o", "r", "l", "d", "!", "🩵"]`. You see, unlike OpenAI's tiktokenizer, SentencePiece does not split "🩵" into `0xF0 0x9F 0xA9 0xB5`. Also, user defined tokens are frozen. They aren't allowed to form pairs with their neighbours. :(  


```python
user_defined_pieces = {}
for i, p in enumerate(g3_pb.pieces):
    if p.type == USER_DEFINED:
        user_defined_pieces[p.piece] = i

```


So this is what their preprocessing code looks like. (Not really, mine is crappy and inefficient. But it's a start.)


```python
def process(txt):
    txt = txt.replace(" ", "▁")
    new_txt = []
    while txt:
        for user_piece in user_defined_pieces:
            if txt.startswith(user_piece):
                new_txt.append(user_piece)
                txt = txt.removeprefix(user_piece)
                break
        else:
            new_txt.append(txt[0])
            txt = txt[1:]
    return new_txt

```


```python
txt = "<start_of_turn>Hello World! <unused0> 🩵<unused1> - ધ્રુવ"
process(txt)

```
```text
['<start_of_turn>',
 'H',
 'e',
 'l',
 'l',
 'o',
 '▁',
 'W',
 'o',
 'r',
 'l',
 'd',
 '!',
 '▁',
 '🩵',
 '▁',
 '-',
 '▁',
 'ધ',
 '્',
 'ર',
 'ુ',
 'વ']

```


Alright, next, we find the pairs which occur most frequently in the training corpus. In the protobuf, there is a field called score. The more the score, more important that piece is than others.  


```python
piece_scores = {
    p.piece: p.score for p in g3_pb.pieces
}

```


```python
def get_candidate_scores(txt):
    scores = {}
    for i in range(1, len(txt)):
        if txt[i] in user_defined_pieces or txt[i-1] in user_defined_pieces:
            continue
        candidate = txt[i-1] + txt[i]
        if candidate not in piece_scores: continue
        scores[candidate] = piece_scores[candidate]
    return scores

```


```python
get_candidate_scores(process("<start_of_turn>Hello"))

```
```text
{'He': -1715.0, 'el': -41.0, 'll': -365.0, 'lo': -350.0}

```


Thus, we will merge `el`. Then we will repeat the process for `[<start_of_turn> H el l o]`.


```python
def merge(txt, to_merge):
    new_txt = []
    merged = False
    i = 0
    while i < len(txt):
        if txt[i] in user_defined_pieces:
            new_txt.append(txt[i])
            i += 1
        elif i < len(txt)-1:
            if txt[i+1] in user_defined_pieces:
                new_txt.extend(txt[i:i+2])
                i += 2
            else:
                candidate = txt[i] + txt[i+1]
                if candidate == to_merge:
                    merged = True
                    new_txt.append(to_merge)
                    i += 2
                else:
                    new_txt.append(txt[i])
                    i += 1
        else:
            new_txt.append(txt[i])
            break
    return new_txt, merged

```


```python
candidates = get_candidate_scores(process("Hello"))
nxt = max(candidates, key=candidates.get)
print(nxt)

```
el



```python
def tokenize(txt):
    txt = process(txt)
    merged = True
    while merged:
        candidates = get_candidate_scores(txt)
        if not candidates: break
        to_merge = max(candidates, key=candidates.get)
        txt, merged = merge(txt, to_merge)
    return txt

```


```python
txt = "<start_of_turn> Hello World! How are you doing! - ધ્રુવ"

```


```python
tokenize(txt) == g3.encode_as_pieces(txt)

```
```text
True

```


Yay!


or Nay?


```python
tokenize("🫩"), g3.encode_as_pieces("🫩")

```
```text
(['\U0001fae9'], ['<0xF0>', '<0x9F>', '<0xAB>', '<0xA9>'])

```


It's nay. Because, we forgot about byte fallback. You see, "🫩" was added to Unicode in December 2024. So, it is not widely used emoji. So, there is no integer id for that piece, as it is not a piece. In cases like this, byte fallback is used. 


```python
def post_process(txt):
    pieces = []
    for p in txt:
        if p in user_defined_pieces or p in piece_scores:
            pieces.append(p)
        else:
            pieces.extend(f"<0x{b:X}>" for b in p.encode())
    return pieces

```


```python
def tokenize_to_ids(txt):
    pieces = post_process(tokenize(txt))
    return [piece_to_id[p] for p in pieces]

```


```python
for txt in txts:
    assert tokenize_to_ids(txt) == g3.tokenize(txt)

```


# Efficient Implementation Ideas


There are many things you can do to improve the performance. Our preprocess function is very very suboptimal. It's quadratic. For each user defined token, we check if our string has that prefix. If it is, we remove the prefix. A better data structure would be Trie. But, I won't use trie. I found state machine (which can be thought of compact trie) to be easier to write.

Let's do some rudimentary benchmarking. 


```python
%%timeit

tokenize("""The given statement (which doesn't require quote marks) is run via the LineProfiler. Profiling is enabled for the functions specified by the -f options. The statistics will be shown side-by-side with the code through the pager once the statement has completed.""")

```
46.1 ms ± 1.26 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)



Got it. Let's check how much time is spent in preprocessing.


```python
%load_ext line_pr   ofiler
%lprun -f tokenize  tokenize("""The given statement (which doesn't require quote marks) is run via the LineProfiler. Profiling is enabled for the functions specified by the -f options. The statistics will be shown side-by-side with the code through the pager once the statement has completed.""")

```
Timer unit: 1e-09 s

Total time: 0.148539 s
File: /tmp/ipykernel_22214/2407760563.py
Function: tokenize at line 1

Line #      Hits         Time  Per Hit   % Time  Line Contents
==============================================================
     1                                           def tokenize(txt):
     2         1  131657030.0    1e+08     88.6      txt = process(txt)
     3         1        160.0    160.0      0.0      merged = True
     4       146      19612.0    134.3      0.0      while merged:
     5       146    7475920.0  51204.9      5.0          candidates = get_candidate_scores(txt)
     6       146      22430.0    153.6      0.0          if not candidates: break
     7       145     351242.0   2422.4      0.2          to_merge = max(candidates, key=candidates.get)
     8       145    9012017.0  62151.8      6.1          txt, merged = merge(txt, to_merge)
     9         1        779.0    779.0      0.0      return txt


Whoa. That is whopping 90%. Well I'm not suprised. Let's try to optimize this using State Machine. The idea is, you start in start state. Then you read byte by byte (you can read codepoint by codepoint as well, they are the same). Each time you read a byte, you transition from one state to another. Each state is either valid or invalid. You always keep track of a last valid state. 

For example, say you have strings "abcd" and "ab". A state machine could look like below. `[a -> 1]` means if you read a, goto 1. 
```
state 0: start state [a -> 1]
state 1: a (invalid) [b -> 2]
state 2: ab (valid)  [c -> 3]
state 3: abc (invalid) [d -> 4]
state 4: abcd (valid)
```
if your string is "babd", you would do something like below. Here `[0]` means you are in this state.

- `[0]`. Read b. No transition. emit b is not a valid prefix.
- `[0]`. Read a. Goto 1.
- `[1]`. Read b. Goto 2.
- `[2]`. Read d. No valid transition. Since the last valid state was 2, we emit "ab", and start from the next byte after "ab". 


```python
class StateMachine:
    def __init__(self, strings):
        is_valid = {}
        states = [[None]*256]  # 0 is the initial state. None entry means no transition.
        for string in strings:
            state = 0
            for c in string.encode():
                if states[state][c] is None: 
                    # There is no state created for this prefix. Create a new state with empty transistions.
                    states.append([None]*256)
                    states[state][c] = len(states)-1
                state = states[state][c]
            is_valid[state] = string # mark the final state as valid.
        self.states = states
        self.is_valid = is_valid

    def find_longest_prefix(self, string, i):
        """Finds the longest prefix of the string that is a valid prefix of any of the strings used to create the state machine."""
        state = 0
        last_valid = None
        last_i = i # keeps track of the last index where a valid prefix was found.
        while i < len(string) and (state := self.states[state][string[i]]):
            if state in self.is_valid:
                last_valid = self.is_valid[state]
                last_i = i+1
            i += 1
        return last_valid, last_i

```


```python
sm = StateMachine([p.piece for p in g3_pb.pieces if p.type == 4])

```


```python
len(sm.states)

```
```text
12951

```


```python



# using the first byte of the utf-8 coded character to determine the length of the character.
char_length = [1]*12 + [2,2,3,4] 

# I am overwriting the process function for "educational purposes" 
def process(input_str):
    input_str = input_str.replace(" ", "▁").encode()
    new_txt = []
    i = 0
    while i < len(input_str):
        found, i = sm.find_longest_prefix(input_str, i)
        if found:
            new_txt.append(found)
        else:
            n = char_length[(input_str[i] >> 4)]
            new_txt.append(input_str[i:i+n].decode())
            i += n
    return new_txt

```


```python
for txt in txts:
    assert tokenize_to_ids(txt) == g3.tokenize(txt)

```


```python
%%timeit

tokenize("""The given statement (which doesn't require quote marks) is run via the LineProfiler. Profiling is enabled for the functions specified by the -f options. The statistics will be shown side-by-side with the code through the pager once the statement has completed.""")

```
8.06 ms ± 220 μs per loop (mean ± std. dev. of 7 runs, 100 loops each)



```python
%lprun -f tokenize tokenize("""The given statement (which doesn't require quote marks) is run via the LineProfiler. Profiling is enabled for the functions specified by the -f options. The statistics will be shown side-by-side with the code through the pager once the statement has completed.""")

```
Timer unit: 1e-09 s

Total time: 0.018039 s
File: /tmp/ipykernel_22214/2407760563.py
Function: tokenize at line 1

Line #      Hits         Time  Per Hit   % Time  Line Contents
==============================================================
     1                                           def tokenize(txt):
     2         1     634474.0 634474.0      3.5      txt = process(txt)
     3         1        354.0    354.0      0.0      merged = True
     4       146      18910.0    129.5      0.1      while merged:
     5       146    7488849.0  51293.5     41.5          candidates = get_candidate_scores(txt)
     6       146      21575.0    147.8      0.1          if not candidates: break
     7       145     339697.0   2342.7      1.9          to_merge = max(candidates, key=candidates.get)
     8       145    9534679.0  65756.4     52.9          txt, merged = merge(txt, to_merge)
     9         1        474.0    474.0      0.0      return txt


So, that is a significant speedup. Just ~25 lines of code reduced the speed from 40ms to ~10ms. We see that process function only takes around 2% of the whole thing. Next bottleneck is the `get_candidate_scores`.


Well, you don't need to recompute scores of all the pairs in every loop. After all, all but one pair remains the same.

e.g., "a b c d e f g" => "a b cd e f g". We would only need to recompute "bcd" score and "cde" score after the merging. Other pairs (like ab) don't need to be recomputed. 

We can instead keep a priority queue. I won't do this here, but it could be interesting exercise for interested reader. You can also look at the original sentencepiece implementation to see how they have done it. 

>[!NOTE] I think there are different schools of thoughts on wether to use heap or not. Some folks believe that for short strings just iterating might be faster than using heap. Maybe topic for the next blog?
