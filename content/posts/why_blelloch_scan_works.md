+++
title = "Why Blelloch Scan Works"
date = "2021-10-02T09:31:44+05:30"
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["parallel-computing", "cuda"]
keywords = ["prefix sum", "parallel algorithm", "cuda"]
description = "A video blog explaining why Blelloch scan works"
showFullContent = false
+++

Blelloch scan is a (exclusive) scan algorithm for parallel computers. A common example of scan is prefix sum.

{{< code language="python" title="sequential.py" >}}

def exclusive_scan(a, op):
    b = [0] # Identity of the op, (for sum and max, it is 0).
    for x in a[:-1]:
        b.append(op(x, b[-1]))
    return b

exclusive_scan([1, 2, 3, 4], lambda x, y: x+y) == [0, 1, 3, 6]

exclusive_scan([1, 2, 3, 4], max) == [0, 1, 2, 3]


{{< /code >}}


This vlog is complementary to the excellent [video description](https://youtu.be/mmYv3Haj6uc) from now archived Udacity CS344 course. The video explains the "how" of the algorithm very well, but I couldn't easily find "why" of the algorithm, neither in that video nor in any other videos on the Internet. So here is my attempt to explain it.

{{< youtube 04QXOwzdIOg >}}