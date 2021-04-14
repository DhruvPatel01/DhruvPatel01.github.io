---
title: "NotAeroCalc Part 2: How does unit conversion work?"
date: 2021-04-11T18:30:00+05:30
tags: ["science", "aero", "physics", "python", "ply", "yacc", "lex"]
draft: true
---

In this post I will be explaining how exactly the unit conversion parts of NotAeroCalc were implemented. This post is more useful to Computer Science students who might have or are going to take a course related to Compilers.

Before you read ahead, I encourage you to read [Ply Documentation](https://ply.readthedocs.io/en/latest/). The documentation is succinct and helpful. You don't actually need to have taken a course in Compiler Design to understand the documentation. Once you have read that, please also read the [example calculator code](https://github.com/dabeaz/ply/blob/master/example/calc/calc.py). This calculator is the base of NotAeroCalc. In just around 100 lines of code you will have simple calculator ready.

I chose to use [Python Prompt Toolkit](https://python-prompt-toolkit.readthedocs.io/en/master/) instead of default `input` function to ask for input because Prompt Toolkit allows emacs bindings that UNIX users are familiar from their shell. It also allows to remember the history, so one can use the up arrow key multiple time to repeat the command from previous session. You can also use `Ctrl+R` in the NotAeroCalc to search for previous command. All thanks to Python Prompt Toolkit.

```python
from prompt_toolkit import print_formatted_text as print
from prompt_toolkit import PromptSession
from prompt_toolkit.history import FileHistory

session = PromptSession(history=FileHistory(os.path.expanduser('~/.aerocalc_history')))

while True:
    try:
        s = session.prompt('NotAeroCalc > ')
    except EOFError:
        break # When `Ctrl+D` is pressed, exit the while loop
    except KeyboardInterrupt:
        continue # when user presses `Ctrl+C` don't terminate but restart the line

    if not s:
        continue

    # code to evaluate s and output the result.
```
