
![image](https://user-images.githubusercontent.com/59710101/224132816-08a2776b-8bbc-4f14-a70a-001490633139.png)


![image](https://user-images.githubusercontent.com/59710101/224132765-24de6666-d648-473f-91bc-969ea683a3b8.png)


```sh
Cloud CDN, or Content Delivery Network, uses Google's globally distributed edge points of presence to cache HTTP(S) load-balanced content close to your users. Specifically, content can be cached at CDN nodes as shown on this map.
00:16
There are over 90 of these cache sites spread across metropolitan areas in Asia Pacific, Americas, and EMEA. For an up-to-date list, please refer to the Cloud CDN documentation. Now, why should you consider using Cloud CDN?
00:34
Well, Cloud CDN caches content at the edge of Google's network providing faster delivery of content to your users while reducing serving costs. You can enable Cloud CDN with a simple checkbox when setting up the backend service of your
00:51
HTTP(S) load balancer. So it’s easy to enable and benefits you and your users but how does Cloud CDN do all of this? Let’s walk through the Cloud CDN response flow with this diagram.
01:05
In this example, the HTTP(S) load balancer has two types of backends. There are managed VM instance groups in the us-central1 and asia-east1 regions, and there is a Cloud Storage bucket in us-east1.
01:21
A URL map will decide which backend to send the content to: the Cloud Storage bucket could be used to serve static content and the instance groups could handle PHP traffic.
01:32
Now, when a user in San Francisco is the first to access a piece of content, the cache site in San Francisco sees that it can't fulfill the request. This is called a cache miss.
01:45
The cache might attempt to get the content from a nearby cache, for example if a user in Los Angeles has already accessed the content. Otherwise, the request is forwarded to the HTTP(S) load balancer, which in turn forwards
01:59
the request to one of your backends. Depending on what content is being served, the request will be forwarded to the us-central1 instance group or the us-east1 storage bucket. If the content from the backend is cacheable, the cache site in San Francisco can store
02:18
it for future requests. In other words, if another user requests the same content in San Francisco, the cache site might now be able to serve that content. This shortens the round trip time and saves the origin server from having to process the
02:35
request. This is called a cache hit. For more information on what content can be cached, please refer to the documentation. Now, each Cloud CDN request is automatically logged within Google Cloud.
02:50
These logs will indicate a “Cache Hit” or “Cache Miss” status for each HTTP request of the load balancer. You will explore such logs in the next lab. But how do you know how Cloud CDN will cache your content?
03:07
How do you control this? This is where cache modes are useful. Using cache modes, you can control the factors that determine whether or not Cloud CDN caches your content by using cache modes.
03:21
Cloud CDN offers three cache modes, which define how responses are cached, whether or not Cloud CDN respects cache directives sent by the origin, and how cache TTLs are applied.
03:35
The available cache modes are USE_ORIGIN_HEADERS, CACHE_ALL_STATIC and FORCE_CACHE_ALL. USE_ORIGIN_HEADERS mode requires origin responses to set valid cache directives and valid caching headers. CACHE_ALL_STATIC mode automatically caches static content that doesn't have the no-store,
03:57
private, or no-cache directive. Origin responses that set valid caching directives are also cached. FORCE_CACHE_ALL mode unconditionally caches responses, overriding any cache directives set by the origin. You should make sure not to cache private, per-user content (such as dynamic HTML or
04:22
API responses) if using a shared backend with this mode configured.
```
