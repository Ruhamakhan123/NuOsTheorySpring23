# NuOsTheorySpring23
By typing command
sudo apt update && sudo apt upgrade
Download Packages to compile the kernel
sudo apt install build-essential libncurses-dev libssl-dev libelf-dev bison flex -y
And we need and extra package which dwarves
We will install it by typing sudo apt install dwarves (Compiltion occurs when we dont have this
package)
Download the Kernel from kernel.org
wget -P ~/ https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.8.1.tar.xz
Extract the kernel
tar -xvf ~/linux-5.8.1.tar.xz -C ~/
Creation
Change your working directory
cd ~/linux-5.8.1/
Make folder for you system call
mkdir HelloWorld

Create a C file for your system call
nano HelloWorld/HelloWorld.c
WRITE THE FOLLOWING CODE IN IT
#include<linus/kernel.h>
#include<linus/syscall.h>
SYSCALL_DEFINE0(HelloWorld)
{
printk("Hello world.\n");
return 0;
}

Create makefile for your system call
nano HelloWorld/Makefile
Paste this in makefile
obj-y := HelloWorld.o

Edit the MakeFile
nano Makefile
Change the version to your roll number
SEARCH core-y
Replace pervious with this
kernel/ certs/ mm/ fs/ ipc/ security/ crypto/ block/ HelloWorld/

Open header file and add asmlinkage
At the bottom of asmlimkage file before endif
asmlinkage long sys_HelloWorld(void);

Add System call to kernel System call table
440 common HelloWorld sys_HelloWorld

Installation
Sudo make menuconfig
scripts/config --disable SYSTEM_REVOCATION_KEYS
scripts/config --disable SYSTEM_TRUSTED_KEYS
Sudo make
sudo make modules
sudo make modules_install
sudo make install
Then an error occurs which says make bzImage
sudo make bzImage
Then sudo install
sudo update-grub
Restart

Result
uname -r will now show your roll number
nano report.c
Paste the code
#include <linux/kernel.h>
#include <sys/syscall.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <errno.h>
#define __NR_HelloWorld 440

long HelloWorld_syscall(void)
{
return syscall(__NR_HelloWorld);
}
int main(int argc, char *argv[])
{
long activity;
activity = HelloWorld_syscall();
if(activity < 0)
{
perror("system call failed.");
}
else
{
printf("System call worked \n");
}
return 0;
}

Compile and run the program
gcc -o report report.c
./report
Dmesg

![kernel](https://user-images.githubusercontent.com/105592893/221377758-8e667029-962c-4ef6-94da-e9b850e780aa.png)

![k](https://user-images.githubusercontent.com/105592893/221377776-bdf96302-93b8-4985-b06b-8ed6cadae212.png)

![ker](https://user-images.githubusercontent.com/105592893/221377777-76734079-6abf-4578-be21-144a7b812fd8.png)







