# Using InstructLab to add knowledge and skills to LLMs in a Jupyter notebook
## A guide for running Instructlab on Colab with a GPU
## By Kenneth Ocheltree, Steve Buckley

# Overview
This Jupyter notebook demonstrates InstructLab, an open source AI project that facilitates knowledge and skills contributions to Large Language Models (LLMs). InstructLab uses a novel synthetic data-based alignment tuning method for Large Language Models introduced in this [paper](https://arxiv.org/abs/2403.01081). The open source InstructLab repository is available [here](https://github.com/instructlab/instructlab) and provides additional documentation on using InstructLab.

The InstructLab method consists of three major components:
* **Taxonomy-driven data curation:**  The taxonomy is a set of training data curated by humans as examples of new knowledge and skills for the model.
* **Large-scale synthetic data generation:** A teacher model is used to generate new examples based on the seed training data. Recognizing that synthetic data can vary in quality, the InstructLab method adds an automated step to refine the example answers, ensuring they are grounded and safe.
* **Iterative model alignment tuning:** The model is retrained based on the synthetic data. The InstructLab method includes two tuning phases: knowledge tuning, followed by skill tuning.

<img src="https://github.com/KenOcheltree/ilab-colab/blob/main/data/images/Flow.png?raw=1" width="800">

InstructLab  can be instantiated in several different forms, depending on the processing capabilities available. InstructLab can take the form of an open source installation or a Red Hat AI InstructLab installation. The open source installation can be run on a range of hardware from a laptop to a build your own (BYO) server instance running on a Virtual Machine (VM).

In this notebook, we will demonstrate the open source version running on Colab with a GPU. The open source version running on a server is demonstrated in this notebook in the following major sections that are run sequentially:
* Configuring InstructLab
* Training with InstructLab
* Inferencing with InstructLab

# Prerequisites

Before running this notebook, you need to perform the following:
1. Arrange for Colab Paid Processing
1. Set up a Hugging Face Token and Place in Colab

## Arrange for Colab Paid Processing


## Set up a Hugging Face Token and Place in Colab
Set up an account on Hugging Face and create a Fine-grained access token with the following permissions: “Read access to contents of all repos under your personal namespace”; “Read access to contents of all public gated repos you can access”. Save the token value for the next step. 

Go back to Colab and on the left side select the Key icon and select "+ Add new secret". Name the secret “hf_token”. For the Value field enter your Hugging Face token value. Slide the Notebook Access slider to the right to enable it (it turns blue). Close the Secrets window.

# Steps

## Step 1. Open the Jupyter Notebook in Colab

Go to https://colab.research.google.com/.
Sign in with a Google account.

Select File->Open notebook, select Github on the left side and enter “KenOcheltree” for the GitHub URL.

Select the KenOcheltree/ilab-colab repository and select the notebook named running_instructlab_on_gpu.jpynb.


## Step 2. Select the GPU to use
•	This step is performed when you wish to change the GPU used for the session. Once a GPU is selected, whenver  

From the top menu, select Runtime->Change runtime type. You must select one of the GPU options. You can select a free GPU called T4 GPU which has a limited amount of resources. However, you may run out of free resources very quickly. There is an option in this dialog to obtain a paid account which has a larger resource allocation. You can start at $10 per month for a moderate amount of notebook testing. In this case, there are several GPU options. A100 GPU is a good option. You can monitor resource usage by selecting Runtime->View resources and change plans as needed.

## Step 3. Run the first cell to perform pre-reset installs 
Run the first code cell by clicking the arrow next to it. When it completes it will ask you to restart the session. Go ahead and restart the session (this only happens once).

## Step 4. Run the second cell and select the InstrutLab run parameters

Run the second code cell by clicking on the arrow next to it. Select the desired run parameters.


## Step 5. Run the remainder of the notebook

Select the third code cell without running it, and click on Runtime->Run cell and below to run the rest of the notebook.

After that run completes by exiting the inferencing loop, you can make another run if desired. To do that, go back to the second code cell, run it, and change the run parameters. Then select the third code cell without running it and click on Runtime->Run cell and below to run the rest of the notebook.


## Step 6. Run inference to compare the base model and the trained model

Click on the Folder icon on the left to explore the files in the ilab folder. Preloaded QNA files and synthetically generated questions and answers can be found in this directory tree.

## Step 7. Optionally Download trained model

## Step 8. Stop Runtime

## Step 9. Create your onw QNA File and repeat the above with your own data

# Summary and next steps

You can explore the complete implementation of the DPK transforms for fine-tuning LLMs in our Jupyter Notebook in our GitHub repo.