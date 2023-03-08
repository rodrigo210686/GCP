## AutoScanling and Health Checks

![image](https://user-images.githubusercontent.com/59710101/223778742-28cc42c3-1f61-4be7-bfb7-05e9b1121195.png)



```sh
Person: Let me provide more details on the autoscaling and health checks of the managed instance group. As I mentioned earlier, managed instance groups offer autoscaling capabilities that allow you to automatically add
00:13
or remove instances from a managed instance group based on increase or decrease in load. Autoscaling helps your applications gracefully handle increase in traffic and reduces cost when the need for resources is lower.
00:27
You just define the autoscaling policy, and the autoscaler performs automatic scaling based on the measured load. Applicable autoscaling policies include scaling based on CPU utilization, load-balancing capacity or monitoring metrics
00:43
or via queue-based workload like Cloud [Indistinct]. For example, let's assume you have two instances that are at 100 percent and 85 percent CPU utilization as shown on the slide.
00:55
If your target CPU utilization is 75 percent, the autoscaler will add another instance to spread out the CPU load and stay below the 75 percent target CPU utilization. Similarly, if the overall load is much lower than the target,
01:12
the autoscaler will remove instances as long as that keeps the overall utilization below the target. Now you might ask yourself, "How do I monitor the utilization of my instance group?"
01:24
When you click on an instance group or even an individual virtual machine, a graph is presented. By default, you'll see the CPU utilization over the past hour, but you can change the time frame
01:37
and visualize other metrics like disk and network usage. These graphs are very useful for monitoring your instance's utilization and for determining how best to configure your autoscaling policy to meet changing demands.
01:52
If you monitor the utilization of your virtual-machine instances and Stackdriver monitoring, you can even set up alerts through several notification channels. For more information on autoscaling, see the links section of this video.
02:06
Another important configuration for a managed instance group and load balancer is a health check. A health check is very similar to an uptime check in Stackdriver. You just define a protocol, port and health criteria
02:20
as shown in this screenshot. Based on this configuration, GCP computes a health state for each instance. The health criteria defines how often to check whether an instance is healthy. That's the check interval.
02:35
How long to wait for a response, that's the time-out. How many successful attempts are decisive, that's the healthy threshold. And how many failed attempts are decisive, that's the unhealthy threshold. In the example on this slide,
02:51
the health check would have to fail twice over a total of 15 seconds before an instance is considered unhealthy.

```
