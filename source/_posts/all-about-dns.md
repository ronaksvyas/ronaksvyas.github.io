+++
title = "All About DNS"
description = "We explore some basic concepts about DNS like What exactly is DNS, understand the journey of a request from DNS perspective, see what is DNS Caching and in the end we look at what are different types of DNS Records and how are they useful."
ogimage = "/dns.png"
tags = [
    "internet",
    "dns",
    "tech",
    "technology",
    "networking",
    "computers"
]
date = "2020-07-25"
categories = [
    "Technology",
    "Networking",
]
menu = "main"
+++


We all have been hearing this term "DNS" since the early days of our exposure to the Internet. I remember the first time I heard this term was when I was setting an IPV4 Address for my machine on our Hostel WiFi(yes, I was late!). This post will go through major concepts of DNS which will be useful for making your Networking concepts stronger or just reinforce your understanding about the topic.

# What is DNS?

Domain Name System(DNS) is analogous to the Address book of the internet. Imagine if you had to remember each person in your contact list by their phone number. That is a painful thought right there! Similarly, humans are not expected to remember the IP Address(Internet Protocol Address) of each website they want to visit. I want to type google(dot)com in my browser and it should just take me there. DNS is responsible for translating the domain names to IP Addresses so that whoever(browsers, programs interacting through Http, etc.) is accessing that domain can successfully do so.

All the devices connected to the Internet has a unique IP Address through which they are reachable. This is also the case with your favorite websites. So if you try to access google(dot)com it has to do through its IP Address which DNS will provide.

# What DNS magic happens when I try to access a website?

![](/dns.png "A diagram that depicts the flow of a request for DNS, please excuse my drawing skills :)")
 
 A diagram that depicts the flow of a request for DNS

The above diagram depicts the flow of a request from a DNS Name Resolution perspective, which we will try to decipher with the steps mentioned below. The numbers on the diagram represent a sequence of steps. We're not going into the Networking Stack and Firewalls and everything, we're gonna look at this purely from DNS perspective. [Here's](https://medium.com/@maneesha.wijesinghe1/what-happens-when-you-type-an-url-in-the-browser-and-press-enter-bb0aa2449c1a) a great post on that part if you're interested.

The list of things on a broad level that happens when you try to access say www(dot)google(dot)com are as follows.

1. You type google(dot)com in a browser. It first goes to the DNS Server of your ISP. It returns with IP Address if it has that information. If the ISP DNS doesn't have that address with it, it sends you back a reply with a Root DNS that might have that information.

2. Root DNS has information about which servers would hold information about your top-level domain. Your top-level domain would be .com, .org, .info etc. Root DNS returns the address of Top-level DNS which you will query further in the next step.

3. Now you will contact Top-level DNS querying it with google(dot)com. Top-level DNS would know where google(dot)com is but not where www(dot)google(dot)com is. www is just another subdomain to your main domain. It will return with the address of google(dot)com Second-level DNS which holds information about all subdomains of google(dot)com.

4. You will hit Second-level DNS Server with www(dot)google(dot)com and it will return you. the answer for www(dot)google(dot)com. This is what they call an Authoritative DNS Server. This one holds the DNS Resource records and is the source of truth.

5. Now when you hit the IP address you received, your ISP DNS server will cache the result so next time you hit the same domain, this whole trip won't happen and will save time.

This system is not centralized and it is highly distributed. This whole process is called Name Resolution.

An interesting command which you can use on any Unix based system to find out the IP Address of a domain is nslookup. You can use it like 
```
nslookup google.com.
```

# DNS Caching

Let's look at some pointers on DNS Caching. DNS Caching is useful because servers that are closer to requesting clients can respond to DNS lookup requests faster than the actual Authoritative servers which hold the source-of-truth records. If a record you're looking for is cached somewhere closer to your geographical location, then it can respond to it quickly without additional lookups.

Now, a natural question to ask is what are all the places can DNS lookups can be cached? Can it be cached on my browser itself? Or on another server? Let's try to see what are all the locations where DNS records can be cached. We will go in order of closest to the farthest location where records are cached.

1.  **Browser**   
Yes! Modern web browsers can cache DNS records for a certain amount of time. Browser is one of the closest contact points when you access a domain and caching it in the browser helps. It is the first location that is checked for the requested record. In Chrome, you can go to chrome://net-internals/#dns to see the status of your DNS cache.

2.  **Operating System DNS Cache**  
Operating System caches DNS records. If browser cache doesn't have it, the next and final local stop is OS-level cache.

3. **Internet Service Provider(ISP) level DNS Cache**   
After your machine's OS reverts that it doesn't have the record you requested in its cache, the next stop is the ISP DNS Cache. Once your request reaches this layer, and ISP doesn't have the record, it follows the whole flow we discussed earlier and when it gets the address, it caches it.

One important thing which is to be noted here is that you can override your local DNS entries in /etc/hosts file of your machine. Any mapping entry of domain to IP address added there will override the actual address of that domain.

# Record Types

DNS Servers will create "DNS Records" to provide information on a domain or hostname. Till now, we kind of assumed that a mapping between IP Address and a human-readable domain name is all that is there to DNS Records. We will explore what different kinds of DNS Records are there and how are they different and useful in their way.

1. **A Record**    
A Record, aka Address Record or Address Mapping Record or DNS Host Record, points a domain or a subdomain to an IP(v4) address. This is one of the most important records you will be configuring when you set up a domain.
2. **AAAA Record**   
AAAA record is the same as A record, but exclusively for IPv6 addresses.
3. **CNAME Record**    
A CNAME (Canonical Name) record points one domain or subdomain to another domain name. This is useful because it allows you to update only one A Record every time you make a change in your IP Address. For example, if I have multiple subdomains of my website ronakvyas.com like www.ronakvyas.com or mail.ronakvyas.com or guitar.ronakvyas.com or cycling.ronakvyas.com, it all will point to ronakvyas.com and then the server can resolve where it wants to route the request. You will also hear this one as an alias record. It is mostly used to configure aliases and subdomains.
4. **NS Record**   
Name Server Record gives information about which DNS server is authoritative for that domain. It can have multiple entries for primary and backup name servers for the domain.
5. **MX Record**   
You can configure this for your domain if you want the email for this domain to go to another server directly.

There are other kinds of records like TXT Records, SRV Records, etc. which you can explore. The most important ones which you will need are discussed above.

To summarise, we covered what is DNS, what happens when you make a request, in the sense of DNS, what is DNS Cache, and what are different types of DNS Records. For any queries or suggestions, please reach out to me on LinkedIn or Email.

### References: 

- [https://www.cloudflare.com/learning/dns/what-is-dns/](https://www.cloudflare.com/learning/dns/what-is-dns/)
- [https://ns1.com/resources/dns-types-records-servers-and-queries](https://ns1.com/resources/dns-types-records-servers-and-queries)
- [https://www.pluralsight.com/courses/tcp-ip-networking-for-devs](https://www.pluralsight.com/courses/tcp-ip-networking-for-devs)