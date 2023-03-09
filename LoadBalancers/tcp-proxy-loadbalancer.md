
![image](https://user-images.githubusercontent.com/59710101/224134139-c588b3fd-8427-46e4-bcc1-139cd40c3ec9.png)

![image](https://user-images.githubusercontent.com/59710101/224134330-09079003-1e6f-4436-957d-ea8a21aed10c.png)


```sh
Person: TCP proxy is a global load balancing service for unencrypted, non-HTTP traffic. This load balancer terminates your customer's TCP sessions at the load balancing layer then forwards the traffic to your virtual machine instances
00:13
using TCP or SSL. These instances can be in multiple regions and the load balancer automatically directs traffic to the closest region that has capacity. TCP proxy load balancing supports both IPv4
00:27
and IPv6 addresses for client traffic. Similar to SSL proxy load balancer, the TCP proxy load balancer provides intelligent routing and security patching. For the full list of ports supported by TCP proxy load balancing
00:41
and other benefits please refer to the links section of this video. This network diagram illustrates TCP proxy load balancing. In this example, traffic from users in Iowa and Boston
00:53
is terminated at the global load balancing layer. From there a separate connection established to the closest back-end instance. As in the SSL proxy load balancing example, the users in Boston would reach the US east region
01:09
and the user in Iowa would reach the US central region if there's enough capacity. Now the traffic between the proxy and the backend can use SSL or TCP, and I also recommend using SSL here.

```
