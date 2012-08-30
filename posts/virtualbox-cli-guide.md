{
    "title": "VirtualBox CLI Management",
    "author": "Austin Yun",
    "date": "2012-07-20"
}

If you're a fan of minimal desktop environments like I am, you may not want to
install all of the dependencies for the VirtualBox GUI -- QT specifically. Not
to fear, there are command line ways of creating, managing, and running VMs.

For the example, I'll be using the [Software Engineering for SaaS class VM][1].
It's part of an online offering of a UC Berkley class that's being done on
[Coursera][2] right now.

Assuming you have VirtualBox installed (pacman -S virtualbox) and have a .vdi
downloaded, just run:
```bash
VBoxManage createvm --name "saas" --ostype Ubuntu --register
VBoxManage modifyvm saas --memory 1024
VBoxManage storagectl saas --add ide --name "IDE Controller"
VBoxManage storageattach saas --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium saasbook-vm-0.8.5.vdi

VBoxSDL -vm saas --fullscreen
```
[1]: http://class.coursera.org/saas-2012-003/class/index 
[2]: http://www.coursera.org/
