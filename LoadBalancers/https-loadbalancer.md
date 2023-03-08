## HTTPS Load Balancer
![image](https://user-images.githubusercontent.com/59710101/223779771-18fffd7c-0abe-4eea-9b18-3378018d9247.png)

![image](https://user-images.githubusercontent.com/59710101/223779941-2bd2abb5-b662-42f0-8b10-a01d25754e99.png)

![image](https://user-images.githubusercontent.com/59710101/223780155-34b9e50f-cf6b-4304-9609-0fb2e5a7a763.png)


```sh
Person: Now let's talk about HTTPS load balancing which acts at layer seven of the OSI model. This is the application layer which deals with the actual content of each message
00:11
allowing for routing decisions based on the URL. GCPs HTTPS load balancing provides global load balancing for HTTPS requests destined for your instances. This means that your applications are available to your customers
00:26
at a single Anycast IP address which simplifies your DNS setup. HTTPS load balancing balances HTTP and HTTPS traffic across multiple back-end instances and across multiple regions. HTTP requests are load balanced on port 80 or 8080
00:45
and HTTPS requests are load balanced on port 443. This load balancer supports both IPv4 and IPv6 clients, is scalable, requires no prewarming and enables content-based and cross regional load balancing.
01:00
You can configure URL maps that route some URLs to one set of instances and route other URLs to other instances. Requests are generally routed to the instance group that is closest to the user.
01:13
If the closest instance group does not have sufficient capacity, the request is sent to the next closest instance group that does have the capacity. You will get to explore most of these benefits in the first lab of the module.
01:27
Let me walk through the complete architecture of an HTTPS load balancer by using this diagram. A global forwarding rule directs incoming requests from the Internet to a target HTTP proxy.
01:41
The target HTTP proxy checks each request against a URL map to determine the appropriate back-end service for the request. For example, you can send requests for www.example.com/audio to one back-end service
01:56
which contains instances configured to deliver audio files, and the requests for www.example.com/video to another back-end service which contains instances configured to deliver video files. The back-end service directs each request
02:13
to an appropriate back-end based on serving capacity, zone and instance held of its attached backends. The back-end services contain a health check, session affinity, a time out setting and one or more backends.
02:28
A health check pulls instances attached to the back-end service at configured intervals. Instances that pass the health check are allowed to receive new requests. Unhealthy instances are not sent requests until they are healthy again.
02:43
Normally HTTPS load balancing uses a round Robin [Indistinct] to distribute requests among available instances. This can be overridden with session affinity. Session affinity attempts to send all requests from the same client
02:58
to same virtual machine instance. Back-end services also have a time out setting which is set to 30 seconds by default. This is the amount of time the back-end service
03:09
will wait on the backend before considering the request a failure. This is a fixed time out, not an idle time out. If you request longer lived connections set this value appropriately.
03:21
The backends themselves contain an instance group, a balancing mode and a capacity scaler. An instance group contains virtual machine instances. The instance group may be a managed instance group with or
03:34
without auto scaling or an unmanaged instance group. A balancing mode tells the load balancing system how to determine when the backend is at full usage. If all the backends for the back-end service in a region
03:48
are at the full usage, new requests are automatically routed to the nearest region that can still handle requests. The balancing mode can be based on CPU utilization or requests per second.
04:02
A capacity setting is an additional control that interacts with the balancing mode setting. For example, if you normally want your instances to operate at a maximum of 80 percent CPU utilization
04:16
you would set your balancing mode to 80 percent CPU utilization and your capacity to 100 percent. If you want to cut instance utilization in half, you could leave the balancing mode at 80 percent CPU utilization
04:29
and set capacity to 50 percent. Now any changes to your back-end services are not instantaneous, so don't be surprised if it takes several minutes for your changes to propagate throughout the network.

```

![image](https://user-images.githubusercontent.com/59710101/223781454-559cd3b1-5661-4c23-8773-0294225a4ccb.png)

![image](https://user-images.githubusercontent.com/59710101/223783569-f7d63790-693c-45c0-90cf-5fca1eeb5483.png)



```sh
Person: Let me walk through an HTTP load balancer in action. The project on this slide has a single global IP address, but users enter the Google Cloud Network from two different locations, one in North America and one in EMEA.
00:15
First, the global forwarding rule directs incoming requests to the target HTTP proxy. The proxy checks the URL map to determine the appropriate backend service for the request. In this case, we're serving a guestbook application
00:30
with only one backend service. The backend service has two back ends, one in US Central 1A and one in Europe West 1D. Each of those back ends consists of a managed instance group.
00:44
Now when a user request comes in, the load-balancing service determines the approximate origin of the request from the source IP address. The load-balancing service also knows the locations of the instances
00:58
owned by the backend service, their overall capacity and their overall current usage. Therefore, the instances closest to the user have available capacity, the request is forwarded to that closest set of instances.
01:13
In our example, traffic from the user in North America would be forwarded to the managed instance group in US Central 1A, and the traffic from the user in EMEA
01:23
would be forwarded to the managed instance group in Europe West 1D. If there are several users in each region, the incoming requests to the given region are distributed evenly across all available backend services and instances in that region.
01:41
If there are no healthy instances with available capacity in a given region, the load balancer instead sends the request to the next closest region with available capacity. Therefore, traffic from the EMEA user could be forwarded
01:57
to the US Central 1A back end if the Europe West 1D back end does not have capacity or has no healthy instances as determined by the health checker. This is referred to as cross-region load balancing.
02:12
Another example of an HTTPS load balancer is a content-paste load balancer. In this case, there are two separate backend services that handle either web or video traffic. The traffic is split by the load balancer based on the URL header
02:28
as specified in the URL map. If the user is navigating to /video, the traffic is sent to the backend video service, and if the user is navigating anywhere else,
02:39
the traffic is sent to the web service back end. All of that is achieved with a single global IP address.

```

![image](https://user-images.githubusercontent.com/59710101/223784232-c1656018-db94-40ad-91ea-1eeb9d780456.png)

![image](https://user-images.githubusercontent.com/59710101/223784297-f0177b06-986f-4e9e-99fb-e7b3364f78a4.png)

![image](https://user-images.githubusercontent.com/59710101/223784439-dc42a25a-aed4-4834-ba8c-c725b11799fa.png)

![image](https://user-images.githubusercontent.com/59710101/223784776-4a2a93ff-52ac-42c8-95bf-cafa07992888.png)


```sh
Person: A HTTPS load balancer has the same basic structure as a HTTP load balancer, but it differs in the following ways. A HTTPS load balancer uses a target HTTPS proxy
00:12
instead of a target HTTP proxy. A HTTPS load balancer requires at least one signed SSL certificate installed on the target HTTPS proxy for the load balancer. The client SSL sessions terminate at the load balancer.
00:30
HTTPS load balancers support the quick transport layer protocol. QUIC is a transport layer protocol that allows for faster client connection initiation, eliminates head-of-line blocking in multiplex streams, and supports connection migration when a client's IP address changes.
00:48
For more information on the QUIC protocol, see the link in the course resources. To use HTTPS, you must create at least one SSL certificate that can be used by the target proxy for the load balancer.
01:01
You can configure the target proxy with up to 15 SSL certificates. For each SSL certificate, you need to create an SSL certificate resource which contains the SSL certificate information.
01:14
SSL certificate resources are only used with load balancing proxies such as a target HTTPS proxy or target SSL proxy, which we'll discuss later in this module. Back-end buckets allow you to use Google Cloud Storage buckets
01:28
with HTTPS load balancing. An external HTTPS load balancer uses a URL map to direct traffic from specified URLs to either a back-end service or a back-end bucket. One common use case is send requests for dynamic content,
01:45
such as data, to a back-end service, and send requests for static content, such as images, to a back-end bucket. In this diagram, the load balancer sends traffic with a path
01:56
of /love-to-fetch to a Cloud Storage bucket in the Europe North region. All the other requests go to a Cloud Storage bucket in the U.S. East region. After you configure a load balancer with the back-end buckets,
02:10
requests to URL paths that begin with /love-to-fetch are sent to the Europe North Cloud Storage bucket, and all other requests are sent to the U.S. East Cloud Storage bucket.
02:23
A network endpoint group, or NEG, is a configuration object that specifies a group of back-end endpoints or services. A common use case for this configuration is deploying services in containers.
02:36
You can also distribute traffic in a granular fashion to applications running on your back-end instances. You can use NEGs as back ends for some load balancers and with Traffic Director.
02:47
Zonal and Internet NEGs define how endpoints should be reached, whether they are reachable and where they are located. Unlike these NEG types, serverless NEGs don't contain endpoints. A zonal NEG contains one or more endpoints
03:04
that can be Compute Engine VMs or services running on the VMs. Each endpoint is specified by either an IP address or an IP [Indistinct] port combination. An Internet NEG contains a single endpoint
03:19
that is hosted outside of Google Cloud. This endpoint is specified by host name FQDN:port or IP:port. A hybrid connectivity NEG points to Traffic Director services running outside of Google Cloud.
03:34
A serverless NEG points to Cloud Run, App Engine, Cloud Functions services residing in the same region as the NEG. For more information on using NEGs, please see the link in course resources.
```
