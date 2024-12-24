+++
title = '容器原理/Cgroup小记'
date = 2023-11-03T22:00:04+08:00
draft = true

tag = ['Container', 'Linux', 'Note', 'Principle', 'Resource Management']
series = 'Container Principle'
+++

## Introduce

> Control Groups provide a mechanism for aggregating/partitioning sets of tasks, and all their future children, into hierarchical groups with specialized behaviour.
> 
> Control Groups 提供了对于聚合/分离的任务以及它们所有的子功能划分到有特殊行为的分层组的机制

    简而言之, 就是可以限制进程的资源使用, 细化对资源的控制. 相关案例: Docker



## References

1. Linux Document - Cgrounp: [Link to]([Index of /doc/Documentation/cgroup-v1/ (kernel.org)](https://www.kernel.org/doc/Documentation/cgroup-v1/))
