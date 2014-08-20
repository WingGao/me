---
layout: post
title: Set Multi Subnets on Windows
category: Tech
tags: [Windows, Net]
comments: true
---
Now I have 2 WANs, one is 10M and the other is 20M. I just want to combine them and I would get 10+20=30M.

So you need 2 routers.

    WAN_A -- router_A (192.168.1.1/24)
                |     
               LAN         				--> 	PC
                |      
    WAN_B -- router_B (192.168.2.1/24)

Finally, just set your net work like this:

![windows-config](/assets/p/2014-08-20-subnet.png)

If you config route by your self use:
	
	route add 1.1.1.1 192.168.x.1 if x

More information abuout [route](http://technet.microsoft.com/en-us/library/cc757323(v=ws.10).aspx).