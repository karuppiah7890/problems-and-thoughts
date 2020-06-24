# Discovery and Distribution of Software

When you build software, you need to think about how people will discover your software and how they will use it.

It depends on the software really. For example, if you are building a software in your company, you need to have some showcase, where you announce about this new software. This makes other people aware that if they need some feature that your software provides, they can use it instead of building it themselves. This also makes sure that there's not yet another team facing similar issues as you and is trying to fix the problem like you by building something similar. Then it becomes duplicate work, reinventing the wheel etc. This was about discovery, where your users, that is internal teams in the organization, have discovered your software, what it provides or is going to provide. I didn't actually tell about the kind of software though. And this software can be of any kind right? But would it make sense to show every kind of software through some showcase? Some different kinds of softwares I have seen are - web apps (front end), backend services, tools like command line tools, frameworks, libraries, mobile apps, desktop apps, platforms, and there could be more, these are just some that I know of.

Usually there are different platforms to help users discover software. Starting from Googling in Google, Ducking in DuckDuckGo, which are very general and broad, based on the kind of software, usually there are platforms to help you find software. 

For example, GitHub has a search feature to search for different kinds of open source software. But beware, if the search is not working out for you, as in, there exists a repo that can help you, but doesn't show up in your search results, or shows up in very later pages, this could be due to multiple reasons, starting with GitHub having a bad search feature to the repo owner not putting any information like description, readme, docs, or not using the tags feature that GitHub provides for better tagging for understanding the repo for better search and what not.

Similarly, for docker images, docker has a platform called docker hub to search for open source docker images. 

The OS specific package managers that help you to install packages or software also have search features to help you search for software based on name, description. 

There are also language specific package managers and package management systems with central index, which helps you search for packages / libraries / modules. For example, pip website for python packages, npm for JavaScript packages, rubygems for ruby gems, and more. There's even this website that helps you search for packages across languages - libraries.io 

Many softwares also have plugins system, also called extensions and other names. Postgres has extensions, Firefox has add-ons, Chrome has extensions, Kong has plugins, and there are more softwares that have this plugins system. Plugins is also one kind of software

You can use similar platforms, open source or paid, for helping with discovery of software in your company too. But make sure the search is good enough, or it can lead to reinventing the wheel thinking the thing that the user is looking for doesn't exist. Also, everyone needs to follow the practice of putting details about their software in this platform.

Another thing is, if you use source hosting software like GitLab, or GitHub etc which also provide search like we spoke before, that itself can be considered as the discovery platform to search for all kinds of software that your company has ever written.

Next comes the concept of distribution. Software distribution is a pretty big and important concept. I'll be discussing some stuff over here.

One key thing is, the user should be able to trust the software that they get and install on their machine and it should be easy for them to use your software.
All this is part of software distribution.

For example, if you are building mobile apps, you can host your mobile app on the Android Play Store, Apple App Store etc, and these platforms scan the mobile app and also help the user to discover and install the mobile app in a secure manner through cryptography concepts. They will do integrity checks to make sure that the software isn't tampered and distributed as is, and do many other such checks.

For command line tools, developers distribute the SHA sum file or SHA sum for the binary that's being distributed so that the integrity of the binary can be checked to make sure it's not tampered.

For desktop apps, there's package managers that help with distribution and then there's store platforms like Windows App Store, Mac App Store.


