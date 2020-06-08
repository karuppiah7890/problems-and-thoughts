# Meddling with insecure stuff

When someone asks to try out an obscure code or some weird thing in your
phone or laptop or browser, don't do it!

Instead, use an emulator or simulator phone in your computer instead of a real
phone, and instead of a real laptop or computer, use a virtual machine or
container (for example, use docker, podman), and for browser, use a browser
in the virtual machine and don't login to any of the apps when you are using
such virtual things

It's better to use such virtual things instead of the actual phone, computer or
browser, so that you don't risk a security attack. An example is this bash
program below is dangerous

```bash
:() { : | : & }; :
```

It's called a [fork bomb](https://en.wikipedia.org/wiki/Fork_bomb) and can cause
the system to crash by using up a lot of resources. If someone asks you to run
something like this, it could be dangerous, so use Virtual Machines (VMs) or
containers in such cases. Usually VMs are very secure and isolated and hence
any damage, will happen to the VM. Same goes for containers, but VMs seem to be
more secure

A similar example for browsers is - obscure javascript code, that people ask to
run in your browser console to get some feature. This a trap! See a story of
mine here - https://karuppiah7890.github.io/blog/posts/childhood-crazy-tech-stuff/ .
So, be very careful about what you run in your browser console too, and not just
computer console / terminal. I would recommend not to login to the application
site in which you are running some javascript code and to also use a browser
which is running inside a VM.

For phones, there are many malicious things. Like - dangerous wallpapers. See
this video here - https://www.youtube.com/watch?v=iXKvwPjCGnY . Even though
the wallpaper is not intentionally dangerous or malicious, still, it can cause
very crazy damages. So, please beware of what you are always running or doing!
