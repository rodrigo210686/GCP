
![image](https://user-images.githubusercontent.com/59710101/224136091-947fe69e-2add-481b-82d0-5cfdc7880658.png)


![image](https://user-images.githubusercontent.com/59710101/224136207-6749cab2-059e-4107-8149-a028cd91762e.png)

![image](https://user-images.githubusercontent.com/59710101/224136406-c7f42bb3-a66a-4462-bd97-949ac9eb6857.png)

![image](https://user-images.githubusercontent.com/59710101/224136597-2f02f50d-f2eb-43c0-ade0-b29985f23208.png)


```sh
Person: Next let's talk about internal load balancing. The internal TCP/UDP load balancer is a regional private load balancing service for TCP and UDP-based traffic. In other words this load balancer
00:14
enables you to run and scale your services behind a private load balancing IP address. This means that it's only accessible through internal IP addresses or virtual machine instances in the same region.
00:27
Therefore you configure an internal TCP/UDP load balancing IP address to act as the front end to your private back-end instances. Because you don't need a public IP address for you load balanced service your internal client
00:42
requests stay internal to your VPC network and region. This often results in lowered latency because all of your load balanced traffic stays within Google's network making your configuration much simpler.
00:56
Let's talk more about the benefits of using a software-defined internal TCP/UDP load balancing service. Google Cloud internal load balancing is not based on a device or on a VM instance.
01:07
Instead it is software-defined fully distributed load balancing solution. In the traditional proxy model of internal load balancing, as shown on the left, you configure an internal IP address on an load balancing device or instances,
01:21
and your client instance connects to this IP address. Traffic coming to the IP address is terminated at the load balancer, and the load balancer selects a back end to establish a new connection to. Essentially you have two connections,
01:34
one between the client and the load balancer and one between the load balancer and the back end. Google Cloud internal load balancing distributes client instance requests to back ends using a different approach,
01:47
as shown on the right. It uses lightweight load balancing built on top of Andromeda, Google's network virtualization stack, to provide software-defined load balancing that directly delivers the traffic from the client
01:59
instance to a back-end instance. For more information on Andromeda see the link section of this video. Now, Google Cloud's internal HTTPS load balancing is a proxy-based regional layer seven load balancer
02:15
that also enables you to run and scale your services behind an internal load balancing IP address. Back-end services support HTTP, HTTPS and HTTP/2 protocols. Internal HTTPS load balancing is a managed service
02:30
based on the open source Envoy proxy. This enables rich traffic control capabilities based on HTTPS parameters. After the load balancer has been configured it automatically allocates Envoy proxies to meet your traffic's needs.
02:45
Now, internal load balancing enables you to support use cases such as the traditional three-tier web services. In this example, the web tier uses an external HTTPS load balancer that provides a single global IP address for users
03:00
in San Francisco, Iowa, Singapore and so on. The back ends of this load balancer are located in US West One, US Central One and Asia East One regions because this is a global load balancer.
03:14
These back ends then access an internal load balancer in each region as the application or internal tier. The back ends of this internal tier are located in US West One A,
03:26
US Central One B and Asia East One B. The last tier is the data-based tier in each of these zones. The benefit of this three-tier model is that neither the data-based tier
03:38
nor the application tier is exposed externally. This simplifies security and network pricing.

```
