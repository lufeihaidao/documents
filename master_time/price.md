Price, Topology, Global Flow optimiun
=========================================================

## Abstract

Nowadays traffic jam problem is increasingly worse and as a result becomes one of the major bottleneck that restrict the city development. ITS (Intelligent Transportation System) is proposed in order to deal with it which generally combines computer science, information system, communication and control technology. Howerver, many cities in the world has become so crowd that almost no route planning method could effect well enough. In this article, we propose a kind of charging policy to meet with this challenge. Besides, we design a concept of similarity between graphs to reduce computing complexity and a thought that realize global optimal road network if considered the tanglement as a result of traditional shortest-path algorithm.

## Keywords

charging policy, similarity between graphs, global optimal road network

## Introduction

The amount of automotive vehicle is increasing sharply. According to statistics, the number of automotive vehicle in China had reached 120 million by the end of 2012 and would reach 200 million by 2020 which is predicted by Ministry of Industry and Information Technology of the People's Republic of China. The vast number of vehicle in city not only worsens the traffic quality and efficiency but also increases time and money cost which leads to more serious traffic accident, traffic jam and environment pollution. The traffic problem has become one of the major bottleneck that restrict the city development[@Qiao2011].

By studying basic traffic theory, ITS (Intelligent Transportation System) is proposed to generally combines computer science, information system, communication and control technology and apply them to the whole traffic management system[@Dimitrakopoulos2010]. As is well known, ITS is the best way to solve traffic problems including but not limited to traffic jam, worsening transportation quality and efficiency and pollutions as a result.

One of the most important technology in ITS is the intelligentization of traffic guidance system. A typical intelligent traffic guidance flow can be described like this: satellites or other equipment collect positions of probe vehicles and send them to the server through communication network, then the server gets traffic information via analysis and in addition return guidance information to the drivers[@Srivastava2011].

figure or not?

交通问题源于供需关系的不平衡：对路网资源的需求远大于路网资源的供给。从管理者的角度，如欲解决该问题当从两个方面考虑，一是扩大资源的供给，即兴建道路等基础设施，大力发展郊区地区等；二是缓解需求的压力，比如摇号限行，或者针对私家车收费，将一部分路网资源的消耗者从私家车调控到公共交通设施。第一种方法虽然效果比较好，但是在已经渐渐成熟的城市中，一方面可供建造道路的空间依然非常狭小；更一方面，建造道路涉及的事物繁多，往往难以动工。对于第二种方法，摇号限行已经在各大城市开始实施。由于不少大城市中车辆已经趋于饱和，摇号购车措施对于缓解交通压力的作用越来越小。对于限行措施，虽然可以一定程度上缓解交通压力，但是作用并不显著。本文提出一种基于价格体系的最短路径方法，这种方法能够很好的利用经济学的供需关系原理，同时可以自动的得到限行措施追求的结果：不同路段不同时间段，都能有较好的交通流量，尽量减小拥堵现象。同时还针对Dijkstra算法的路网拓扑结构，提出了一种相似图的概念，旨在减小动态交通诱导中的计算量。

现有的问题是什么（比如杭州，北京这样的城市，基本全堵，无论静态还是动态诱导，都很难有显著的效果（开题报告现有问题里有），局部最优的问题，），为什么，设计怎样的方法来解决。

## General System

We proposed a kind of architecture which is shown in figure \ref{general_system}  to serve as an intelligent traffic system. This system is divided into three parts: the client side, internet and the server side. In the client side, the car-mounted terminal would send location infomation to the server every once in a while and the smart phone (which may be replaced by car-mounted terminal) would send a request for guidance infomation and receive it on the other hand. In the server side, our server is designed to implement the following functions: real-time traffic analysis, valuation module, route planning algorithms and guidance infomation digitalizing.

![General System\label{general_system}](general_system.png)

As to the car-mounted terminal, we decide to collect the probe vihicles' position with the help of BD-2, inertial navigation module and supplementary module. BeiDou is Chinese satellite navigation system and was updated to BeiDou-2 (BD2) in 2007. BD-2 system is able to provide basic positioning service in China and the surrounding area now and is designed to gradually cover the earth. It has bee tested that BD-2 performed better than GPS most of time in Chinese mainland in the eyes of visibility, stability and some other aspects[@Chen2010].

The car-mounted terminal is designed to communicate with the server through LTE/4G which will become the most popular communication method in the future due to its better quality, speed and stability.

![Car-mounted Terminal](car_mounted_terminal.png)

## Charging Policy

Considering directed graphs $G=(V,E)$ with $n$ nodes and $m=\Theta (n)$ edges. An edge $(u,v)$ has a nonnegative weight $w(u,v)$. A shortest-path query between a source node $s$ and a target node $t$ asks for the minimum weight $d(s, t)$ of any path from $s$ to $t$. In most route planning practise, the shortest-path algorithm regard the distance as edge weight. 

In our project, we decide to develop shortest-path algorithm which takes price as the edge weight. As shown in figure \ref{pricecontrol}, the traffic jam status is identified with colors. The green color means the road is open or unimpeded (② and ④); The yellow color means the traffic is a little heavy (③); The red color means that traffic is very heavy (①). 

![Pricing System Sketch\label{pricecontrol}](pricecontrol.png)

Suppose that in the unimpeded road each car would cost 1 unit per kilometer which is writtern for $1u$; In the a little heavy road the cost is $3u/km$ and in the very heavy road it is $8u/km$. There are two schemes for one to dirve from A to B: the first is driving alone ① which will cost the driver $40u$ ($5km\times 8u/km$) and the second is driving alone ②③④ which will cost $25u$ ($5\times1+5\times3+5\times1$). Obviously, if we take reasonable charging policy, drivers would automatically keep away from the heavy road without traffic guidance (But actually traffic guidance is still a necessity considering many other issues).

Whether this charging policy would be adopted or not is a administrative and  economic problem. In addition, the charging and distribution policy will definetely raise many calls in question. However, the policy is actually benefical to improving nowadays traffic jam problems.

## Similarity between Graphs

