![image](https://user-images.githubusercontent.com/109401839/216487677-14f36f8b-0aba-4ae5-80bb-24cc92f9a75f.png)


[Video Implementation](https://www.youtube.com/watch?v=kqVJjWjjOyc&ab_channel=FarisNabeel)


<h1>Building a Data Pipeline in Windows 10</h1>

What is StreamSets Data Collector is a lightweight engine used to stream data in real time. 
It can be used to route and process data in your data streams.

The purpose of this document is to show a general step by step process of how to setup StreamSets Data Collector and utilise it in Linux via Windows 10 without dual booting. Originally, I planned to use Windows Subsetting Linux (WSL) through Visual Studios Code (VSC). This attempt worked but was time consuming to set up for notation. Perhaps, I will create a seperate repository demonstrating WSL through VSC. 

<h2>Environments and Technologies Used</h2>

- [StreamSets Data Collector 3.22.3](https://accounts.streamsets.com/install/select/data-collector)
- [VM Workstation](https://www.vmware.com/products/workstation-pro.html)

<h2>Dataset</h2>

- [NYC Taxi Data](https://docs.streamsets.com/datacollector/sample_data/tutorial/nyc_taxi_data.csv)

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

<h3>Set Up Phase I</h3>

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




Use ``` ulimit -n```
It should respond with 1024 as default, we need atleast 32768 to run Data Collectors. The ulimit increases the amount of files the user can create which is needed for data collector. 

``` ulimit -n 32768``` will increase the descriptor limit.

Then use ```ulimit -n``` to verify the change. 

Next, ```cd streamsets-datacollector-3.22.3```

Afterwards, ```bin/streamsets dc``` is used to allow us to access the localhost interface of data collector. 



> Running on URI : 'http://"user"-virtual-machine:18630' , enter the url into your browser and you should be welcomed with; 



<h3>Configuration and Running Pipeline, Phase II</h3>

<b>Now the setup Phase is over and Data collectors is deployed, its time to create a pipeline, configure it and run a sample dataset.<b>

![vmware_0NyxDaoVLR](https://user-images.githubusercontent.com/109401839/216791622-4772eda6-c656-43d3-8a34-496647a75183.png)

I lay a basic template first or later can be done.
> 0.Directory > 0.Stream Selector > 1. Jython Evaluator > 1.Field Masker > 1.Hadoop FS
> 2. Expression Evaluator (Connect to Hadoop FS) > 2.Field Type Converter > 2.Expression Evaluator > 2.Trash

 Place Directory 1 on the plane first and enter it's config. 

![Inkedvmware_0Mw3nKfJLZ](https://user-images.githubusercontent.com/109401839/216791724-3edb0fcb-3a42-407e-9376-df18824a3c7d.jpg)

![vmware_vr8ciH2dLf](https://user-images.githubusercontent.com/109401839/216794271-0a554548-3606-491b-964b-6392beda1a4a.png)

Next Stream Selector Configurations, Conditions Tab

Add the conditions ```${record:value('/payment_type') == 'CRD'}```

Be sure to havbe pathway 1 go to the jython, and pathway 2 to the other way.

It should look something like this:



Next Install Jython in the Package Manager section. 



Go back home and enter the pipeline. 

Under the Jython Evaluator Config, enter the script:

```
try: 
  for record in records:
    cc = record.value['credit_card']
    if cc == '':
      error.write(record, "Payment type was CRD, but credit card was null")
      continue

    cc_type = ''
    if cc.startswith('4'):
      cc_type = 'Visa'
    elif cc.startswith(('51','52','53','54','55')):
      cc_type = 'MasterCard'
    elif cc.startswith(('34','37')):
      cc_type = 'AMEX'
    elif cc.startswith(('300','301','302','303','304','305','36','38')):
      cc_type = 'Diners Club'
    elif cc.startswith(('6011','65')):
      cc_type = 'Discover'
    elif cc.startswith(('2131','1800','35')):
      cc_type = 'JCB'
    else:
      cc_type = 'Other'

    record.value['credit_card_type'] = cc_type

    output.write(record)
except Exception as e:
  error.write(record, e.message)
```

<b>Expression Evaluator (1)<b>
Expression Tab: Field Output | ```/credit_card_type``` | ```n/a```

 
<b> Write to Destination | Local FS<b>

Output Files Tab:

![vivaldi_FHJIDE910g](https://user-images.githubusercontent.com/109401839/216795711-36764a03-9513-4f61-aa65-ad55f36d0169.png)

Data Format Tab:

![vivaldi_O0E1aQfxzp](https://user-images.githubusercontent.com/109401839/216795728-2a28397a-d6dd-4932-a061-2708c356678c.png)

That completes the main branch of the pipeline.

<b>Mask Credit Card Numbers Through Field Masker<b>

For the credit card numbers, we'll use the following regular expression to mask all but the last four digits: ```(.*)([0-9]{4})```

Field Masker Configuration, Mask Tab

Fields to Mask: ```/credit_card.```

Mask Type: ```Regular Expression```

Regular Expression: ```(.*)([0-9]{4})```

Groups to Show: ```2```

It should look like this:



<b>Next Convert Types with a Field Type Converter<b>

Under Field Type Converter Configuration Conversions Tab:
Modify the "Fields to Convert" to ```/dropoff_datetime``` and ```/pickup_datetime```
Modify "Convert to Type" to  ```DATETIME```
Modify "Date Format" to ``` yyyy-MM-dd HH:mm:ss```


Add a new section by hitting the plus and fill the Fields to Convert with:
```
/fare_amount
/dropoff_latitude
/dropoff_longitude
/mta_tax
/pickup_latitude
/pickup_longitude
/surcharge
/tip_amount
/tolls_amount
/total_amount
```

The Convert to Type to ```Double```
In the end, the Field Type Converter should look something like this. 



<h3>Data Maniuplation<h3>

Under Expression Evaluator (2) Configuration , Expressions Tab

The Field Expressions Output field:

```/pickup_location``` | ```	${record:value('/pickup_latitude')}, ${record:value('/pickup_longitude')}```

Add Field Expressions:

```/dropoff_location``` | ```	${record:value('/dropoff_latitude')}, ${record:value('/dropoff_longitude')}```

Add Field Expressions:

```/trip_revenue``` | ```${record:value('/total_amount') - record:value('/tip_amount')}```
>This expression subtracts the tip from the total fare.


 <b>Running the Pipeline(Sucessful)</b> 15 minutes.

 ![EntyCHChHT](https://user-images.githubusercontent.com/109401839/217294875-cad46a55-c57b-467a-b081-b6fb67a0e361.png)


>Note to self, check directories and ensure everystep is taken or somethings that seem minor will cause the entirety of the pipeline to fail.
>I found it strange that in some pipelines there was no output and a few errors and others there was no errors, no output. This final screenshot seems like a success, because the pipeline is doing its job. An automated process that moves data from one place to another, transforming and processing it along the way. The final screenshot to me shows theres a process happening. 

> If running a previous pipeline or stopped a current one, to reinitiate it proper, use the "reset origin & start option".
