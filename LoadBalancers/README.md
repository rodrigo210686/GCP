## Informações

![image](https://user-images.githubusercontent.com/59710101/223777328-12e8675b-d75f-489a-8010-0fc047c183f2.png)


``` sh
In this module, we focus on load balancing and autoscaling. Cloud Load Balancing gives you the ability to distribute load-balanced compute resources in single or multiple regions to meet your high availability requirements,
00:13
to put your resources behind a single anycast IP address and to scale your resources up or down with intelligent autoscaling. Using Cloud Load Balancing, you can serve content as close as possible to your users
00:27
on a system that can respond to over 1 million queries per second. Cloud Load Balancing is a fully distributed, software-defined managed service. It is not instance or device-based, so you do not need to manage a physical load balancing infrastructure.
00:43
GCP offers different types of load balancers that can be divided into two categories, global and regional. The global load balancers are the HTTP, HTTPS, SSL proxy and TCP proxy load balancers.
00:58
These load balancers leverage the Google front ends, which are software-defined, distributed systems that sit in Google's point of presence and are distributed globally. Therefore, you want to use a global load balancer
01:10
when your users and instances are globally distributed, your users need access to the same application and content, and you want to provide access using a single anycast IP address.
01:22
The regional load balancers are the internal and network load balancers, and they distribute traffic to instances that are in a single GCP region. The internal load balancer uses Andromeda,
01:33
which is GCP's software-defined network virtualization stack, and the network load balancer uses Maglev, which is a large, distributed software system. There is also another internal load balancer for HTTP,
01:47
HTTPS traffic. The sixth load balancer is a proxy-based regional layer 7 load balancer that enables you to run and scale your services behind a private load-balancing IP address that is accessible only in the load balancer's region in your VPC network.
02:05
In this module, we will cover the different types of load balancers that are available in GCP. We will also go over the managed instance groups and their autoscaling configurations,
02:15
which can be used by these load balancing configurations. You will explore many of the covered features and services throughout the two labs of this module. And I will wrap things up by helping you determine
02:27
which GCP load balancer best meets your needs. Let's start by talking about managed instance groups.

```
