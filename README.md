## DATA622 HW #3
- Assigned on September 27, 2017
- Due on October 11, 2017 11:59 PM EST
- 15 points possible, worth 15% of your final grade

### Instructions:
1. Get set up with free academic credits on both Google Cloud Platform (GCP) and Amazon Web Services (AWS).  Instructions has been sent in 2 separate emails to your CUNY inbox.

2. Research the products that AWS and GCP offer for storage, computing and analytics.  A few good starting points are:
    - [GCP product list](https://cloud.google.com/products/)
    - [AWS product list](https://aws.amazon.com/products)
    - [GCP quick-start tutorials](https://codelabs.developers.google.com/)
    - [AWS quick-start tutorials](https://aws.amazon.com/getting-started/tutorials/)
    - [Mapping GCP to AWS products Azure](https://stackify.com/microsoft-azure-vs-amazon-web-services-vs-google-compute-comparison/)
    - [Evaluating GCP against AWS](http://blog.armory.io/choosing-between-aws-gcp-and-azure/)


3. Design 2 different ways of migrating homework 2's outputs to *GCP*.  Evaluate the strength and weakness of each method using the Agile Data Science framework.

4. Design 2 different ways of migrating homework 2's outputs to *AWS*.  Evaluate the strength and weakness of each method using the Agile Data Science framework.

### Critical Thinking (8 points total)

- Fill out the critical thinking section by modifying this README.md file.
- If you want to illustrate using diagrams, check out [draw.io](https://www.draw.io/), which has a nice integration with github.

**AWS Method 1** (2 points)

Description: We've developed a python app that models a small dataset inside a Docker container that is set up for data analysis. For such a small development project, we could port to AWS using several low-cost services that can be turned on/off at will. S3 simple storage can hold our Titanic data for repeat model experiments. We can create a linux virtual machine using the EC2 compute service. (I created one that costs 20 cents and hour, with expandable EBS data storage and 16 GB of RAM.) We can upload our Docker python container to Amazon's container registry, with the latest module updates, and run it in the cloud to get results. We can also do further development on the project and update and store our Docker container on Amazon's Container Service. We can easily create identical instances so that collaborators on a project an work in the same software environment.

Strengths: This is a cheap way to compute if you don't want to invest in hardware. It's easy to accommodate the need for more data storage and computing power. The container storage makes it easy to work within Amazon's ecosystem, and because it supports Docker, there are many pre-existing starting points for containerized apps and modeling taskss. This approach would work for a small team of collaborators.

Weaknesses: There is a learning curve on AWS. This approach is not suited to large-scale apps or enterprise-wide projects; it's definitely for small data. The machine I built costs about $5 a day to operate, but as storage grows costs will get higher. Hardware-cloud tradeoffs would have to be computed.

My app is not industrialized -- (that's v. 2.0 tk) -- it doesn't grab updated data, it doesn't trap errors and recover if the source data changes, authentication requires manually putting in a username and password for Kaggle, there could be problems with Kaggle changing urls in the future, etc., etc. Furthermore, it's not optimized for security and could be easily hacked. There are no provisions for upgrading containers with newer modules. These weaknesses, for now, apply to all the methods I've proposed here and on GCP.

**AWS Method 2** (2 points)

Description: A more robust, industrial approach would be to create a stack like the one described in Agile Data Science. Imagine that our app would be analyzing thousands of data sets, or perhaps bank-sized transaction datasets to model customer behavior. AWS has services to distribute the computing needed over multiple, easy-to-instantiate computer instances. But since this is a small project,  my method 2 involes using Amazon's Machine Learning service, which is an all-in-one solution that holds data, creates a computing environment, runs models and produces predictions and output. I tried the tutorial and was impressed.

Strengths: Simpler to set up than making a containerized app environment. According to Amazon, it's extensible for big data and deep learning.

Weaknesses: Doesn't appear to be as configurable as setting up your own work environment. Hard to determine how pricing compares; choice likely will depend on the nature of the data science project.

**GCP Method 1** (2 points)

Description: Similarly in GCP we can set up a containerized virtual machine. I created one, installed Docker and successfully ran my python Titanic code. Data was stored locally on the instance I created, but could have been kept separately (and in larger volumes) in various formats (Cloud Storage, Cloud SQL, NoSQL, etc.) Google has its own container system, one it created then made opensource, called Kubernetes. I did not have time to experiment, but this could be another choice. GCP makes it easy to create clusters of containerized virtual machines to allow for collaborative work in the same environments. Google has a specialized container service, Container Engine, for this kind of application. There are convenience factor compared with setting up an individual project and VM instance, as in my trial.

Strengths: As with the AWS solution above, this is a boutique, small-scale approach. It's relatively easy to set up and inexpensive, makes for a good collabortive project environment, is agile. Once a template container enviroment is constructed, it can be easily replicated and shared. This is the method shown in the screenshots folder. (**NOTE:** *I had a fail problem with score_model.py on GCP that I didn't have on my Mac; the error involved encoding and pickle. I haven't had time to debug, but I suspect that my container isn't as containerized as I imagined, or it has something to do with the difference between Mac OS and Debian.)*

Weaknesses: Google does not have as many compute options as Amazon, and it appears that when storage and other features are added in, the cost quickly mounts. This approach is not suited to big data projects. Google's tutorials are fast but didn't always work. Fine tuning permissions to allow connectivity outside the container was frustrating and took a long time. GCP's instances were easy to set up, and their CLI in a pop-up window is easy to use and more flexible than ordinary terminals.

**GCP Method 2** (2 points)

Description: Google has a specialized machine learning service designed to handle big data. Imagine, again, that we are processing data from thousands of shipwrecks (just metaphorically) pouring in from satellite sensors around the globe in real time. We ingest the data, clean it, impute missing values, predict and score to forecast the realtime dangers of icebergs. Gogle's machine learning service is integrated with its storage services and a Cloud Dataflow service that integrates with Apache Spark and Kafka, each part of the Agile Data Science stack in our text. With TensorFlow, models can be trained locally from samples and then industrialized for larger data flows manged by Google.

Strengths: This is a theoretical big-data approach for taking an idea to industrial scale. Much the same could be done on AWS and Azure. Google seems to be in the forefront on Machine Learning, with a more integrated suite of services.

Weaknesses: Could be expensive -- on a per-shipwreck basis! But then again, as for all these cloud service providers, you can turn things on or off with a few clicks or command line entries. This kind of flexibility and efficiency is why cloud computing is creating a revolution in information technology. See other weaknesses listed above.




### Applied (7 points total)

Choose one of the methods described above, and implement it using your work from homework 2.  Submit screenshots in the *screenshot* folder on this repo to document the completion of your process.
