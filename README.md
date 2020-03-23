# Final report for STAT 359 Data Science Project

## Summary 

During the course of this class, I worked mainly on the data acquisition and data ingestion portions of the project. At the beginning of the course, I worked on familiarizing myself with Python and using Python to acquire time series data from Alpha Vantage APIs, which can be found [here](https://github.com/rbpeng/stat359_project1). In particular, I wrote wrapper functions to obtain daily equity data, daily currency exchange rate data, and intraday currency exchange rate data, which takes produces csv files of the requested data. 

After working on this data acquisition project, I followed Professor Liu's advice and shifted to projects more aligned with the data ingestion and management portions of the data science pipeline. In particular, I focused on data lake infrastructures, which are centralized repositories that allows you to store all your data (both structured and unstructured) at any scale. In addition to doing research on data lakes, including setup of data lakes, cloud platforms to host data lake structures, organization of data lakes, limitations, and various other aspects, I also deployed a sample data lake infrastructure using AWS. I then explored various features of data lakes using guides from AWS, which allowed me to perform search, transforms, queries, analytics, and visualization of sample data provided by the AWS Data Lake demo. Using these guides, I was able to put together a working data lake through AWS and was able to give a walkthrough of the key features of the data lake infrastructure, using [AWS Lake Formation](https://aws.amazon.com/lake-formation/) to establish a centralized platform to manage and secure the data lake architecture.

The work I did on data acquisition and data lakes fits into the data science infrastructure framework by providing key steps in the data ingestion pipeline. A well-organized data ingestion pipeline is a key component of most data science projects (Recall data ingestion is the process by which data is moved from one or more sources to a destination where it can be stored and prepared for further analysis), since you can't do any data science projects without having data! It is vitally important to have a well-organized infrastructure for moving streaming data and batched data from pre-existing databases and data sources to a repository where you can store and prepare the data for further analysis. More and more commonly for many companies, this repository takes form in a data lake, which are particularly advantageous because they can hold data in its raw form (whatever that form may be), allowing us to accommodate any future schema requirements or design changes. In addition, data lakes are increasingly being deployed on the cloud rather than being hosted on-premises. Thus, it is important that we become familiarized with cloud-based data lake infrastructures, since if we do decide to utilize a data lake structure for our projects, such as PredicT, it will most likely be cloud-based. It is also important to become familiar with the features of a data lake infrastructure, as these features comprise key steps within the data ingestion pipeline. Thankfully, AWS Lake Formation provides a nice centralized platform to manage the data lake and data ingestion process, which is why I spent the last few weeks familiarizing myself with this tool. 

## Instructions & Guides

For the data acquisition through Alpha Vantage APIs, one can follow the [GitHub repository here](https://github.com/rbpeng/stat359_project1) for instructions to use the functions I wrote, as well as the code for the functions. For instance, `get_daily_equity_data(outdir="C:/Users/RBP7855/Desktop", filename="MSFT", stock='MSFT', values='high', num_days=500)` would produce a csv file named `MSFT.csv` in the specified directory, with 500 observations of the highest value of the equity `MSFT` each day. As another example, `get_daily_currency_data(outdir="C:/Users/RBP7855/Desktop", filename="JPY_to_USD", curr1='JPY', curr2='USD', values='low', num_days=1000)` would produce a csv file named `JPY_to_USD.csv` in the specified directory, with 1000 observations of the lowest currency exchange value from Japanese Yen to US Dollar each day. These functions are basically wrapper functions around default [Alpha Vantage functions](https://alpha-vantage.readthedocs.io/en/latest/) (from the Python package `alpha_vantage`). 

Here is an example of the csv file produced by the `get_daily_equity_data` function:

![Example](https://github.com/rbpeng/stat359_final_report/blob/master/MSFT%20example.png?raw=true)

I also did some other work with getting data from APIs with Python, and I used [this guide](https://www.dataquest.io/blog/python-api-tutorial/) for that. 

For my work with deploying a data lake infrastructure and going through the features of the data lake, I mainly used these two following guides from AWS:
[Quick Start Reference Demo](https://aws-quickstart.s3.amazonaws.com/quickstart-datalake-47lining/doc/data-lake-foundation-on-the-aws-cloud-with-aws-services.pdf)
[Demo and Walkthrough](https://aws-quickstart.s3.amazonaws.com/quickstart-demo-47lining-datalake-foundation/doc/data-lake-foundation-on-aws-demo-and-walkthrough.pdf)

The work I did with building a data lake involved less coding, so I will mainly provide screenshots so that you can follow along with what I did. The first guide above is what I used to build a new AWS environment consisting of the virtual private cloud (VPC), subnets, NAT gateways, bastion hosts, security groups, and other infrastructure components, and then deploy the data lake services and components into this new VPC. The Quick Start basically builds a data lake foundation that integrates AWS services such as Amazon S3, Amazon Redshift, Amazon Kinesis, Amazon Athena, AWS Glue, Amazon Elasticsearch Service (Amazon ES), Amazon SageMaker, and Amazon
QuickSight to provide data lake features, such as ingest processing, management, search, transforms, queries, analytics, and visualization. 

After logging into your AWS account and creating a key pair for the region you select (follow [this guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) to create your key pair), you can deploy the Quick Start data lake into a new VPC on AWS using [this link](https://fwd.aws/7D5gP). I kept all the default settings while deploying the Quick Start, but you will need to provide certain required inputs (such as a password for Amazon Redshift and at least two availability regions, as well as a trusted IP address for Remote Access CIDR). Once you provide all of these inputs, click on "Create stack" on the "Review" page, as seen here:
![Deploy Quick Start](https://github.com/rbpeng/stat359_final_report/blob/master/Deploy%20Quick%20Start.PNG?raw=true)

(Note: Deploying the quick start will take up AWS resources and cost money! As mentioned in class, this can be quite expensive)

It should take up to an hour to deploy the Quick Start after clicking on "Create stack," but once the Quick Start is deployed, it will have all the features mentioned earlier, as well as sample data that you can use for the data lake walkthrough that goes through the features of the AWS data lake architecture. You can access the walkthrough using Amazon Redshift using the username and password you provided when deploying the Quick Start. Basically, to access the walkthrough, go to the [AWS CloudFormation console](https://console.aws.amazon.com/cloudformation/), choose the URL for DataLakeWizardURL in the Outputs tab, and open it in a web browser. See the image below to find the data lake wizard URL:
![Access Data Lake Wizard URL](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20CloudFormation%20Data%20Lake%20Foundation%20Outputs.PNG?raw=true)

Following the AWS data lake walkthrough is actually quite simple. Simply follow the [AWS Walkthrough](https://aws-quickstart.s3.amazonaws.com/quickstart-demo-47lining-datalake-foundation/doc/data-lake-foundation-on-aws-demo-and-walkthrough.pdf) and the on-screen prompts to go over the features of the data lake using the sample data provided. 
![AWS Quick Start Walkthrough](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Quick%20Start%20Walkthrough.png?raw=true)

In this walkthrough, you go over the data lake features using a sample data set from ECommCo, a fictional company that sells multiple categories of products through its ecommerce website, and the AWS services you use throughout the walkthrough include Amazon S3 and Amazon Redshift for dataset management and transformation, Amazon Kinesis for streaming submission ingestion, validation and analytics, AWS Glue to perform extract, transform, and load (ETL) jobs and to auto-discover curated datasets with crawlers, Amazon Elasticsearch Service for data governance over data submissions, curated datasets, and published data, Amazon Redshift and Amazon Redshift Spectrum to transform, aggregate and analyze curated datasets directly from S3, Amazon Athena for ad-hoc analyses, data validation and exploration, and Amazon SageMaker for development, training and deployment of machine learning models.

Now, with the data lake infrastructure in place, I then used [AWS Data Lake Formation](https://aws.amazon.com/lake-formation/) to establish a centralized platform to manage and secure the data lake architecture I deployed in the VPC. With this tool, you point Lake Formation at your data sources, and Lake Formation crawls those sources and moves the data into a Amazon S3 data lake. Lake Formation also establishes a centrally defined permissions model through AWS IAM, manages AWS Glue crawlers, AWS Glue ETL jobs, and security settings, and creates and manages a Data Catalog containing metadata about data sources and data in the data lake. I used [this guide](https://docs.aws.amazon.com/lake-formation/latest/dg/getting-started.html) to familiarize myself with the features of AWS Lake Formation. 

Here are the dashboard and sidebar of AWS Lake Formation, which shows the different things you can do with the tool:
![Dashboard](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20Dashboard.PNG?raw=true)
![Sidebar](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20Sidebar.PNG?raw=true)

Basically, the steps needed to create and manage a data lake through Lake Formation involve: 
1. Registering an Amazon S3 path as a data lake.
2. Setting up an Administrator IAM User for the data lake.
3. Creating a database to organize the metadata tables in the Data Catalog.
4. Ingesting data from a data source using crawlers and blueprints.
5. Setting up permissions to allow others to manage data in the Data Catalog and the data lake.
6. Setting up Amazon Athena to query the data that you imported into the data lake.
7. Setting up Amazon Redshift Spectrum to query the data that you imported into the S3 data lake.

Here are screenshots showing how to accomplish each of these steps through Lake Formation:

Step 1:
![Linking a Path as a Data Lake](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20How%20to%20Link%20a%20Database.PNG?raw=true)

![Data Lake Locations](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20Data%20Lake%20Locations.PNG?raw=true)

This is the S3 bucket that the data lake is pointing to:
![S3 bucket](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20S3%20Submissions%20Bucket.PNG?raw=true)

Step 2:
![Administrators](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20Admins%20and%20Database%20Creators.PNG?raw=true)
![Manage Administrators](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20Manage%20Administrators.PNG?raw=true)

Step 3:
![Tables](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20Tables.PNG?raw=true)

Step 4:
(Note: the crawlers are created through AWS Glue, which is incorporated into the data lake framework)
![Crawlers](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Glue%20Crawlers.PNG?raw=true)
![Crawler Description](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Glue%20Crawler%20Details.PNG?raw=true)
![Blueprints](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20Blueprints.PNG?raw=true)

Step 5:
(You can see in the following screenshot that I granted Ana permissions to manage the data lake)
![Permissions](https://github.com/rbpeng/stat359_final_report/blob/master/AWS%20Lake%20Formation%20Permissions.PNG?raw=true)



## Further Insights

Data acquisition and ingestion is one part of the data science pipeline, but it is an extremely pivotal part. Before any analysis is done or any models are created, one needs the data to be stored and managed properly in a manner that allows for analysis and model-building. Nowadays, more and more companies are turning to a data lake infrastructure to handle data ingestion and storage, as data lakes are extremely flexible and allow data of all types to be stored in its raw format. Having an efficient and organized data ingestion pipeline is critical in any data science project, as this is the first step that any data science business must take before any analytics, predictive modeling, or reporting can occur. The need to have a central repository, whether it be a data lake or some other infrastructure, is also very important, as without it, a business is at risk of having different groups performing analytics with incomplete or conflicting data sets, which then has the potential to deliver inconsistent results. When working on a data science project, people tend to think of analytics and results and tend to forget about the data ingestion and management portions, when these portions are just as important in the context of the big picture. Having an efficient, streamlined data ingestion pipeline is a critical component of making sure that the entire data science infrastructure is running smoothly.

Through the course of this project, I used AWS Lake Formation to create this data ingestion pipeline and used sample data provided by the Demo to explore the features of the data lake. Thus, all the data ingestion I've done with this tool has been somewhat artificial and not representative of how a business would actually be expected to perform data ingestion. The natural next step would be to use the Lake Formation tool to ingest real data, using the data lake foundation deployed using [this guide](https://aws-quickstart.s3.amazonaws.com/quickstart-datalake-47lining/doc/data-lake-foundation-on-the-aws-cloud-with-aws-services.pdf) and set up streaming submissions through Kinesis Firehose. For instance, it would be useful to try to incorporate the Alpha Vantage data acquisition functions I wrote to directly ingest stock/exchange rate data into the data lake. In addition, there are other widely-used tools used to set up data lake architectures, such as Azure Data Lake, and it would be useful to become familiarized with those tools to see the advantages and disadvantages compared to building a data lake through AWS. Finally, it would be useful to work with other people to see how the data lake infrastructure fits into the complete data science pipeline. For instance, after setting up a data lake and ingesting data from various sources, it would be useful to see how people doing analytics and model deployment are utilizing the data to gain insight, as data ingestion is of course only one piece of the full data science picture. 
