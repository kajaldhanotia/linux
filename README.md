<h1>CMPE 283 Assignments</h1>
<h3>By Sumeet Gupta and Kajal Dhanotia</h3>

<h2>Assignment-02-Instrumentation via hypercall</h2>

<h3>Work done by Kajal (015210884):</h3>
We began working on the assignment 02 once our assignment 01 environment was built successfully. We decided to edit the cpuid.c and vmx.c at first and then rebuild the kernel. I edited the cpuid.c and added if..else condition in the kvm_emulate_cpuid block code and commited it to the GitHub repo inside /arch/x86/kvm. After Sumemet commited the changes he made to vmx.c, I rebuilt the kernel and rebooted the VM. I also installed KVM on the hypervisor so that a guest VM can be created using virt-manager.  <br>
  
<h3>Work done by Sumeet (015252003):</h3>
I worked with Kajal for this assignment. On my machine, I edited the vmx.c file according to the edits made in cpuid.c by Kajal. I pushed the changes to GitHub. I then tried to rebuild the kernel. There were some errors encountered while rebuilding the kernel which I eventually resolved. I also installed gnome on ubuntu host so that we could work with GUI and work on virtual machine manager. I then worked with Kajal to help create the nested VM.  <br>

<h3>Steps followed:</h3>
  
1. Update the files arch/x86/kvm/vmx/vmx.c and arch/x86/kvm/cpuid.c <br>
2. Rebuild the kernel using ```make modules``` command and ```make INSTALL_MOD_STRIP=1 modules_install && make install```.<br>
3. Run ```lsmod | grep kvm``` to check if the kvm modules are preloaded.<br>
4. If they are already present remove them using ```rmmod kvm``` and ```rmmod kvm_intel``` commands.<br>
5. Run ```modprobe kvm``` and ```modprobe kvm_intel``` commands to reload edited kvm modules.<br>
  
6. Optional- We installed GUI for out Ubuntu host for a friendly UI and ease fo work. Also, we wanted to use Virtual machine manager to created the nested VM. GUI can be enabled on Ubuntu VM using below commands:(<a href="https://subscription.packtpub.com/book/big-data-and-business-intelligence/9781788474221/1/ch01lvl1sec15/installing-and-configuring-ubuntu-desktop-for-google-cloud-platform">ref</a>)<br>
  ```$ sudo apt-get install gnome-shell``` <br>
  ```$ sudo apt-get install ubuntu-gnome-desktop``` <br>
  ```$ sudo apt-get install autocutsel``` <br>
  ```$ sudo apt-get install gnome-core``` <br>
  ```$ sudo apt-get install gnome-panel``` <br>
  ```$ sudo apt-get install gnome-themes-standard``` <br> 
  
7. Install xrdp through the below commands- we need this to be able to access Ubuntu in GUI mode.<br>
  ```sudo apt-get update``` <br>
  ```sudo apt-get install -y xrdp``` <br>
  ```sudo apt-get install -y xfce4``` <br>
  ```sudo service xrdp restart``` <br>

8. Login to the host VM using RDP to have graphical interface.<br> 
9. To enable the kvm module in the host and install necessary packages, run the below commands from host terminal: (<a href="https://www.tecmint.com/install-kvm-on-ubuntu/">ref</a>) <br>
  ```sudo apt install qemu qemu-kvm qemu-system qemu-utils```
  ```sudo apt install libvirt-clients libvirt-daemon-system virtinst``` 
10. Run Virtual Machine Manager and create a new VM inside the host. (download the iso file or guest VM as a prerequisite)<br>
11. Install Guest OS once the VM is created and login to the nested VM.<br>
12. Install CPUID using ``` sudo apt install cpuid ``` if it is an Ubuntu VM <br>  
13. Run the command ```cpuid -l 0x4FFFFFFF``` to get the verify output.<br>
14. Run the test.sh script to produce results and print number of exits.<br>
