# NuOsTheorySpring23
Adding a Hello World System Call

Preparations

1. Update Your System:
By adding the following commands update/upgrade your system first.

sudo apt-get update
sudo apt-get upgrade

2. Download Packages To Compile The Kernel:
sudo apt install build-essential libncurses-dev libssl-dev libelf-dev bison flex-y And we need and extra package which dwarves We will install it by typing sudo apt install dwarves (Compiltion occurs when we dont have this package).

3. Download The Kernel:
Download the kernel from kernel.org. wget -P ~/ https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.8.1.tar.xz

4. Extract The Kernel:
tar -xvf ~/linux-5.8.1.tar.xz -C ~/

Creation

1. Change Your Working Directory:
cd ~/linux-5.8.1/

2. Make a Folder For Your System Call:
mkdir HelloWorld

3. Create a C File For Your System Call:
nano HelloWorld/HelloWorld.c

Write the following code in it:

#include <linux/kernel.h> asmlinkage long sys_hello(void) { printk("Hello world\n"); return 0; }

4. Create a File For Your System Call;
nano HelloWorld/Makefile Paste this in makefile obj-y := HelloWorld.o

5. Edit The MakeFile:
Change the version to your roll number SEARCH core-y Replace pervious with this kernel/ certs/ mm/ fs/ ipc/ security/ crypto/ block/ HelloWorld/

6. Open Header File and add asmlinkage :
At the bottom of asmlimkage file before endif asmlinkage long sys_HelloWorld(void)

7. Adding the prototype of the new system call into the system calls header file:
Now we have to add the prototype of our system call in the system’s header file which is located in the kernel folder then “/include/linux/syscalls.h”. We have to add the prototype of our system call function in this file.

Installation:

Run the following commands for the installation

Sudo make menuconfig
scripts/config --disable SYSTEM_REVOCATION_KEYS
scripts/config --disable SYSTEM_TRUSTED_KEYS
Sudo make
sudo make modules
sudo make modules_install
sudo make install Then if an error occurs which says make bzImage
sudo make bzImage
Then sudo install
sudo update-grub
Restart

Results:

nano userspace.c
Paste the code
#include <linux/kernel.h> #include <sys/syscall.h> #include <stdio.h> #include <unistd.h> #include <string.h> #include <errno.h> #define __NR_HelloWorld 440 long HelloWorld_syscall(void) { return syscall(__NR_HelloWorld); } int main(int argc, char *argv[]) { long activity; activity = HelloWorld_syscall(); if(activity < 0) { perror("system call failed."); } else { printf("System call worked \n"); } return 0; }

RollNo "21k-3097" being displayed using uname -r command:

![kernel](https://user-images.githubusercontent.com/105592893/221377758-8e667029-962c-4ef6-94da-e9b850e780aa.png)

![k](https://user-images.githubusercontent.com/105592893/221377776-bdf96302-93b8-4985-b06b-8ed6cadae212.png)

<img width="365" alt="221380329-c6d92756-a267-4c19-8704-2adcf30ea762" src="https://user-images.githubusercontent.com/105592893/224255238-fbf71ef6-304c-4854-967f-447e834bfb46.png">








