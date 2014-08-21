---
layout: post
title: Update An Unsupport Ubuntu
category: Tech
tags: [Linux]
comments: true
---
The Ubuntu 12.10 is EOL. And it suggests your to update by using <code>do-release-update</code>. But it would told you <code>404</code>.

First change the sources to the old server:

	sudo cp /etc/apt/sources.list /etc/apt/sources.list.old
	sudo sed -i -e 's/security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
	sudo sed -i -e 's/archive.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list

Second change the dist update info:
	
	sudo cp /etc/update-manager/meta-release /etc/update-manager/meta-release.old
	sudo sed -i -e 's/changelogs.ubuntu.com/blog.wingao.me\/p/g' /etc/update-manager/meta-release

Because offical file is point the url to the <code>archive.ubuntu.com</code> and it will get a <code>404 ERROR</code>. So I just made this file and change all the url to <code>old-release.ubuntu.com</code>.

Finally:
	
	sudo do-release-update

And It DONE!

PS: When you update successful. Use the backup files to replace them.