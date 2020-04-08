---
layout: article
title: How to connect to UC Davis Library VPN on Ubuntu
tags: software programming
aside:
    toc: true
  
---
You might be wondering why all this is necessary to do. Lots of services and features such as the New York Times and Textbooks are available to UC Davis students only if they have physical access to the Campus wifi. UC Davis Virtual private network service or VPN, serviced by the Information and Educational Technology department, mitigate this problem to allow you to send and recieve data as if you were there. This is especially critical during times like now with the Covid-19 pandemic and probably future Fall quarter cancelling's because of Northern California's tendency to catch on fire a lot.


## Installing Pulse Secure VPN

For this tutorial I will walk you through the steps I took to personally to install Pulse Secure VPN on Ubuntu and connect to the UC Davis Library VPN. 

Since I am using Ubuntu 18.04.4 LTS, I installed the 64-bit DEB package directly from [UC Davis Website](https://www.library.ucdavis.edu/wp-content/uploads/vpn-clients/pulse-9.1R4.x86_64.deb). The other options are located [here](https://www.library.ucdavis.edu/service/connect-from-off-campus/vpn-questions-known-issues/)


Since Ubuntu is a derivative of the Debian Linux distribution (a special type of operating system with it's own unique and FREE software), we will use the package management system ```dpkg``` with the ```-i``` install flag to unpackage the newly downloaded file that is in a software package format called debian. We however use the ```sudo``` program "superuser do" to gain security priviledges to perform this step.

```console
alejandro@Alejandro-Desktop:~/Downloads$ sudo dpkg -i pulse-9.1R4.x86_64.deb 
```

Now we will install the required dependency packages for the Graphical User Interface so that the program is easy and convenient to use. 

```console
alejandro@Alejandro-Desktop:~/Downloads$ /usr/local/pulse/PulseClient_x86_64.sh install_dependency_packages

```
At this point you can just skip to the **Using the VPN Command User Interface** section if that is what you prefer. With that said, whenever we wish to launch the UI, simply executing the below command: 

```console
alejandro@Alejandro-Desktop:~/Downloads$ /usr/local/pulse/pulseUi
```
You will now click the plus sign to add a new connection. I selected the server to connect to as ```vpn.library.ucdavis.edu```. You should do the same. Afterwards I was prompted to sign in with my Kerebos credentials and everything was good to go. 

## Using the VPN Graphical User Interface

Most users will probably prefer this approach, which is why I'm putting it first. Go to the [Library Site](https://www.library.ucdavis.edu/) and search for whichever article you are interested in. 

For instance I will search for a published article of the esteemed Professor Ding. I simply searched for Zhi Ding and filtered my results with "Engineering, Conference Proceedings, Articles". I was quickly able to access this article published through Institute of Electrical and Electronics Engineers (IEEE) Transactions on Wireless Communications.
<p>
    <img src="/assets/images/connectVPN/working.png" alt="Cover photo"/>
    <br>
    <em>Successful access!
    </em>
</p>

You will however notice you run into this particular problem when you do not connect with the VPN. This is because UC Davis encrypted network is neccesary to establish a connection with third party site LibKey to give access to the IEEE Publisher. 

<p>
    <img src="/assets/images/connectVPN/3rdpartyfail.png" alt="Cover photo"/>
    <br>
    <em>Oh no!
    </em>
</p>

## Using the VPN Command User Interface


The command line client can be launched using the command below for 64 bit client:

```console
alejandro@Alejandro-Desktop:~$ /usr/local/pulse/PulseClient_x86_64.sh -h vpn.library.ucdavis.edu -u <your kerberos id> -r Library
```

In general, you would use the following to connect to any other VPN provider.

```console
 alejandro@Alejandro-Desktop:~$ /usr/local/pulse/PulseClient_x86_64.sh -h <PCS appliance IP/hostname> -u <vpn username> -p <vpn password> -U <PCS SIGNINURL>  -r <realm>

 ```

Remember the Library VPN is intended for access to electronic resources only and Service ports on the Library VPN have been restricted to web browsing and email only. Other Internet applications, such as FTP or SSH, to external services will not function until the Library VPN is disconnected. So to disconnect, use this command.

 ```console
alejandro@Alejandro-Desktop:~$ /usr/local/pulse/PulseClient_x86_64.sh -K
 ```
Thanks for getting to the end, I hope you found this article useful and that you enjoy putting your newfound knowledge to good use! Remember, I wrote this for UC Davis students, but if you follow these steps you can and will be able to access material at other instititions. For example MIT also uses Kerebos, so the process is nearly identical. 