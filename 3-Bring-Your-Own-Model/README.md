# Deploy a SageMaker trained model to your DeepLens

## Module Objective
In this section of the workshop, we are going to train a custom model using Amazon SageMaker and then deploy that model to
AWS DeepLens for inference at the edge.  We are going to use MXNet Deep Learning framework with a pretrained ResNet model
and build a classifier for the [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) data set.

The basic steps involved include: 

1. **Model Training:** Training your model using Amazon SageMaker and export model artifacts to S3
2. **Import Model to AWS DeepLens:** Import your model artifacts from S3 and deploy it to your AWS DeepLens device
3. **Evaluate Model Performance:** Evaluate your model by looking at the DeepLens output

## Model Training

1. Using your browser, open the Amazon SageMaker console at https://console.aws.amazon.com/sagemaker/.
2. Sign in to the console using the ID & credentials provided as part of the workshop.
3. Choose **Notebook Instances** from the left hand menu, then choose **Open Jupyter** next to the notebook you created in the earlier lab
4. Import the notebook `mxnet_cifar10_with_gluon` from this repository.  
5. Trust the notebook after the import is complete.
6. Upload the python scripts `cifar10.py` and `cifar10_utils.py` into the same folder on your notebook instance.
7. Create a new S3 bucket with a name starting with `deeplens`.  Enter the name of this bucket in the first cell block for the variable `bucket`.
8. Execute all the cells in the notebook.  The training job will take about 10 minutes to finish.

## Import Model to AWS DeepLens

 1. Follow the steps outlined in [Import Your Amazon SageMaker Trained Model](https://docs.aws.amazon.com/deeplens/latest/dg/deeplens-import-from-sagemaker.html) to import your model to DeepLens.
 2. Follow the steps outlined in [Create and Publish an Inference Lambda Function](https://docs.aws.amazon.com/deeplens/latest/dg/deeplens-inference-lambda-create.html) to create the function that will run on your DeepLens.  Use the code in the file `lambda.py` for the function.
 3. Follow the steps outlined in [Create and Deploy a Custom AWS DeepLens Project](https://docs.aws.amazon.com/deeplens/latest/dg/deeplens-create-custom-project.html) to publish your new project to the DeepLens.
 
 *Note:* When importing the model choose MXNet as the **Model Framework**

## Evaluate Model Performance

After publishing the project, look in the `Project output` section of the DeepLens console.  Follow the instructions there to look at the output of the CIFAR10 model in the IoT console.  You'll see JSON-formatted messages that show the probability of each of the 10 classes in the CIFAR10 data set.  

Try pointing your DeepLens at some objects like a car or an airplane and see if the results match up (your lab instructors may have some toy cars and planes you can borrow).  But be aware that we only trained the model for 5 epochs to save time, so the results may not be very impressive yet.
