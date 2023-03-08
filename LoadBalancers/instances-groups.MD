## instances-groups
![image](https://user-images.githubusercontent.com/59710101/223778088-4f4a59e4-8a1c-4f00-b5e2-be3f17f380ea.png)

![image](https://user-images.githubusercontent.com/59710101/223778185-27d7c5d7-1f5c-43f7-bfcd-6a0fd3d8f6b1.png)

![image](https://user-images.githubusercontent.com/59710101/223778418-fed280f5-1f66-4a1e-a000-25d303328efd.png)

```sh
Person: A managed instance group is a collection of identical VM instances that you control as a single entity using an instance template. You can easily update all the instances in a group
00:11
by specifying a new template in a rolling update. Also when your applications require additional compute resources, managed instance groups can scale automatically to the number of instances in the group.
00:24
Managed instance groups can work with load balancing services to distributor network traffic to all of the instances in the group. If an instance in the group stops, crashes or is deleted by an action other than the instance group commands,
00:38
the managed instance group automatically recreates the instance so it can resume its processing tasks. The recreated instance uses the same name and the same instance template as the previous instance.
00:51
Managed instance groups can automatically identify and recreate unhealthy instances in a group to ensure that all instances are running optimally. Regional managed instance groups are generally recommended over zonal managed instance groups
01:07
because they allow you to spread the application load across multiple zones instead of confining your application to a single zone or having you manage multiple instance groups across different zones.
01:19
This replication protects against zonal failures and unforeseen scenarios where an entire group of instances in a single zone malfunctions. If that happens, your application can continue serving traffic from instances running in another zone in the same region.
01:36
In order to create a managed instance group, you first need to create a instance template. Next, you're going to create a managed instance group of N specified instances. The instance group manager then automatically populates the instance
01:51
group based on the instance template. You can easily create instance templates using the cloud console. The instance template dialogue looks and works exactly like creating an instance, except that the choices are recorded so they can be repeated.
02:08
When you create an instance group, you define the specific rules for that instance group. First, you decide what type of managed instance group you want to create. You can use managed instance groups
02:21
for stateless serving or batch workloads. such as website front end or image processing from a queue, or for stateful applications. such as databases or legacy applications. Second, provide a name for the instance group.
02:35
Third, decide whether the instance group is going to be single or multizoned and where those locations will be. You can optionally provide port name mapping details. Fourth, select the instance template that you want to use.
02:49
Fifth, decide whether you want to autoscale and under what circumstances. Finally, consider creating a health check to determine which instances are healthy and should receive traffic. Essentially, you're creating virtual machines,
03:05
but you're applying more rules to that instance group.

```
