<img src="./images/VisualRecognition.png" width="20%"/>

# 3.3 Lab Watson - Watson Visual Recognition - Introduction

Watson Visual Recognition understands an image’s content out-of-the-box. The pre-trained models enable you to analyze images for objects, faces, colors, food, explicit content and other subjects for insights into your visual content.

Watson can also learn any new object, person, or attribute.

With only a few images, the computer vision service can learn any new object, person, or attribute such as identifying car type and damage to estimate repair costs. Train models effortlessly with Watson Studio — a free workspace where you can seamlessly create, evaluate, and manage your custom models.


In this lab, you go through a step-by-step process to use Watson Visual Recognition out-of-the-box and then you will create your own custom model using the integrated tooling available on IBM Cloud.


# Objective

In the following lab, you will learn:


+ How to use the Watson Visual Recognition API
+ How to use the Watson Studio tools to create your own custom model
+ Integrate the service in a web app


# Pre-Requisites

+ Get an [IBM Cloud Platform account] in the US region (https://cllebrun.github.io/labs/0_Registration/), or use an existing account.


# Steps

1. Using Visual Recognition with UI
2. Creating custom classifier with UI
3. Integrate Visual Recognition in your application with Node-Red

# Step 1 - Using Visual Recognition with UI

The first part of this lab will show you how to create a Visual Recognition Service, and use its tooling to test Watson provided models.

1. Login to IBM Cloud. https://cloud.ibm.com/login

2. Go to the IBM Cloud **Catalog** and select AI category.

 <img src="./images/catalog.png"/>

3. Then click the **Watson Studio** tile, then choose a name for your service (e.g. Watson Studio-pizza), in the **DALLAS** region, then click the Create button.

 <img src="./images/studio-service.png"/>
Watson Studio is the tool for building AI models in a collaborative fashion so you can provide a more democratic training process that reduces AI biases.

4. Click the Get Started button to open Watson Studio.
5. Click the Get Started button when prompt.

6. Click **Create a project**.
   <img src="./images/create-project.png"/>
7. Select **Visual Recognition** type of project.
   <img src="./images/vr-project.png"/>

8. Select the **US South** region.
   <img src="./images/vr-region.png"/>

9. Enter a name for your project (e.g. My Pizza Quality Check) and a description if you like then click the **Create** button. This project will create a Watson Visual Recognition service and the needed Cloud Object Storage.
   <img src="./images/pizza-check.png"/>



   Great! You have created a new machine learning project that you can collaborate on with others, upload data-sets, and create training models. Additionally, this project wizard has instantiated the Watson Visual Recognition service that is pre-trained on millions of consumer oriented images and can be used with no additional training (as we'll see below).

   However, since consumer data represents only 20% of the world's data, we will create a custom model below to teach Watson your business and what insights are in your images that consumer trained visual recognition software just doesn't cover.

**Test the General model:**

Before creating a custom model, let's check out the General model and the Food model that IBM has already trained on millions of images.

10. Click the **watson-visual-combined-dsx** link for the Watson Visual Recognition service that was automatically created for you.
   <img src="./images/default-model.png"/>



11. Click the Test button of the General model panel.

12. Click the Test tab of this model to upload an unlabeled image that Watson will examine to determine what insights can be gleaned from Watson's training of millions of images.
  <img src="./images/test-general.png"/>

13. Locate your favorite image search tool to find test images, use your personal images or drag images from [Test images folder](https://github.com/cllebrun/cllebrun.github.io/tree/master/labs/3.3%20Lab%20Watson%20-%20Watson%20Visual%20Recognition/Lab1%20-%20Test%20Images)
  <img src="./images/test-general-images.png"/>

Notice it displays the confidence score (which is the statistical probability of this classification against other classifiers in this model).

Now let's explore the Faces model.

14. Click the watson-vision-combined-dsx link to return to the model choices.

15. Click the Test button of the Faces model.

16. Click the Test tab of this model then drag images from [Test images folder](https://github.com/cllebrun/cllebrun.github.io/tree/master/labs/3.3%20Lab%20Watson%20-%20Watson%20Visual%20Recognition/Lab1%20-%20Test%20Images) on the canvas.

<img src="./images/test-faces-images.png"/>
As you can see, the Faces model not only detect the number of persons, but also the gender and an estimate of the age. It also locates the position of each faces on the picture.

Out of the box, Watson can tell you what kind of objects are in a photo even though these are your private photos that have not been indexed by a search engine nor contain labeled tags that tell Watson what the photo is about -- instead Watson can deduce this by comparing your photo against the millions of labeled photos that Watson has been trained on.

Yet still, these millions of photos are a drop in the bucket compared to how many photos are in the world and only come from the small 20% of consumer facing data, which leaves 80% of data behind your firewall -- and inside this data is your companies competitive edge.

Therefore, let's examine how easy it is to teach Watson something that consumer oriented AI doesn't do.

# Step 2 - Creating custom classifier with UI

Objectives : Teaching Watson New Tricks

The Visual Recognition service is trained by providing example images for each classification bucket -- the more examples you provide, the better the accuracy. After Watson has trained itself on your images, then it will classify a new image that it has never seen before and calculate how confident it is that it belongs to one of your classification types.

1. Once again click the **watson_vision_combined-dsx** service link to return to the model choices.

2. Click on the **Create Model** button on the Classify Images tile.
  <img src="./images/classify-images.png"/>

3. Rename your model "Default Custom Model" by "PizzaConditionModel"

4. You will now load images create your model classes. The pane to manage file upload is shown on the right side of your screen.
Click the Browse button to upload a zip file containing at least 10 photos (.jpg or .png) for good pizzas, at least 10 photos for bad pizzas, and 10 photos for not-pizzas. You can also drag and drop from your file explorer good_pizza_images.zip, bad_pizza_images.zip and not_pizza_images.zip in the [Lab 2 - Training Set folder](https://github.com/cllebrun/cllebrun.github.io/tree/master/labs/3.3%20Lab%20Watson%20-%20Watson%20Visual%20Recognition/Lab2%20-%20Training%20Set).

  <img src="./images/upload-jpeg.png"/>
