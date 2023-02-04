![image](https://user-images.githubusercontent.com/109401839/216487677-14f36f8b-0aba-4ae5-80bb-24cc92f9a75f.png)


<h1>Building a Data Pipeline in Windows 10</h1>

What is StreamSets Data Collector is a lightweight engine used to stream data in real time. 
It can be used to route and process data in your data streams.

The purpose of this document is to show a general step by step process of how to setup StreamSets Data Collector and utilise it in Linux via Windows 10 without dual booting or VM software. 

<h2>Environments and Technologies Used</h2>

- StreamSets Data Collector 3.22.3
- VM Workstation

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

First I downloaded the ISO file of [Ubuntu 22.04.1 LTS](https://apps.microsoft.com/store/detail/ubuntu-22041-lts/9PN20MSR04DW?hl=en-gb&gl=gb)

In Linux, Download the [Data Collector](https://accounts.streamsets.com/install/select/data-collector) for "Linux Server - For Porduction Use" , then selected the Download Type to be "Tarball(Recommended)" 

![vivaldi_TRru1imRLL](https://user-images.githubusercontent.com/109401839/216780044-7bb372ab-25cc-44ec-b36a-86d49631faf5.png)

These are the instructions for Tarball:

![vivaldi_93pnGrQIWy](https://user-images.githubusercontent.com/109401839/216780174-79bf2504-b6aa-46c1-91f7-0ae5ae7b1a2a.png)
