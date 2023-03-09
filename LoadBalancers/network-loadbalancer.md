![image](https://user-images.githubusercontent.com/59710101/224134670-7f5abaa1-585d-40bd-a6f9-d4109645f6a3.png)

![image](https://user-images.githubusercontent.com/59710101/224134836-2f72f889-4e4d-4da0-8383-0d68cd683591.png)

![image](https://user-images.githubusercontent.com/59710101/224134969-74e8c373-2804-4d90-9e22-4a5d8e724fa9.png)


```sh
Person: Now let's talk about network load balancing, which is a regional load balancing service. Network load balancing is a regional, non-proxied load balancing service. In other words, all traffic is passed through the load balancer
00:13
instead of being proxied, and the traffic can only be balanced between VM instances that are in the same region, unlike a global load balancer. This load balancing service uses forwarding rules
00:25
to balance the load of your systems based on the incoming IP protocol data, such as address, port and protocol type. You can use it to load balance UDP traffic
00:35
and to load balance TCP and SSL traffic on ports that are not supported with the TCP proxy and SSL proxy load balancers. The architecture of a network load balancer
00:46
depends on whether you use a back-end service-based network load balancer or a target-pool-based network load balancer. Let's explore these in more detail. New network load balancers can be created
00:59
with a regional back-end service that defines the behavior of the load balancer and how it distributes traffic across its back-end instance groups. Back-end services enable new features that are not supported with legacy target pools,
01:13
such as support for non-legacy health checks, TCP, SSL, HTTP, HTTPS and HTTP/2 auto-scaling with managed instance groups, connection draining and a configurable failover policy. You can also transition an existing target-pool-based network load balancer
01:32
to use a back-end service instead, but what is a target pool resource? A target pool resource defines a group of instances that receive incoming traffic from forwarding rules. When a forwarding rule directs traffic to a target pool,
01:48
the load balancer picks an instance from these target pools based on a hash of the source IP and port and the destination IP and port. These target pools can only be used with forwarding rules
02:00
that can handle TCP and UDP traffic. Now, each project can have up to 50 target pools, and each target pool can only have one health check. Also, all the instances of a target pool must be in the same region,
02:14
which is the same limitation as for the network load balancer.
```
