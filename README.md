![image](https://user-images.githubusercontent.com/109401839/216487677-14f36f8b-0aba-4ae5-80bb-24cc92f9a75f.png)


<h1>Building a Data Pipeline in Windows 10</h1>

What is StreamSets Data Collector is a lightweight engine used to stream data in real time. 
It can be used to route and process data in your data streams.

The purpose of this document is to show a general step by step process of how to setup StreamSets Data Collector and utilise it in Linux via Windows 10 without dual booting or VM software. 

<h2>Environments and Technologies Used</h2>

- Windows Subsystem Linux Installation
- StreamSets DataOps Platform | Control Hub
- StreamSets Data Collector 3.22.3
- Visual Studios Code & Plugins 
- Windows Terminal Preview

<h2>Operating Systems Used </h2>

- Ubuntu Linux 22.04.1 LTS 

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

<b>Set Up</b>

![OptionalFeatures_JvZFIbf6Tk](https://user-images.githubusercontent.com/109401839/216782290-a1584427-94d0-491a-9bfb-7a1a49785e66.png)

First I enabled Windows 10 Subsystem Linux (WSL), then [install](https://visualstudio.microsoft.com) Visual Studio Code programme if not installed already. 

Visual Studio Plugin, "[WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)" by Microsoft

Next the operating system of choice, [Ubuntu 22.04.1 LTS](https://apps.microsoft.com/store/detail/ubuntu-22041-lts/9PN20MSR04DW?hl=en-gb&gl=gb)
The reason I went with Ubuntu over Oracle or Redhat is due to compadibility issues in Visual Studios. 


Download the [Data Collector](https://accounts.streamsets.com/install/select/data-collector) for "Linux Server - For Porduction Use" , then selected the Download Type to be "Tarball(Recommended)" 

![vivaldi_TRru1imRLL](https://user-images.githubusercontent.com/109401839/216780044-7bb372ab-25cc-44ec-b36a-86d49631faf5.png)

These are the instructions for Tarball:

![vivaldi_93pnGrQIWy](https://user-images.githubusercontent.com/109401839/216780174-79bf2504-b6aa-46c1-91f7-0ae5ae7b1a2a.png)

<b>Connect to Ubuntu<b>

![remote-wsl-open-code](https://user-images.githubusercontent.com/109401839/216782789-144af2ff-1341-41f8-837e-dc7ea1790f91.gif)

![image](https://user-images.githubusercontent.com/109401839/216782795-79a94846-5a8f-4dfa-bf2b-e8ed51cc2aa3.png)

<b>Open Folder<b>

![image](https://user-images.githubusercontent.com/109401839/216782811-608838fb-ac12-45fe-a20e-c0f6181645db.png)

![Code_Xh2hyl3jlq](https://user-images.githubusercontent.com/109401839/216782834-3a45d747-390b-41e6-8284-06407ffd9294.png)

Now we are in Ubuntu via Windows.. 

![Code_ETLoaBueQt](https://user-images.githubusercontent.com/109401839/216782939-be7abb9f-8f32-45c6-8a05-de9cc033c988.png)




