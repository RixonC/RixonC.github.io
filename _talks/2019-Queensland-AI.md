---
title: "Distributed Deep Learning for the 5G Era"
collection: talks
type: "Talk"
permalink: /talks/2019-Queensland-AI
venue: "Queensland AI"
date: 2019-08-22
location: "River City Labs, Brisbane, Australia"
---

<img src='/files/qld-ai.jpeg' width='64' href='/'>

<img src='/files/qld-ai-ad.jpeg' width='100%' href='/'>

## Promotion
We’ve all heard that 5G is going to change wireless communication, with incredible bandwidths enabling a new era of connectivity and the realisation of the Internet of Things. (No doubt we’re all looking forward to our grandchildren finally enjoying the internet speeds of the developing world.) With all those devices, there will no doubt be spare computing power for the next generation of citizen science like Folding at Home. Coupled with recent developments in distributed deep learning, perhaps this represents the threshold of a new era of AI. After all, cluster computing and the cloud have been hugely successful in scaling tasks, we can only go upwards. But there’s a problem. Even though 5G promises massive potential increase in transmission speed and volume, communication costs are always the bottleneck in distributed computing.

Enter Rixon Crane, a PhD student from UQ. He sees a world where every mobile phone could be part of a giant supercomputer. Rather than working on making deep learning computationally efficient, he’s building a system that makes deep learning communicationally efficient. By deliberately using expensive local training steps, he’s designed a way to minimise overall worker/server communication rounds, increase the scalability of deep learning training and still ensure efficient convergence. To do this, he uses a technique known as “second order optimisation”, which up until recently had too many limitations to be used in most deep learning optimisation. Plus he came up with a great acronym, which (as we all know) is the hardest part of research and development. Yes, this talk is going to get unavoidably technical, but Rixon has a way with breaking down complex ideas into digestible chunks. So come along, learn about some bleeding edge model training techniques and network with fellow pioneers! This talk promises a vision of the future of distributed computing, and it’s awesome that it’s happening here in Brisbane.

## Comments
**Richard H.**
> The whole speech is pretty inspiring and interesting. The DINGO is not only for the 5G, but it can also be applied to every distributed model. Newton's method was not popular since it needs extra computation to calculate the second-order differential. But the Rixon can use it to benefit the distributed system since the largest cost in the system is transmitting the weights. Informative speech!

**Callum H.**
> As a lowly code monkey, most of that went way over my head, but it sure as heck seemed pretty innovative! I can't wait to see the performance metrics.

**Matthew**
> github.com/RixonC/DINGO <br>
Give this some stars on github. It's more than a little deserved.
