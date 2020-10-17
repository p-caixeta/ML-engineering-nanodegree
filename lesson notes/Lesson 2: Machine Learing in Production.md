# 1. Intro to production #

**Workflow:** explore&process data(retrieve, clean&explore, prepare/transform) ; modeling(develop&train model, validate/evaluate model) ; deployment (to production, monitor&update model)

**Paths to Deployment:**

-Python model is recoded into the programming language of the production environment.
 
-Model is coded in Predictive Model Markup Language (PMML) or Portable Format Analytics (PFA).
 
-Python model is converted into a format that can be used in the production environment.   <-----

The third method is to build a Python model and use libraries and methods that convert the model into code that can be used in the production environment. Specifically most popular machine learning software frameworks, like PyTorch, TensorFlow, SciKit-Learn, have methods that will convert Python models into intermediate standard format, like ONNX (Open Neural Network Exchange format). This intermediate standard format then can be converted into the software native to the production environment.

This is the easiest and fastest way to move a Python model from modeling directly to deployment.
Moving forward this is typically the way models are moved into the production environment.
Technologies like containers, endpoints, and APIs (Application Programming Interfaces) also help ease the work required for deploying a model into the production environment.

**Endpoint:** 
is the interface to the model. This facilitates an ease of communication between the model and the application. Specifically, 
Allows the application to send user data to the model and Receives predictions back from the model based upon that user data.

-the **endpoint** itself is like a function call 

-the function itself would be the **model** and

-the Python program is the **application**.

### Endpoint and REST API
Communication between the application and the model is done through the endpoint (interface), where the endpoint is an **Application Programming Interface (API)**.

An easy way to think of an API, is as a set of rules that enable programs, here the application and the model, to communicate with each other.
In this case, our API uses a **REp**resentational **S**tate **T**ransfer, **REST**, architecture that provides a framework for the set of rules and constraints that must be adhered to for communication between programs.
This REST API is one that uses HTTP requests and responses to enable communication between the application and the model through the endpoint (interface).
Noting that both the HTTP request and HTTP response are communications sent between the application and model.

-The HTTP request that’s sent from your application to your model is composed of four parts:

**Endpoint** (in the form of a URL, Uniform Resource Locator, which is commonly known as a web address)

**HTTP Method**(Below you will find four of the HTTP methods, but for purposes of deployment our application will use the POST method only.)

**HTTP Headers**(contains additional information, like the format of the data within the message)

**Message (Data or Body)** (for deployment will contain the user’s data which is input into the model)

![httpmethods.png](attachment:httpmethods.png)

-The HTTP response sent from your model to your application is composed of three parts:

**HTTP Status Code** (If the model successfully, the status code should start with a 2, like 200)

**HTTP Headers**(The headers will contain additional information, like the format of the data within the message)

**Message (Data or Body)** (What’s returned as the data within the message is the prediction that’s provided by the model)

-As we learn more about **RESTful API**, realize that it's the application’s responsibility:

To format the user’s data in a way that can be easily put into the HTTP request message and used by the model and
To translate the predictions from the HTTP response message in a way that’s easy for the application user’s to understand.

-Notice the following regarding the information included in the HTTP messages sent between application and model:

Often user's **data and prediction** will need to be in a **CSV or JSON** format with a specific ordering of the data that's dependent upon the model used.

-Both the model and the application require a computing environment so that they can be run and available for use. One way to create and maintain these computing environments is through the use of ****containers.****

Specifically, the model and the application can each be run in a container computing environment. The containers are created using a script that contains instructions on which software packages, libraries, and other computing attributes are needed in order to run a software application. A container can be thought of as a ****standardized collection/bundle of software**** that is to be used for the specific purpose of running an application.

-A common container software is **Docker**.

*Docker containers*:

Can contain all types of different software; 
The structure enables the container to be created, saved, used, and deleted through a set of common tools;
The common tool set works with any container regardless of the software the container contains.

*Docker structure*:

![container-2.png](attachment:container-2.png)

-The **underlying computational infrastructure** which can be: a cloud provider’s data center, an on-premise data center, or even someone’s local computer.

-an **operating system** running on this computational infrastructure, this could be the operating system on your local computer.

-**container engine**, this could be Docker software running on your local computer. The container engine software enables one to create, save, use, and delete containers

-The final two layers make up the **composition of the containers**: The first is the **libraries and binaries** required to launch, run, and maintain; and the next layer, the ****application layer****.

The applications are isolated from each other; the container only require the specific software for the app (lighter, faster); it is simple and secure to create, replicate, save and share.

# 2. Building a model using SageMaker #

**SageMaker** = Jupyter (in an AWS VM) + API

**Model artifacts** = saved model (e.g. random forest)

*Tools:*

Ground Truth - To label the jobs, datasets, and workforces

Notebook - To create Jupyter notebook instances, configure the lifecycle of the notebooks, and attache Git repositories

Training - To choose an ML algorithm, define the training jobs, and tune the hyperparameter

Inference - To compile and configure the trained models, and endpoints for deployments

****SageMaker Instances****
are the dedicated VMs that are optimized to fit different machine learning (ML) use cases. The supported instance types, names, and pricing in SageMaker are ****different than that of EC2.**** The type of SageMaker instances that are supported varies with AWS Regions and Availability Zones.

****Quotas****
https://sa-east-1.console.aws.amazon.com/servicequotas/home?region=sa-east-1#!/ (SA does not support this service yet)

to request higher quotas: https://classroom.udacity.com/nanodegrees/nd009t/parts/bb263cf2-a4c3-48f1-b5e9-957771b4790c/modules/ce966c86-ac77-4e58-97ee-eb396eeadc09/lessons/b922a210-7ac8-4786-a39d-a09daba5a170/concepts/6fd38593-8aa6-45c4-b85f-9127fd613a60

****Cloning the Deployment Notebooks****:  click on the new drop down menu and select terminal. Then:
cd SageMaker; 
git clone https://github.com/udacity/sagemaker-deployment.git; 
exit

****Random Trees tend to overfit****. Usar validation (pegar 1/3 do training pra isso)

****SageMaker Sessions & Execution Roles****:

Session - A session is a special object that allows you to do things like manage data in S3 and create and train any machine learning models. The upload_data function should be close to the top of the list! You'll also see functions like train, tune, and create_model all of which we'll go over in more detail, later.

Role - Sometimes called the *execution role*, this is the IAM role that you created when you created your notebook instance. The role basically defines how data that your notebook uses/creates will be stored. You can even try printing out the role with print(role) to see the details of this creation.

**XGBoost** is an optimized distributed gradient boosting library designed to be highly efficient, flexible and portable. It implements machine learning algorithms under the Gradient Boosting framework. XGBoost provides a parallel tree boosting (also known as GBDT, GBM) that solve many data science problems in a fast and accurate way. The same code runs on major distributed environment (Hadoop, SGE, MPI) and can solve problems beyond billions of examples.

->high level approach simplifies a lot of the details when working with SageMaker and can be very useful.

->to check logs: AWS > sagemaker > training;training jobs > logs (at the bottom)

A **model** is a collection of information that describes how to perform inference. For the most part, this comprises two very important pieces:

-The first is the container that holds the model inference functionality. For different types of models this code may be different but for simpler models and models provided by Amazon this is typically the same container that was used to train the model.

-The second is the model artifacts. These are the pieces of data that were created during the training process. For example, if we were fitting a linear model then the coefficients that were fit would be saved as model artifacts.

When a model is **fit** using SageMaker, the process is as follows.

First, a compute instance (basically a server somewhere) is started up with the properties that we specified.

Next, the code, in the form of a *container*, that is used to fit the model is loaded and executed. When this code is executed, it is provided access to the training (and possibly validation) data stored on S3.

Once the compute instance has finished fitting the model, the resulting model artifacts are stored on S3 and the compute instance is shut down.
