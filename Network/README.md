## Types of routing
https://cloud.google.com/blog/products/networking/introducing-network-service-tiers-your-cloud-network-your-way

https://en.wikipedia.org/wiki/Hot-potato_and_cold-potato_routing


![image](https://user-images.githubusercontent.com/59710101/213186352-1b3c005c-6af4-418d-81fb-7a8031f3cddc.png)


## Load Balancer
https://cloud.google.com/load-balancing/docs/load-balancing-overview

https://cloud.google.com/load-balancing/docs/choosing-load-balancer


## VPC
https://cloud.google.com/vpc/docs/vpc#subnet-ranges

https://cloud.google.com/vpc/docs/vpc


### ROLES, Service accounts, IAM
https://cloud.google.com/compute/docs/access/service-accounts
https://cloud.google.com/iam/docs/creating-custom-roles
https://cloud.google.com/iam/docs/understanding-custom-roles

### Pricing

![image](https://user-images.githubusercontent.com/59710101/215999671-64e7f891-bdf8-46c7-aa34-c78e2f6328fd.png)

![image](https://user-images.githubusercontent.com/59710101/216000253-8df039ca-7ee6-47c2-939e-08891048ead5.png)


### Cloud Nat

![image](https://user-images.githubusercontent.com/59710101/216009716-a221f129-0ad3-4fd2-a69e-0ef0b68909db.png)

### Private google access 

![image](https://user-images.githubusercontent.com/59710101/216010180-92882d74-78ea-405c-8184-ab993f4bdfdb.png)

### Shared VPC

![image](https://user-images.githubusercontent.com/59710101/217641634-f03a7907-6d5c-479d-bf16-6244990f1c8c.png)

![image](https://user-images.githubusercontent.com/59710101/217642605-501a1fa5-a49a-4d5c-8867-8b852e9d7abd.png)

![image](https://user-images.githubusercontent.com/59710101/217642676-de0968c5-9448-4a3a-9c23-6a46b3866df4.png)


```txt
Let's move our attention from hybrid connectivity to shared VPC networks. In the simplest cloud environment, a single project might have one VPC network spanning many regions with VM instances
00:13
hosting very large and complicated applications. However, many organizations commonly deploy multiple isolated projects with multiple VPC networks and subnets. In this lesson, we are going to cover two configurations
00:30
for sharing VPC networks across GCP projects. First, we will go over shared VPC, which allows you to share a network across several projects in your GCP organization. Then we will go over VPC network peering,
00:46
which allows you to configure private communication across projects in same or different organizations. Shared VPC allows an organization to connect resources from multiple projects to a common VPC network.
01:01
This allows the resources to communicate with each other securely and efficiently using internal IPs from that network. For example, in this diagram, there's one network that belongs to the web application service project.
01:16
This network is shared with three other projects, namely the recommendation service, the personalization service, and the analytics service. Each of those service projects has instances that are in the same network as the web application server
01:31
and allow for private communication to that server using the internal IP addresses. The web application server communicates with clients and on-premises using the server's external IP address. The backend services in contrast cannot be reached externally
01:48
because they only communicate using internal IP addresses. When you use shared VPC, you designate a project as a host project and attach one or more other service projects to it.
02:02
In this case, the web application service project is the host project and the three other projects are the service projects. The overall VPC network is called the shared VPC network.
02:15
VPC network peering in contrast, allows private RFC 1918 connectivity across two VPC networks, regardless of whether they belong to the same project or the same organization. Now, remember that each VPC network will have firewall rules
02:33
that define what traffic is allowed or denied between the networks. For example, in this diagram, there are two organizations that represent a consumer and a producer respectively. Each organization has its own organization node, VPC network,
02:50
virtual machine instances, network admin, and instance admin. In order for VPC network peering to be established successfully, the producer network admin needs to pure the producer network with the consumer network and the consumer network admin
03:06
needs to pair the consumer network with the producer network. When both peering connections are created, the VPC network peering session becomes active and routes are exchanged. This allows the virtual machine instances to communicate
03:20
privately using their internal IP addresses. VPC network peering is a decentralized or distributed approach to multi project networking. Because each VPC network may remain under the control of separate administrator groups
03:37
and maintains its own global firewall and routing tables. Historically, such projects would consider external IP addresses or VPNs to facilitate private communication between VPC networks. However, VPC network peering does not incur the network latency, security
03:56
and cost drawbacks that are present when using external IP addresses or VPNs. Now that we've talked about shared VPC and VPC network peering, let me compare both of these configurations to help you decide
04:10
which is appropriate for a given situation. If you want to configure a private communication between VPC networks in different organizations, you have to use VPC network peering, shared VPC only works within the same organization.
04:26
Somewhat similarly, if you want to configure private communication between VPC networks in the same project, you have to use VPC network peering. This doesn't mean that the networks need to be in the same project,
04:40
but they can be, shared VPC only works across projects. In my opinion, the biggest difference between the two configurations is the network administration models. Shared VPC is a centralized approach to multi project networking.
04:57
Because security and network policy occurs in the single designated VPC network. In contrast, VPC network peering is a decentralized approach, because each VPC network can remain under the control
05:11
of separate administrator groups and maintains its own global firewall and routing tables.

```



