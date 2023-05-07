---
layout:	post
title:	"A way to locally monitor Docker Container network in real-time with Wireshark"
date:	2022-05-30
---

  Once I wanted to monitor the network traffic of an application. By capturing the network at HOST, there were many packets not relating to what I wanted, it was out of my knowledge to filter them out correctly.

I thought of Docker container, it provides a simple way to isolate the network of a container. It took me a few days to set up everything. Phewww, eventually, it worked.

Check out the sample here:  
<https://github.com/VanDng/LiveCaptureDockerContainerWithWireshark.git>

  