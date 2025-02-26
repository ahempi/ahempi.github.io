---
title: My Linux Server experience
description: >-
  My Linux experience creating a Linux Server for Minecraft and other
author: ahempi
date:  2025-2-25 19:10:00
categories: [Linux, Server]
tags: [Linux, Server, Minecraft, VPN]
pin: false
media_subpath: '/posts/20180809'
---

# My Starting Experience with Linux

My experience with Linux is relatively small. While I don't know very much about Linux, I do have some foundational knowledge. For example, I know how to flash Linux onto a USB stick, boot it on a computer, and install it. These basic skills were the starting point for my journey into the world of Linux, and they opened up a lot of possibilities for me.

Linux is an open-source operating system that powers millions of devices worldwide, from servers to desktops. It is known for its flexibility, security, and customization options[^1]. Although I am still learning, I have found that the Linux community is incredibly supportive, with countless forums, tutorials, and documentation available online[^2].

---

# How Was My First Run, and How I Accomplished It

I wanted to create my own Minecraft server for me and my friends. Initially, I used **Aternos**, a popular free hosting service for Minecraft servers[^3]. However, Aternos had several limitations that frustrated me:
- It wasn’t 24/7, meaning the server would shut down after periods of inactivity.
- Installing mods was cumbersome and time-consuming.
- There was a strict 2 GB RAM limit, which restricted performance and scalability.

A friend then introduced me to **CasaOS**, a Docker-based local hosting application designed to simplify server management[^4]. While CasaOS seemed promising, I encountered issues getting it to work properly. My father had to step in and help me troubleshoot, but even then, we couldn’t resolve all the problems.

Determined to find a solution, I explored another local hosting program called **YunoHost**[^5], which is essentially a Linux-based operating system tailored for self-hosting applications. Unfortunately, I ran into another roadblock: some critical apps weren’t functioning as expected. This led me to try **Lubuntu**, a lightweight version of Ubuntu[^6]. Unlike full-fledged Ubuntu, Lubuntu is optimized for older or less powerful hardware, making it an excellent choice for beginners like me.

With Lubuntu, I decided to start everything from scratch. After setting it up, I successfully created a functional environment for hosting my Minecraft server. However, I still needed to set up a **VPN** to control my servers remotely. This was the next challenge I faced.

---

# How I Controlled My Servers Remotely

Controlling my Minecraft server remotely required some trial and error. At first, I experimented with **Playit.gg**, a free port-forwarding service[^7]. Unfortunately, this approach didn’t work as intended. My dad and I then tried **Twingate**, a zero-trust remote access platform[^8]. While Twingate offered robust security features, its free plan only supported up to five users—a limitation that didn’t meet my needs.

Undeterred, I continued my search and discovered **Cloudflare Zero Trust**[^9]. This service allowed me to securely expose my server to the internet without exposing my home network directly. The downside? Cloudflare requires a custom domain name, which meant I had to purchase one. I opted for **Ahempi.party**, a budget-friendly domain registrar[^10].

To forward ports for my Minecraft server, my dad and I scoured the internet for solutions. Eventually, we figured out how to configure everything correctly using Cloudflare’s tools. This process taught me a lot about networking and port forwarding. In fact, I plan to write a detailed article about how i setup the minecraft server true cloudflare so other people can access it, because this is not a lot of information about it.

---

# Lessons Learned and Future Goals

This journey has been both challenging and rewarding. Here are some key takeaways:
1. **Patience is essential**: Setting up a server involves troubleshooting and problem-solving, which can be frustrating at times.
2. **Not all resources are equally helpful**: While forums like Reddit’s **r/linuxquestions**[^11] and **Stack Overflow**[^12] are often recommended as go-to places for tech support, I found them unhelpful in my specific situation. Many of the answers I encountered were outdated, overly technical, or simply not applicable to my issues. This taught me to rely more on official documentation and targeted searches instead.
3. **Learning never stops**: Every obstacle I overcame taught me something new about Linux, networking, and server management.

In the future, I hope to expand my knowledge of Linux by exploring advanced topics such as shell scripting, containerization (e.g., Docker), and automation tools like Ansible[^13]. Additionally, I want to experiment with other lightweight distributions like **Xubuntu** or **Linux Mint XFCE**[^14] to see if they offer better performance for my use case.

---

### Footnotes and References
[^1]: [What is Linux? - Linux Foundation](https://www.linuxfoundation.org/about/what-is-linux/)  
[^2]: [Linux Documentation Project](https://tldp.org/)  
[^3]: [Aternos Official Website](https://aternos.org/)  
[^4]: [CasaOS GitHub Repository](https://github.com/IceWhaleTech/CasaOS)  
[^5]: [YunoHost Official Website](https://yunohost.org/)  
[^6]: [Lubuntu Official Website](https://lubuntu.me/)  
[^7]: [Playit.gg Official Website](https://playit.gg/)  
[^8]: [Twingate Official Website](https://www.twingate.com/)  
[^9]: [Cloudflare Zero Trust Documentation](https://www.cloudflare.com/products/zero-trust/)  
[^10]: [Ahempi.party Domain Registrar](https://ahempi.party/)  
[^11]: [r/linuxquestions on Reddit](https://www.reddit.com/r/linuxquestions/) – Note: While this subreddit is popular, it may not always provide actionable solutions for niche problems.  
[^12]: [Stack Overflow](https://stackoverflow.com/) – Note: Stack Overflow is excellent for coding-related queries but less so for specific server or networking issues.  
[^13]: [Ansible Official Website](https://www.ansible.com/)  
[^14]: [Linux Mint XFCE Edition](https://linuxmint.com/download.php)

By sharing my experiences, I hope to inspire others who are just starting their Linux journey. Whether you’re setting up a Minecraft server or diving deeper into system administration, remember that every step forward brings you closer to mastery.