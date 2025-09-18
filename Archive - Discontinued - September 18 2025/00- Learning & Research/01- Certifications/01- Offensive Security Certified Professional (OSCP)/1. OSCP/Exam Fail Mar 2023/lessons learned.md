---
#lessons learned
- need to work on linux & windows initial access alot more.
- ssh port forwarding more, refer to .110.
- sql injection.
- never got into the AD machines but probably more AD practice.
- identify web back end to exploit.

	- For narrowing down exploits. You wanna try and identify what is running on a box/website. So for your shoppr thing... the software wasnt actually called shoppr. For example like.... if i wanted to start a webstore and I made RyansHotFuckinDildos.com but I used shopify.com as my software/platform... You'd be wanting to identify that I'm running shopify. Or wordpress, or joomla, or whatever. Because you'd be lookin for some exploit against a shopify/wordpress/joomla version or maybe a plugin for that software.

	- So for a website my go to is literally just right click view source or ctrl + U. Then look around for something that looks like a software name. For example in the screenshot of this website I pulled up and viewed source on, I found it's running wordpress. not sure what version exactly (but sometimes it will actually be in the source). However, I also see its running a plugin Yoast SEO plugin 4.8 as well. So I would searchsploit yoast as well as google "Yoast seo plugin 4.8 CVE" and "yoast seo plugin 4.8 exploit poc github".

- do proving grounds boxes
- sql, 
```