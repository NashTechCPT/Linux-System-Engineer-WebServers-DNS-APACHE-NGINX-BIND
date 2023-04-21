# LocalNetworkCONFIG-KALI-Linux
Home Lab Setup 

Step 1: Install Virtualbox 

Step 2: Install Kali Linux Installer Image - https://cdimage.kali.org/kali-2023.1/kali-linux-2023.1-installer-amd64.iso

Step 3: Open Virtualbox and Install the downloaded Image

Step 4: Click on the Kali Linux VM instance after installation and configure the network settings by clicking on "Settings" > "Network" > Adapter1 > and change "Attached to:" from "NAT" to "Bridged Adapter" and the "Name:" section select the network adapter your Host Computer is using to access the internet. Click "OK".

(Make sure VM is Powered Off)

Step 5: In the Virtualbox Menu, go to the "Machine" menu and select "Clone", a dialog box asking for the VM name should appear. Make sure to check "reinitialize the Mac address of all network cards", select "Linked Clone" (uses less disk space)

Step 6: Clone another VM from the first VM installation. (3 VM's in total) exact same configuration where only the names differ. eq. VM1 and VM2. 

Step 7: Start VM 1, make sure your network adapter has an assigned IP address by either using the Terminal or the UI "ifconfig" or "network adapter icon"

Step 8: Open a Terminal and type the following commands: 

 # sudo hostnamectl set-hostname <yournewhostname.localnet.com>
 # sudo apt install acpid
 # sudo systemctl enable acpid
 # sudo systemctl start acpid
 
 Step 9: Start up VM2, check for IP address and follow the same process as above, each instance having a unique hostname
        
        Open a Terminal and type the following commands: 

 # sudo hostnamectl set-hostname <yournewhostname.localnet.com>
 # sudo apt install acpid
 # sudo systemctl enable acpid
 # sudo systemctl start acpid
 # sudo vi /etc/hosts

    in the vi text editor go to the end of the file, start a new line and enter the IP address, Domain name and Hostname of VM1 and VM2:
    192.168.1.88 yournewhostname.localnet.com yournewhostname
    192.168.1.89 yournewhostname2.localnet.com yournewhostname2
    
    Save the file

Step 10: ping vm1

If ping is successful, then you can continue, if not do not proceed or no further configuration can be completed. 

Step 11: Copy the /etc/hosts file from VM2 to VM1 in order to have local name resolution on both machines by executing the following commands in the Terminal:

 # sudo scp /etc/hosts yournewhostname:/etc/hosts
  If promted to continue for authentication, type "yes" without quotes. 

  If a permission denied error is received, open a Terminal on VM1 and execute the following command: 
  
 # systemctl status ssh.socket
 # if status disabled then 
 # systemctl enable ssh.socket
 # AND
 # systemctl start ssh.socket
 # sudo chmod 777 /etc/hosts (this will allow read, write and execute to the file on vm1)
    If a permission denied error is still received, execute the following commands: 
 # sudo vi /etc/ssh/ssh_config
  add the following lines to the file excluding the #: 
# PermitRootLogin yes
# AllowUsers yourhostname2

Save the file and try the scp command from vm2 again, if promted for the password, enter the password of vm1. 

Save a snapshot of VM1 and VM2 in order to maintain the network configuration. 




    


