# low-latency-grid-landing
A system that takes a feed of landing requests that must determine if one can land in a requested spot given timing and distance requests.

### The Formal Problem Statement

When designing this problem, I really loved problems like the closest pair of points where performance is applied to topics like algorithms and computational geometry. Here, I wanted to explore low-latency programming and dealing with parallelism, concurrency, and multithreading.

Here's what I came up with.

We are given a large, 6400 square foot landing pad. A stream of drones send out requests to land in a particular $(x,y)$ coordinate for $(x,y) \in [0,64] \times [0,64]$. Take such a request $i$ with requested coordinate $(x_i, y_i)$. It sends it out at time $s_i$, and it must receive a decision as to if it can land by time $f_i$. In other words, we must respond to it between $f_i - s_i$. In addition, if cleared to land, it will stay there for duration $d_i$ before it is automatically evicted.

We will say that no two drone requests $i,j$ cannot land within some fixed distance $D = 30$ feet of each other. A request is accepted if it is cleared to land in its requested coordinate within the time window. A request is rejected if within the window, a drone can't land in its requested coordinate. A request expires if we don't make a decision within that requests time window.

The goal is to maximize responsiveness; in other words, in either a finite or infinite stream, maximize the number of requests that we respond to within their windows without allowing them to expire.
