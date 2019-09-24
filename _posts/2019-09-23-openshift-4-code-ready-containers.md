---
layout: post
published: true
title: Openshift 4 Codeready containers Windows 10 pro laptop
---
## Openshift on your Windows 10 pro machine
make sure your machine is multi core and has at last 16gb of ram.
Windows 10 PRO is a requirement.

### Turn on Hypervisor
programs and features ->  enable all Hyper-v options

### Download the windows version of Coderedy Containers and pull secet
*** this requies a free Redhat account   
[Codeready Containers](https://cloud.redhat.com/openshift/install/crc/installer-provisioned?intcmp=7013a000002CtetAAC) 

### set a local path to the location of crc.exe
![set local path](https://user-images.githubusercontent.com/10190444/65509159-d23ead00-de9f-11e9-924e-0387be562ac3.png)

### start Openshift
open a cmd prompt   
```bash
crc setup
crc start
```   

### Go to the Openshift console
[https://console-openshift-console.apps-crc.testing](https://console-openshift-console.apps-crc.testing)   

***see below if you get any errors***   

### fix windows 10 Pro bug if you get an error on crc start
```dial tcp: lookup api.crc.testing```  
This is related to a bug with how Hyper-v on windows handles DHCP for virtual machines   
 

* Open a Powershell cmd prompt with admin priviliges
![image](https://user-images.githubusercontent.com/10190444/65512344-05386f00-dea7-11e9-9e92-6b69f02376d6.png)   

* Get the IP address of your Openshift Hyper-v VM
```get-vm -Name crc | Select -ExpandProperty Networkadapters```

* Open Notepad with admin priviliges
![image](https://user-images.githubusercontent.com/10190444/65511982-60b62d00-dea6-11e9-8770-d569f8c7c30f.png)   

* Open the hosts file in C:\Windows\System32\drivers\etc with DNS entries for Openshift
```bash
# replace you VM ip address with the address below and save the file
172.18.7.77  api.crc.testing
172.18.7.77  oauth-openshift.apps-crc.testing
172.18.7.77  console-openshift-console.apps-crc.testing
```   

* start Codeready containers again
```crc start```

