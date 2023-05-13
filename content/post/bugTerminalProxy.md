---
title: "记录一个关于代理的小坑"
date: 2023-05-13T14:58:50+08:00
draft: false
author: "Liang Li"
---

When I running the `git push` command, I get error:
``` text {linenos=true}
$ git push origin main 
kex_exchange identification: Connection closed by remote host
connection closed by 20.205.243.166 port 22
```

Next, I checked the ssh key I found the following output:
``` text {linenos=true}
$ ssh -T github.com
kex_exchange identification: Connection closed by remote host
connection closed by 20.205.243.166 port 22
```

I tried many solutions including changing the port to 443, turning off the VPN, and regenerating the ssh key, none of which worked.

Finally, I found that I can't successfully run the `curl google.com` command, but can successfully run the `curl baidu.com` command. I guess that my proxy has errors. However, the browser proxy is functioning normally, so I guess there's something wrong with my terminal proxy.

Run the following command:
```
$ curl ipinfo.io
```
Cities are shown in the China. Now the problem is very clear, that is, **the terminal proxy is not turned on**.

If you use VPN, then the problem is most likely that you do not have a terminal proxy enabled.

When I turned on the **terminal proxy**, the problem was successfully solved. 
I use the macOS system. In macOS, the success of the browser proxy does not mean the success of the terminal proxy.
For example, my proxy port is 7890, I run the following command:

    export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890

If you use oh-my-zsh, you can use plugin  zsh-osx-autoproxy to automatically set the terminal proxy.
```
git clone https://github.com/sukkaw/zsh-osx-autoproxy ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-osx-autoproxy

echo "plugins+=(zsh-osx-autoproxy)" | tee -a .zshrc
```
# References
- https://blog.skk.moe/post/macos-auto-read-proxy-settings-zsh/