# Using InstructLab to add knowledge and skills to LLMs in a Jupyter notebook
### A guide for running Instructlab on Colab with a GPU
### By Kenneth Ocheltree, Steve Buckley

# Overview
This Jupyter notebook demonstrates InstructLab, an open source AI project that facilitates knowledge and skills contributions to Large Language Models (LLMs). InstructLab uses a novel synthetic data-based alignment tuning method for Large Language Models introduced in this [paper](https://arxiv.org/abs/2403.01081). The open source InstructLab repository is available [here](https://github.com/instructlab/instructlab) and provides additional documentation on using InstructLab.

The InstructLab method consists of three major components:
* **Taxonomy-driven data curation:**  The taxonomy is a set of training data curated by humans as examples of new knowledge and skills for the model.
* **Large-scale synthetic data generation:** A teacher model is used to generate new examples based on the seed training data. Recognizing that synthetic data can vary in quality, the InstructLab method adds an automated step to refine the example answers, ensuring they are grounded and safe.
* **Iterative model alignment tuning:** The model is retrained based on the synthetic data. The InstructLab method includes two tuning phases: knowledge tuning, followed by skill tuning.

<img src="./images/Flow.png" width="800">

InstructLab  can be instantiated in several different forms, depending on the processing capabilities available. InstructLab can take the form of an open source installation or a Red Hat AI InstructLab installation. The open source installation can be run on a range of hardware from a laptop to a build your own (BYO) server instance running on a Virtual Machine (VM).

In this notebook, we will demonstrate the open source version running on Colab with a GPU. The open source version running on a server is demonstrated in this notebook in the following major sections that are run sequentially:
* Configuring InstructLab
* Training with InstructLab
* Inferencing with InstructLab

# Prerequisites

Before running this notebook, you need to perform the following:
1. Sign In to Colab with a Google Account
1. Arrange for Colab Paid Processing
1. Set up a Hugging Face Token and Place in Colab

## Sign In to Colab with a Google Account

Go to the the Colab page (https://colab.research.google.com/) and select Sign In at the upper right.

<img src="./images/ColabWelcome.png" width=700>

Select a Google Account to use with Colab. If you do not have a Google account, choose Sign in and on the SIgn In page, select Create account at the lower right.

<img src="./images/SignIn.png" width=500>

Proceed though the steps to create a Google Account and then come back to the [Colab Sign In page](https://colab.research.google.com/) and sign in with your account

## Arrange for Colab Paid Processing

While signed into your Google account, go to the [Colab Plan page](https://colab.research.google.com/signup?utm_source=notebook_settings&utm_medium=link&utm_campaign=premium_gpu_selector). 

<img src="./images/ColabPlan.png" width=600>

Select one of the four offered plans that give access to a GPU with memory of at leat 18 GB. A typical single Instructlab run on a GPU will incur charges of one to two dollars. After selecting a plan, you will have to pay for it before you can use the GPU.

Once you have a Paid Colab Account, you will be able to select your choice of GPU.

## Set up a Hugging Face Token and Place in Colab
Go to the [Hugging Face site](https://huggingface.co/).

<img src="./images/HF.png" width=700>

If you have previously used that site, select **Log In** and provide your credntials. Otherwise, select Sign Up and create a free HuggingFace account.

Select your account icon in the upper right and from teh drop down meu select **Access Tokens**.

<img src="./images/HFDropDown.png" width=200>

On the Access Token page, select Create Token at the upper right.

<img src="./images/HFAccessTokens.png" width=600>

Create a Fine-grained access token with the following permissions: “Read access to contents of all repos under your personal namespace”; “Read access to contents of all public gated repos you can access”. Save the token value for the next step. This is done on the Create new Access Token page, by selecting **Fine-grained**, name the Token "ilab", select the first two boxes under ***Repositories*** and move to the bottom of the page and select **Create Token**.

<img src="./images/HFCreateToken.png" width=400>

On the popup that shows your access token, select the Copy Button, then Done.

Now go back to [Colab](https://colab.research.google.com/) and select the key icon in the left column.

<img src="./images/ColabKey.png" width=80>

On the new sceen that appears, select **+Add new secret**/

<img src="./images/ColabAddSecret.png" width=400>

Name the secret "hf_token" and paste the copied HuggingFace Token into the "Value" field. Slide the Notebook Access slider to the right to enable it (it turns blue). Close the Secrets window. 

<img src="./images/ColabSecretEnabled.png" width=400>

# Steps

## Step 1. Open the Jupyter Notebook in Colab

Go to https://colab.research.google.com/ and sign in with your Google account. 

Select File->Open notebook, select Github on the left side and enter “KenOcheltree” for the GitHub URL. Select the KenOcheltree/ilab-colab repository

<img src="./images/Github.png" width=600>

At this point, Select the notebook named running_instructlab_on_gpu.jpynb and it will open into Colab.

<img src="./images/RunningILab.png" width=600>


## Step 2. Select the GPU to use

This step is performed when you wish to change the GPU used for the session. Once a GPU is selected, whenver  

From the top menu, select Runtime->Change runtime type. You must select one of the GPU options. You can select a free GPU called T4 GPU which has a limited amount of resources. However, you may run out of free resources very quickly.

<img src="./images/ColabChangeRuntime.png" width=400>

The A100 GPU is a good option. You can monitor resource usage by selecting Runtime->View resources and change plans as needed.

## Step 3. Run the first cell to perform pre-reset installs 
Run the first code cell by clicking the arrow next to it. 

<img src="./images/ColabRunFirst.png" width=400>

When it completes it will ask you to restart the session. Go ahead and restart the session (this only happens once).

<img src="./images/ColabRestart.png" width=400>

## Step 4. Run the second cell and select the InstrutLab run parameters

Run the second code code cell by clicking on the arrow next to it. Once the second cell is run, it presents a number of different parameters available for running Instructlab.

<img src="./images/IlabParms.png" width=400>

Select the desired run parameters. The paramters are as follows:


## Step 5. Run the remainder of the notebook

Select the third code cell without running it, and click on **Runtime->Run cell and below** to run the rest of the notebook.

The run will proceed as follows:
1. Complete the environment setup by downloading and installing instructlab and other required packages
1. Configure the InstructLab installation for running
1. Download necessary Models for training and teaching
1. Create a taxonomy with the new data to be added
1. Perform synthetic data generation
1. Perform model training wiht the synthetic data


After that run completes by exiting the inferencing loop, you can make another run if desired. To do that, go back to the second code cell, run it, and change the run parameters. Then select the third code cell without running it and click on Runtime->Run cell and below to run the rest of the notebook.


## Step 6. Run inference to compare the base model and the trained model

Click on the Folder icon on the left to explore the files in the ilab folder. Preloaded QNA files and synthetically generated questions and answers can be found in this directory tree.

## Step 7. Optionally Download trained model

## Step 8. Stop Runtime

## Step 9. Create your onw QNA File and repeat the above with your own data

# Summary and next steps

You can explore the complete implementation of the DPK transforms for fine-tuning LLMs in our Jupyter Notebook in our GitHub repo.