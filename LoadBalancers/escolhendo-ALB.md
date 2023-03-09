
![image](https://user-images.githubusercontent.com/59710101/224148753-1f504a3a-1beb-4bf5-aa70-0c26edda8b2b.png)


![image](https://user-images.githubusercontent.com/59710101/224149416-84c49dd0-b57d-441b-aac9-f0f8a1d73c2b.png)

![image](https://user-images.githubusercontent.com/59710101/224149725-fda91284-46f4-4b3c-a616-797d8299f374.png)

```sh
Person: Now that we have discussed all the different load balancing services within GCP, let me help you determine which load balancer best meets your need. One differentiator between the different GCP load balancers
00:12
is the support for IPv6 clients. Only the HTTPS, SSL proxy and TCP proxy load balancing services support IPv6 clients. IPv6 termination for these load balancers enables you to handle IPv6 requests from your users
00:29
and proxy them over IPv4 to your back end. For example, in this diagram, there is a website, www.example.com, that is translated by cloud DNS to both an IPv4 and IPv6 address.
00:43
This allows a desktop user in New York and a mobile user in Iowa to access the load balancer through the IPv4 and IPv6 addresses respectively. But how does the traffic get to the back ends and their IPv4 addresses?
00:58
Well, the load balancer acts as a reverse proxy, terminates the IPv6 client connection and places the request into an IPv4 connection to a back end. On the reverse path,
01:09
the load balancer receives the IPv4 response from the back end and places it into the IPv6 connection back to the original client. In other words, configuring IPv6 termination for your load balancers
01:22
lets your back-end instances appear as IPv6 applications to your IPv6 clients. Now, in order to decide which load balancer best suits your implementation of GCP, consider the following aspects of Cloud Load Balancing.
01:38
Global versus regional load balancing, external versus internal load balancing, and the traffic type. If you need an external load balancing service, start on the top left of this flowchart.
01:50
First, choose the type of traffic that your load balancer must handle. If that is HTTP or HTTPS traffic, I'd recommend using the HTTPS load balancing service as a layer 7 load balancer.
02:03
Otherwise, use the TCP and UDP traffic paths of this flowchart to determine whether the SSL proxy, TCP proxy or network load balancing service meets your needs. If you need an internal load balancing service,
02:18
you have the internal load balancing service available, and it supports both TCP and UDP traffic. As I mentioned at the beginning of this module, there is actually another internal load balancer for HTTPS traffic,
02:31
but it's in beta as of this recording. The sixth load balancer is for HTTP or HTTPS traffic, and it's regional, meaning for IPv4 clients. If you prefer a table over a flowchart, I'd recommend this summary table.
02:47
This table helps you identify the right load balancer based on the traffic type, the distribution of your back end, global or regional, and the type of IP addresses of your back end, external or internal.
02:59
This table also lists the available ports for load balancing and highlights that only the global load balancers support both IPv4 and IPv6 clients.
```
