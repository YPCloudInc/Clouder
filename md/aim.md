Hello AI Marketplace
===
Get started with AI Marketplace! 

GitBook Handbook: http://203.145.214.235:4000/

Model Training Example: [Link](md/aim_model_example.md)

## What is AI Marketplace
AI Marketplace is an online platform for training, purchasing, and using AI models on the TWCC cloud. 

Customers can easily find, buy, and deploy AI models in moments.

Developers have a one-stop workspace where they can train and deploy ML models online using TWCC cloud resources, then sell their models in the Marketplace. 

## Sign in to AI Marketplace
To complete this tutorial, you need an iService account and have a project wallet with credits.

- If you don't already have an iService account, go to iservice.nchc.org.tw and select **Registration** to create a new one. 

- Please ensure that you are part of the AI Market project and have available credits. Have a project admin add you to the AI Market project. 

#### TWCC Documentation
- [確認已有可用計畫](https://man.twcc.ai/@twccdocs/rJ09wRoa4?type=view)

- [Manage Project Team](https://man.twcc.ai/@twccdocs/BJe4IOiNH?type=view)

- [申請使用計畫](https://man.twcc.ai/@twccdocs/rkXUICiTE?type=view)

- [HowTo：從 TWCC 進入 Service 會員系統？](https://man.twcc.ai/@twsdocs/howto-service-access-service-zh)

#### Login
- Go to ai-mkt.nchc.org.tw (ai-labs.nchc.org.tw) and click the icon on the top-right corner to sign in. 

## ML Training (The Developer's Guide)

### Prepare MLflow
Your personal MLflow tracking server and UI will be created automatically the first time you login to AI Marketplace. 

It may take some time to get ready for you to start logging model training runs, so give it a minute to finish setting up. 

Go to the [MLflow] page to check its status. Once you can successfully load the MLflow UI page, you can start your ML training. 
![](https://i.imgur.com/yrwpNjZ.png)

- Introduction to MLflow [[link]](https://databricks.com/blog/2018/06/05/introducing-mlflow-an-open-source-machine-learning-platform.html)

- MLflow Documentation [[link]](https://mlflow.org/docs/latest/index.html)

### Begin your Jupyter Notebook instance
1. Go to the [Jupyter] page on AI-Marketplace and create a new TWCC container. This is where your Jupyter Notebook will run. 
![](https://i.imgur.com/xarC9Kv.png)

2. Name the container (preferably with your name), select the container image (either Tensorflow or Pytorch), and select the container specs. For the purposes of this tutorial, select `1 GPU, 4 cores, 90 GB memory`.
![](https://i.imgur.com/mqPBUET.png)

3. Click 'Create' to confirm.

4. It will take some time for your container to be created. Once [Progress] has reached 100, you can click [Run] to open Jupyter Notebook.
![](https://i.imgur.com/J9YT79O.png)

- Sample Jupyter Notebook:
![](https://i.imgur.com/ZCQGoRG.png)

- JupyterLab is also available on this server. Simply change the last component of the url address `/tree` to `lab`. 

### Model training with Jupyter Notebook
1. Upload your ML source code. 
  Here are some examples you can use:
- [train-wine-quality.py](https://cos.twcc.ai/modelmarketplace/YPcloud/train-wine-quality.py)
- [train-mnist.py](https://hackmd.io/luY3t5_hTL66ZuP_GSnS-w?view#mnist)

2. Edit MLflow APIs in the python ML source code. MLflow API functions include: 
  - save model
  - save artifact (ML training output) to [file path location]
  - register model under "registered_model_name" 
  - describe input/output
  - provide input examples

Example: ![](https://i.imgur.com/3rRwJ8E.png) 
 
 With the ML training source code examples provided above, you will only need to edit the "registered_model_name" in the code line 
`mlflow.<model_flavor>.log_model(`

e.g.

>
    # Log the sklearn model and register as version 1
    mlflow.sklearn.log_model(
        sk_model=sk_learn_rfr,
        artifact_path="sklearn-model",
        registered_model_name="sk-learn-random-forest-reg-model"
    )


2. Open a terminal (or use notebook cells) to install packages. Use the following commands:
    ```
    pip install mlflow
    pip install boto3
   ```
   And install packages for particular model types
    
    `pip install sklearn`(for wine-quality)
    `pip install keras` (for mnist)


3. Execute model training
   - Use the following command (in terminal):
   ```
   python train-wine-quality.py
   ```
Once the run finishes, you should be able to view your training results in MLflow and see your training result on the My Models list.

The list on the [My Models] page corresponds to [Registered Models] in the MLflow UI. 
![](https://i.imgur.com/OTLfrjV.png)

5. Remember to shutdown all running files and logout, then delete your container to terminate your instance. 

:::warning
You will continue to be billed for a running container if you don't delete your container. 
:::

### MLflow UI
Go to the MLflow UI page to view your training logs, artifacts, and registered models. <br> Here you can compare different runs with MLflow in-built functions. 
![](https://i.imgur.com/uETtyps.png)




## Publish your model 
1. On your Model List, find the model you wish to publish and click 'Test'.
![](https://i.imgur.com/syf8zXl.png)

2. Confirm publish/test in the popup window. The container for Swagger will be created. 

3. The Status of the Swagger container will be 'Initializing' until it is ready for use. Click 'Cancel' for now. (Clicking 'Finish' will delete the container). 

4. Go to the "Tested Models" Model List to find the model you want to publish. Click 'Preview', then click 'Go Model'. ![](https://i.imgur.com/JbUhr4L.png)

5. On the Swagger page, click 'Try it out' to change the input parameters and run an ML inference test. ![](https://i.imgur.com/RduArxA.png)

6. Once you are done, return to the "Tested Models" Model List and click 'Delete' to delete the container running Swagger.

7. Go to the "Models" Model List and click 'Publish' to fill out details about your model and confirm publish. ![](https://i.imgur.com/g2fh5DB.png)

8. Once your publish request has been reviewed by admin, it will be officially published and visible on the public model list, available for other users to subscribe to and deploy. 

## Subscribe to and deploy models 
To deploy an AI model from the AI Marketplace store....

## Training ENV API Keys
#### Cloud Object Storage (S3) API Keys and MLflow UI

:::success
These environment paramaters are now set by default. The steps in this section can be skipped. 
:::

When training your AI model, you need to set your artifact and training log output location.
      
      export MLFLOW_S3_ENDPOINT_URL=https://cos.twcc.ai
      
      export AWS_ACCESS_KEY_ID=
      
      export AWS_SECRET_ACCESS_KEY=
      
      export MLFLOW_TRACKING_URI=

- To obtain your s3 (TWCC COS) access key and secret key, login to https://www.twcc.ai with your iService account and go to Cloud Object Storage > Private COS 
![](https://i.imgur.com/MbllxaU.png)
![](https://i.imgur.com/QJqRm3P.png)

- To obtain your MLflow tracking URI, make sure you are signed in to your account on AI Market, and go to the MLflow page. Right-click on the MLflow logo to copy the link address. 
  ![](https://i.imgur.com/f8xjPp8.png)

#### CKAN API Key
The NCHC Data Market provides a free, public database of datasets that can be used for your ML training. 

- To access your NCHC Data Market API Key, go to https://scidm.nchc.org.tw/ and sign-in with your iService account. Select your profile in the top-right to view your personal account details. 

Your details are in the bar on the left. Scroll to the bottom to find your API key.

If you wish to create a new CKAN API key, go Manage/Edit Settings, scroll to the end of the page and click **Regenerate API Key**. 

#### TWCC API Key
- To obtain your TWCC project API key, sign in to twcc.ai, and click on the Account & Project Information button in the top-right corner, displayed as **[:bust_in_silhouette: NAME]**. <br> From the dropdown list select **API Key** to go your API Key Management Page. Here you can copy, delete and create API keys. 

## What is MLflow
(copied from databricks AWS docs)

MLflow is an open source platform for managing the end-to-end machine learning lifecycle. It has the following primary components:

- Tracking: Allows you to track experiments to record and compare parameters and results.

- Models: Allow you to manage and deploy models from a variety of ML libraries to a variety of model serving and inference platforms.

- Projects: Allow you to package ML code in a reusable, reproducible form to share with other data scientists or transfer to production.

- Model Registry: Allows you to centralize a model store for managing models’ full lifecycle stage transitions: from staging to production, with capabilities for versioning and annotating.

- Model Serving: Allows you to host MLflow Models as REST endpoints.

MLflow supports Java, Python, R, and REST APIs.

https://docs.databricks.com/applications/mlflow/tracking.html

- NCHC AI Marketplace manages a fully managed and hosted version of MLflow. MLflow is the main tool for tracking ML training experiments and managing model registry, and is also used to serve models as REST endpoints running on TWCC resources. 

---
# FAQs
# AI Model Marketplace - FAQs

Created at: 2022/07/04

### No MLflow UI + unable to create Jupyter Notebook
- Make sure you are a member of the iService project and have valid wallet credits.

- AI Marketplace > My Wallet <br> https://ai-mkt.nchc.org.tw/en-us/user/profile/wallet

- iService https://iservice.nchc.org  

- Member Center > Projects > My Projects
![](https://i.imgur.com/wa631PV.png)


### Unable to delete Jupyter Notebook container
![](https://i.imgur.com/03F8Kqh.png)

Go to https://www.twcc.ai, login with your iservice account. Make sure you are in the NCHC-AI Model Marketplace project. 

From the Services list, select: Compute > Interactive Container (運算>開發型容器)

Delete your container from the list. 

If you have admin rights, you will be able to see everyone's containers. Please be careful about the changes you make through the www.twcc.ai console. 

![](https://i.imgur.com/d4EX74o.png)

### Swagger UI: Error 401

![](https://i.imgur.com/PubOm0P.png)

Get API key from model info page

![](https://i.imgur.com/CDsPSo8.png)
![](https://i.imgur.com/oxeSbOr.png)

![](https://i.imgur.com/JK5FLtJ.png)

---
[Shin's Document](https://hackmd.io/@ypsc/SkJcFfVIu)
###### tags: `AIM`
---
> [YPCloud Inc.](https://www.ypcloud.com)
> [name=Shin]
> [time=Aug23, 2022]
