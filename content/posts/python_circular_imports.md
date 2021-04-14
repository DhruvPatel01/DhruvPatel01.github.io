+++
title = "Python got me with circular imports!"
date = "2021-04-14T21:51:48+05:30"
author = "Dhruv Patel"
cover = ""
tags = ["python-gotcha", "python"]
keywords = ["python circular imports"]
description = "Yet another way circular import can get you. This blog describes how Python import works, why circular imports cause issue and how to fix it."
showFullContent = false
draft = false
+++

I have been programming in Python from last seven years. Apart from the new features Python adds in every new release, I didn't think Python would surprise me, until it did.

I will demonstrate what happened with the trimmed down code. I have two files, `main.py` and `notmain.py`. `main.py` has a global variable called `var`. `notmain` has some code that would process user input and add entry into `main.var`. Pretty simple, right?

{{< code language="python" title="main.py" expand="Hide" collapse="Hide" >}}
import notmain

var = {}

def work():
    print("Before:", var)
    notmain.populate()
    print("After: ", var)

if __name__ == '__main__':
    work()

{{< /code >}}

{{< code language="python" title="notmain.py" expand="Hide" collapse="Hide" >}}
import main

def populate():
    main.var['answer'] = 42
{{< /code >}}

What do you think will happen when I run `python main.py`? Don't know about you, but I imagined that after I call `notmain.populate`, `main.var` will have one key, value in it.

```
Shell> python main.py
Before: {}
After:  {}
```

But boy I was wrong. To explain what just happened, let me try to explain how Python imports work.

## How does Python import work? (A simple version)

In what follows, I only explain what happens when you use `import x`. `from x import y` is not explained here.

When you import a module, two steps happen.
1. Search (done by finder)
2. Load (done by loader)

In the search step, `sys.modules` is the first place checked. If the module is not in `sys.modules`, Python will search for that module in other ways, current directory being one of them. Once the module(which was not in `sys.modules`) is found, it will be added to `sys.modules` before step 2 is executed. Thus if `a` imports `b`, and `b` imports `c`, and `c` imports `b`, `b` will not be executed again.

If the module was not found in `sys.modules`, the loading step will execute the module and the exported variables will be made available in the importee module.

One thing you should note is that everything in Python is an object. Even the imported module is. Try this,

```python
import math, types
assert isinstance(math, types.ModuleType)
```

Objects are stored somewhere in memory. Try this,
```python
print(hex(id(math)))
# printed '0x7f7e21029c20' on my machine
```

So everything in the object module will be available as attributes.

Now that we know how import works, let's try to see what happened with my code.

## What happened with my code?

Let's augment the files to print location of `var` object. That shall give some ideas.

{{< code language="python" title="main.py" expand="Hide" collapse="Hide" >}}
import notmain

var = {}
print("In Main: ", hex(id(var)))

def work():
    print("Before:", var, 'at', hex(id(var)))
    notmain.populate()
    print("After: ", var, 'at', hex(id(var)))


if __name__ == '__main__':
    work()
{{< /code >}}

{{< code language="python" title="notmain.py" expand="Hide" collapse="Hide" >}}
import main

def populate():
    main.var['answer'] = 42
    print('In not main: ', main.var, 'at', hex(id(main.var)))

{{< /code >}}

```
Shell> python main.py
In Main:  0x7f64e4778cc0
In Main:  0x7f64e490c6c0
Before: {} at 0x7f64e490c6c0
In not main:  {'answer': 42} at 0x7f64e4778cc0
After:  {} at 0x7f64e490c6c0
```

First of all notice that `In Main: ...` line is printed two times. In the previous section I did tell that **if the module is found in `sys.modules`**, the module will not be executed again. The problem is that `main.py` is only imported once, but executed twice.

Here is what happens.
- `python main.py` starts executing.
- The first line is `import notmain`. Since `notmain` is not in `sys.modules` yet, it will be executed next. Notice that `main` was never imported. So `sys.modules` does not have an entry for `main`.
- Control goes to `notmain.py`. First line of it is `import main`, and as `main` is not in the cache, finder adds it into `sys.modules` and then loader starts executing `main.py` (again!).
- Control goes to `main.py`. Since the first line is `import notmain` and `notmain` **is in** the `sys.modules` now, there is no effect.
- Next line in `main.py` creates a variable `var@0x7f64e4778cc0`.
- Next few lines defines a function `work`. 
- The `__name__ == '__main__'` condition is false, as at the moment `__name__ == 'main'`
-  Control goes back to `notmain.py`. Attributes from the `main` module will now be accessible.
- `populate` is defined in `notmain`.
- Control comes back to `main`. 
- Variable `var` is created (again!) and stored at `0x7f64e490c6c0`. Notice that there are two `var` variables. `notmain` has no idea that there is another `var` at `0x7f64e490c6c0`, it still thinks that `main.var` is at `0x7f64e4778cc0`.
- `work` function is defined.
- `__name__ == '__main__'` condition evaluates to true this time. So `work` is called, which calls `notmain.populate`.
- `notmain.populate` adds `answer` key into `main.var` and not `__main__.var`.

The issue is self-evident now. We need to distinguish between `main` and `__main__`. A simple solution is to create another file that imports `main` and then calls `main.work`. This way when `notmain` calls import, `sys.modules` will already have an entry for `main` and `main` will not be executed again, and both `main` and `notmain` have same view of `var`. So let's try this.

{{< code language="python" title="really_main.py" >}}
import main

main.work()

# no change in other files
{{< /code >}}


```
Shell> python really_main.py
Before:  {}
After:   {'answer': 42}
```

Whooo! That worked.

## Comments?
You have any doubts? Any feedbacks? Please reach out to me at `hello at domain` with subject line `Comment: Post title`. I'll get back to you as soon as possible.
