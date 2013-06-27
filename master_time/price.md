Price, Topology, Global Flow optimiun
=========================================================

## Abstract

Nowadays traffic jam problem is increasingly worse and as a result becomes one of the major bottleneck that restrict the city development. ITS (Intelligent Transportation System) is proposed in order to deal with it which generally combines computer science, information system, communication and control technology. Howerver, many cities in the world has become so crowd that almost no route planning method could effect well enough. In this article, we propose a kind of charging policy to meet with this challenge. Besides, we design a concept of similarity between graphs to reduce computing complexity and a thought that realize global optimal road network if considered the tanglement as a result of traditional shortest-path algorithm.

## Keywords

charging policy, similarity between graphs, global optimal road network

## Introduction

城市机动车的数量激增，据统计，截至2012年底，中国汽车数量已达到1.2亿辆，工信部预计在2020年将达到2亿辆。城市中大量的机动车使得交通质量恶化，行车效率低下，增加了时间损失和费用消耗，进而使得交通事故、交通拥堵和环境污染等问题日益严重。成为制约社会可持续发展的一大瓶颈。
无论是发达国家还是发展中国家，都遭遇不同程度交通问题的困扰。据美国德州运输研究所对美国39个主要城市的研究，估计美国每年因交通阻塞而造成的经济损失约410亿美元，12个最大城市每年的经济损失均超过10亿美元。日本东京每年因交通拥堵造成的时间损失以货币单位计算高达123000亿日元。欧洲每年因交通事故、交通拥堵造成的经济损失分别为500亿欧元和5000亿欧元。

用高新技术改造传统产业，提高交通运输整体效率和水平，已经成为各国共识。智能交通系统是通过研究交通关键基础理论模型，将计算机处理技术、数据通信技术、信息技术和电子控制技术等有效的应用于整个交通管理体系的综合系统。ITS在道路、车辆和出行者之间建立起智能联系，最大程度的调整道路交通运行状态，从而保障人、车、路的协调与统一，在提高道路运行效率的同时，充分保障道路交通安全，提高能源利用率和改善环境质量。所以ITS是目前公认的解决城市交通拥堵、改善行车安全、提高运行效率、减少车辆对空气的污染的最佳途径，也是交通运输领域研究的前沿课题。

ITS中的关键技术之一是交通诱导系统的智能化。它以实时动态分配理论为核心，动态地向驾驶员提供最优路径引导指令和丰富的实时交通信息，通过诱导车辆来改善路面交通状况。本文主要讨论交通诱导中路径规划算法中的一些改进概念。
这里可以配张图

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

