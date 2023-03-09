![image](https://user-images.githubusercontent.com/59710101/224133012-9d1ef954-8327-458c-bd7e-2dcd202534e8.png)

![image](https://user-images.githubusercontent.com/59710101/224133674-c7310849-0765-4966-a5c3-ee752565df10.png)


```sh
Person: Let's talk about SSL proxy and TCP proxy load balancing.
00:04
SSL proxy is a global load balancing service for encrypted non-HTTP traffic.
00:10
This load balancer terminates user SSL connections at the load balancing layer, then balances the connections across your instances using the SSL or TCP protocols.
00:21
These instances can be in multiple regions and the load balancer automatically directs traffic to the closest region that has capacity.
00:29
SSL proxy load balancing supports both IPv4 and IPv6 addresses for client traffic and provides intelligent routing, certificate management, security patching and SSL policies.
00:43
Intelligent routing means that this load balancer can route requests to back-end locations where there is capacity.
00:50
From a certificate management perspective, you only need to update your customer-facing certificate in one place when you need to switch those certificates.
01:00
Also you can reduce the management overhead for your virtual machine instances by using self-signed certificates on your instances.
01:08
In addition, if vulnerabilities arise in the SSL or TCP stack, GCP will apply patches at the load balancer automatically in order to keep your instances safe.
01:19
For the full list of ports supported by SSL proxy load balancing and other benefits, please refer to the links section of this video.
01:28
This network diagram illustrates SSL proxy load balancing.
01:31
In this example, traffic from users in Iowa and Boston is terminated at the global load balancing layer.
01:37
From there a separate connection established to the closest back-end instance.
01:42
In other words the user in Boston would reach the US east region, and the user in Iowa would reach the US central region if there's enough capacity.
01:52
Now the traffic between the proxy and the backend can use SSL and TCP.
01:58
I recommended using SSL.
```
