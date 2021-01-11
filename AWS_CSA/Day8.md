# Day 8 topic Covered 
1. 👉 How do AWS Edge locations work internally ?
1. 👉 Why do we use Cloud Front ? Mention some use cases.
1. 👉 Do we have any storage facility in Cloud Front other than cache ?
1. 👉 What is TTL ? Is it tunable ? What is it's default value ?
1. 👉 What is Cloud Front RTMP ? Why is it going to be discontinued by AWS from 2021 ?
1. 👉 What is cache miss and cache hit ?
1. 👉 How can we access Cloud Front cache statistics reports ? What information does it provide ?
1. 👉 What are Geo Restrictions in AWS Cloud Front ? Mention some use cases.
1. 👉 Why we might need to clear cache from all edge locations immediately ?
## Answer
1. Edge locations are like mini AZs where the data is stored as cache.Amazon has its own global infrastructure which is private to itself,which connects all its data centers and edge locations. It solves two problems ie.,latency and security
1. Amazon CloudFront is a middle-ware which stands in between a user requesting for a file from AWS and the S3 data center in a specific region, CloudFront is used to speeds up distribution of your static and dynamic web content from S3 to the User.
use case : If a client is from a far off location from a server then Cloudfront first stores data as cache in nearby edge location of client and then delivers to client. From then on any request from client or clients from same nearby location is located at nearest edge location and delivered.
1. Cloudfront has cache as a service but storage as a service
1. TTL stands for time to live and its time limit of cache files in all Edge locations. Yes, it is tunable. Default value of TTL is 1
1. RTMP is "Real time messaging protocol", used for Audio video streaming by AWS CloudFront. It uses Adobe flash player. Majority of browsers will stop providing compatibility for flash player in 2020 end, after that CloudFront will no longer be supporting RTM
1. If the processor finds that the memory location is in the cache, a cache hit has occurred. However, if the processor does not find the memory location in the cache, a cache miss has occurred. In the case of a cache hit, the processor immediately reads or writes the data in the cache line
" or the first time when a client makes a request to server then there will be a miss called "Cache miss" at edge location as there won't be any data cache stored before
If another request is made by same client or different client belonging to same edge location then it leads to a "Cache hit" as there will be data cache from previous request" 
1. Cache statistics provides all the details about total requests,their hits and misses,their errors,bytes transferred to clients etc.,
It can be found under reports and analytics tab
1. Geo restriction can be defined as restriction of the content for particular area or country so that people of that area could not access it. 
1. When we update something in server data,  we have to immediately remove the caches from the CloudFront because if we don't remove the cache than the user might access the old content of data from the edge locations and  will not get the actual content or data.

Steps for do Clear Cache immediately :

  1. Create Invalidations
  2. put the Object path
  3. select Invalidate.
