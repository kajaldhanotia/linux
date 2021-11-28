<h1>CMPE 283 Assignments</h1>
<h3>By Sumeet Gupta and Kajal Dhanotia</h3>

<h2>Assignment-02-Instrumentation via hypercall</h2>

<h3>Work done by Kajal (015210884):</h3>
We began working on the assignment 02 once our assignment 01 environment was built successfully. We decided to edit the cpuid.c and vmx.c at first and then rebuild the kernel. I edited the cpuid.c and added if..else condition in the kvm_emulate_cpuid block code and commited it to the GitHub repo inside /arch/x86/kvm. After Sumeet commited the changes he made to vmx.c, I rebuilt the kernel and rebooted the VM. I also installed KVM on the hypervisor so that a guest VM can be created and test script can be executed on that.  <br>
  
<h3>Work done by Sumeet (015252003):</h3>
I worked with Kajal for this assignment. On my machine, I edited the vmx.c file according to the edits made in cpuid.c by Kajal. I pushed the changes to GitHub. I then tried to rebuild the kernel. There were some errors encountered while rebuilding the kernel so we decided to start from scratch for assignment 02. After rebuilding the kernel, I also installed gnome on ubuntu host so that we could work with GUI and work on virtual machine manager. I then worked with Kajal to help create the nested VM.  <br>

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
13. Run the command ```cpuid -l 0x4FFFFFFF``` to verify the output.<br>
14. Run the test bash script to produce results and print number of exits.<br>
15. Run the test2 bash script to produce number of cycles in ebx and ecx registers when eax=0x4ffffffe.<br>

<h3>Output Screenshots:</h3>
<ul>
<li>Output screen that verifies that kvm is installed on Ubuntu host.<br>
  
  ![image](https://user-images.githubusercontent.com/89494219/142976711-117f65f3-75ad-407e-9132-e9dd0c094fd6.png)
<br>
  
<li>Output screen that shows nested VM created on KVM Host:<br>
  
  ![image](https://user-images.githubusercontent.com/89494219/142977493-ea58632d-4b90-4836-a7da-311dea1c3184.png)
  
  <br>

  ![image](https://user-images.githubusercontent.com/89494219/142977561-3eb6f60e-07d5-4b62-9270-ba2a0dd50086.png)
  
  <br>
  
  <li>Output screen that shows number of exits when eax=0x4fffffff:<br>

  ![image](https://user-images.githubusercontent.com/89494219/142977843-5bcd7169-33d6-41da-9c53-4a7ae8dca34f.png)

  <br>
    
  <li>Output screen that shows cycles spent when eax=0x4ffffffe:<br>
    
 ![image](https://user-images.githubusercontent.com/89494219/142978056-a00ec5ca-aaa8-44fa-9b59-e6bfc8a793ae.png)


  <br>
    
------------------------------------------------------------------------------------------------------
<h2>Assignment-03</h2>
    
<h3>Work done by Kajal (015210884):</h3>
    
<h3>Work done by Sumeet (015252003):</h3>
    
    
<h3>Steps followed:</h3>
     

<h3>Output Screenshots:</h3>
    <ul>
     
<li> Output of cpuid command in nested VM for specific exit reason when eax=0x4ffffffd.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723386-6ba9b824-1599-46a3-9645-1d6f13554e47.png) <br>

<li> Output for dmesg log showing exit count for exit reason 0.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723417-0f9c4232-3efb-42ce-afcf-3f8028ddeb25.png) <br>

<li> Output for dmesg log showing exit count for exit reason 10.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723431-dd624f12-1838-4fda-9675-6bdaa978d489.png) <br>

<li> Output for dmesg log showing message when exit reason is not defined by SDM.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723464-491c0951-3b61-4ed4-b3a9-649202e48243.png) <br>

<li> Output for dmesg log showing message when exit reason is not enabled in KVM. <br>
  
![image](https://user-images.githubusercontent.com/89494219/143723486-daa51102-06d6-42d9-8809-a4b6fd6b4f20.png) <br>

<li> Output of cpuid command for ebx(high 32-bit) and ecx(low 32-bit) values when eax=0x4ffffffc.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723518-03aa21cc-d68b-4b74-b793-8bd928325c25.png) <br>

<li> dmesg output of cpuid command for ebx(high 32-bit) and ecx(low 32-bit) values when eax=0x4ffffffc.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143724096-e9102625-cd83-408e-8e8a-750fae2d0f36.png) <br>


<li> dmesg output for number of exits for exit reason=0.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723699-2a963076-ecf5-4733-bb82-f95cb5367439.png) <br>

<li> dmesg output for number of exits for exit reason=0 after one reboot.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723687-e46c9dd9-ff34-455c-b36c-30be546baeb9.png) <br>

<li> dmesg output for number of exits for exit reason=0 after one more reboot.<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723714-a90837e9-1420-4908-964a-ba7eed9e6479.png) <br>


<li> dmesg output for most frequent exits, here exit reason = 48<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723931-64e01688-ae94-478f-8877-643dddbd8348.png) <br>


<li> dmesg output for least frequent exits, here exit reason = 29<br>
  
![image](https://user-images.githubusercontent.com/89494219/143723957-e02a195c-607f-4e03-b7d3-f185ff7ad33b.png)
      
    </ul>
