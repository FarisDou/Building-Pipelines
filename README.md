![image](https://user-images.githubusercontent.com/109401839/216487677-14f36f8b-0aba-4ae5-80bb-24cc92f9a75f.png)


<h1>Building a Data Pipeline in Windows 10</h1>

What is StreamSets Data Collector is a lightweight engine used to stream data in real time. 
It can be used to route and process data in your data streams.

The purpose of this document is to show a general step by step process of how to setup StreamSets Data Collector and utilise it in Linux via Windows 10 without dual booting. Originally, I planned to use Windows Subsetting Linux (WSL) through Visual Studios Code (VSC). This attempt worked but was time consuming to set up for notation. Perhaps, I will create a seperate repository demonstrating WSL through VSC. 

<h2>Environments and Technologies Used</h2>

- [StreamSets Data Collector 3.22.3](https://accounts.streamsets.com/install/select/data-collector)
- [VM Workstation](https://www.vmware.com/products/workstation-pro.html)

<h2>Operating Systems Used</h2>

- [Ubuntu Linux 22.04.1 LTS](https://apps.microsoft.com/store/detail/ubuntu-22041-lts/9PN20MSR04DW?hl=en-gb&gl=gb) 

<h2>Phases</h2>

- Set Up
>Environments>Deployments>Engines>Connections
- Build
>Fragments> Pipelines> Sample Pipelines
- Run
>Job Templates> Job Instances> Scheduled Tasks> Draft Runs
- Monitor
>Operations Dashboard> Topologies Dashboard> Subscriptions> Topologies> Reports> Alerts
-Manage
> My Organisation> Users> Groups> Audis> API Credentials

<h3>Set Up</h3>

First I downloaded the ISO file of Ubuntu 22.04.1 LTS and installed it into VM Workstation. 

![vmware_3ngMFZ7NOs](https://user-images.githubusercontent.com/109401839/216786096-2e9d6cc6-6dda-4999-a569-fe61e849730f.png)


In Linux, Download the [Data Collector](https://accounts.streamsets.com/install/select/data-collector) for "Linux Server - For Porduction Use" , then selected the Download Type to be "Tarball(Recommended)" 

![vivaldi_TRru1imRLL](https://user-images.githubusercontent.com/109401839/216780044-7bb372ab-25cc-44ec-b36a-86d49631faf5.png)

These are the instructions for Tarball:

![vivaldi_93pnGrQIWy](https://user-images.githubusercontent.com/109401839/216780174-79bf2504-b6aa-46c1-91f7-0ae5ae7b1a2a.png)


In Linux Terminal I first installed the OpenJDK 8 / Java 8 JDK, either or by using the commands; 

```
sudo apt-get update && sudo apt-get install openjdk-8-jdk
```

Enter your password and install. 

```
wget https://archives.streamsets.com/datacollector/3.22.3/tarball/activation/streamsets-datacollector-common-3.22.3.tgz
```

![vmware_KyOKSSfkTq](https://user-images.githubusercontent.com/109401839/216790885-1dc88284-2dd1-4c07-a727-74c9c763fce3.png)


Use ``` ulimit -n```
It should respond with 1024 as default, we need atleast 32768 to run Data Collectors. 

``` ulimit -n 32768``` will increase the descriptor limit.

Then use ```ulimit -n``` to verify the change. 

Afterwards, ```bin/streamsets dc``` is used to allow us to access the localhost interface of data collector. 

![vmware_nefeOlVQU9](https://user-images.githubusercontent.com/109401839/216791163-47d59477-053a-4e9d-ac95-664eec406c4c.png)

> Running on URI : 'http://fnabeel-virtual-machine:18630' , enter the url into your browser and you should be welcomed with; 

![vmware_pqzGMdAWzf](https://user-images.githubusercontent.com/109401839/216791224-8a7e1349-fec7-4b5e-878a-7ac1e2c68450.png)

<h3>Configuration</h3>

<b>Now the setup Phase is over and Data collectors is deployed, its time to create a pipeline, configure it and run a sample dataset.<b>



