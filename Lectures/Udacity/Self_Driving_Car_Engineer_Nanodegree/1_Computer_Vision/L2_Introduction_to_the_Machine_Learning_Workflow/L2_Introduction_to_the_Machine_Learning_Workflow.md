#### 2021/12/29
## Lesson 2: The Machine Learning Workflow
### Introduction to the Machine Learning Workflow
- In the lesson, we are going to learn how to think about Machine Learning problems. Machine Learning (ML) is not only about cool math and modeling but also about choosing setting the problem, identifying the client needs and the long term goals. This lesson is going to be organized as follow:
  - We will practice framing Machine Learning problems by identifying the key stakeholders and choosing the correct metrics.
  - Because ML is about data, we will discuss the different challenges linked to data.
  - We will also tackle how to organize your dataset when solving a ML problem to be confident that you created a model that will perform well on new data.
  - Finally, we will see how you can leverage different tools to pinpoint your model's limitations.
- In this course, we will be using the German Traffic Sign Recognition Benchmark (GTSRB) multiple times for exercises. A downsampled version of the dataset has already been downloaded to your workspace.

### Big Picture
- In the following videos and lessons, we are going to take a deeper dive into each component of the workflow.
  - Problem setup is the phase where we set the boundaries of the problem and will be tackled in the next few videos.
  - The Data part of the workflow consists in getting familiar with the available dataset and will be the main focus of the next lesson on the camera sensor.
  - Modeling is such a critical step that we will spend 3 lessons on it. Modeling consists in choosing and training different models and picking the best one.
- Classifying Traffic Signs
  - Problem: Classifying traffic signs from images
  - Data: Thousand of images for each type of traffic sign
  - Model: Logistic regression, neural network

### Framing the Problem
- Do I even need Machine Learning?
- Who are the key stakeholders?
- What data do I have access to?
- Which metrics should I use?
- `As a machine learning engineer, it is easy to solely focus on model performances, but you may need to consider other factors as well`
- Unless you are taking part in a Machine Learning competition, the model's performance is rarely the only thing you care about. For example, in a self-driving car system, the model's inference time (the time it takes to provide a prediction) is also an important factor. A model that can digest 5 images per seconds is better than a model that can only manage one image per second, even if the second one is performing better. In this case, the inference time is also a metric to choose our model.

- Understanding your data pipeline is very important because it will drive your model development. In some cases, getting new data is relatively easy but annotating them (by associating a class name for example) may be expensive. In this case, you would want to create a model that requires less data or that can work with unlabeled data.
- `Machine Learning is an iterative process. You should always start with a simple model before building on complexity. Moreover, the business side often drives the metrics and the problem itself.`

### Identifying the Key Stakeholders
- Who is going to be impacted by the product?
- Stakeholders if ride sharing app:
  - Customers
  - Drivers
  - Engineering teams
- As a Machine Learning Engineer, you will rarely be the end user of your product. Therefore, you need to pinpoint the different stakeholders of the problem you are trying to solve. Why? Because this will drive your model development.
- Congratulations! Self-driving car technology will indeed impact many aspect of our society and this is what makes this technology so exciting. Daily commuters, insurance companies and environmentalists will benefit from the reduced traffic and car accidents. I recommend reading this excellent article on [the impact of self-driving cars on cities](https://www.washingtonpost.com/transportation/2019/07/20/city-planners-eye-self-driving-vehicles-correct-mistakes-th-century-auto/).

### Choosing Metrics
- Business metrics != Machine Learning metrics
- A good metric must be easy to understand and adapted to a specific problem
- Machine leanring metrics, like accuracy, may not be the best indicator of success from the business side
- You created an app that classify an image as containing a burger or not.
  - **True Positive (TP)**: The image contains a burger and the model predicts burger
  - **True Negative (TN)**: The image does not contain a burger and the model does not predict burger
  - **False Positive (FP)**: The image does not contain a burger and the model predicts burger
  - **False Negative (FN)**: The image contains a burger and the model does not predict burger

- Each Machine Learning problem requires its own metrics, and whereas some metrics like Accuracy may be suited for many problems, you need to keep in mind the consequences of misprediction. 
- Let's consider the following: you are building a spam classification algorithm. 
- Well, you should aim for very few False Positives, because you do not want your algorithm to classify some potentially important emails to your spam folder. 
- A False Negative however is simply a spam located in your inbox, which could be manually removed by the user.

### Classification & Object Detection Metrics
- **Precision = TP / (TP + FP)**
  - Of the elements classified as a particular class, how many did we get right? For example, we classified 6 images as containing burgers and only 5 of them actually contain a burger. The precision is 5/6
  - True 라고 한 것 중에 실제로 True인 비율
- **Recall = TP / (TP + FN)**
  - The number of images classified correctly divided by the total number of images. For example, we have 40 images of burgers and we classified 15 of them correctly. The recall is 15/40.   
  - True 여야 하는데 진짜 True라고 맞힌 비율
- **Accuracy = TP + TN / (TP + FN + FP + TN)**
  - (Only for classification problems) The number of correctly classified images over the total number of images.
--- 
- **Intersection over Union**
  - IOU is defined as the ratio of the intersection of bounding boxes and the union of bounding boxes.
  - `An IOU of 0.5 between a ground-truth bounding box and a detected bounding box is a pretty common threshold to qualify the detection as a TP.`
---
#### 2021/12/30
### Using a Desktop Workspace
- Certain exercises in this course make use of Workspaces attached to a virtual desktop that you can use to display visual output from your programs or to work with Linux desktop applications, such as Visual Studio Code.
#### Viewing the Desktop
- You can view the Desktop by clicking on the "Desktop" button in the lower right side of the Workspace. This will open a new window in your browser with the virtual desktop. The desktop has a Visual Studio Code application along with a terminal app called Terminator, which can be used to browse files or run code.

- Try the desktop now in the workspace below!

Note: Just as with other Workspace types, the Desktop will disconnect after 30 minutes of inactivity.
- Note that if you are working on exercises that make use of matplotlib to show plots or images, you can still choose to work directly out of the main workspace window when programming, but viewing the pop ups for any visualizations will require you to navigate to the Desktop button to view them.

#### Enabling GPU Mode in Desktop Workspaces
- Several desktop workspaces require the use of a GPU to display the desktop. If a desktop workspace has support for GPU, it will be displayed on the bottom left corner of the workspace, as shown in the snapshot below:
- You are provided with a fixed number of GPU hours at the beginning of this Nanodegree program. The amount of GPU time you have remaining in your account is displayed in the lower-left corner of your workspace.
- GPU Workspaces can also be run without time restrictions when the GPU mode is disabled. The "Enable"/"Disable" button can be used to toggle GPU mode. Note that in GPU-enabled workspaces, some libraries will not be available without GPU support.
  
NOTE: Toggling GPU support may switch the physical server your session connects to, which can cause data loss unless you click the save button before toggling GPU support.

#### 2021/12/31
### Data Acquisition and Visualization
#### Data
- Understand the data:
  - Orogin
  - Sensor
  - Labels
- ML engineering is all about data!
- `You will spend your time building data pipelines, creating data visualization, and trying to understand as much as possible about your dataset.`
- In many cases, you will need to gather your own data but in some, you will be able to leverage Open Source datasets, such as the Google Open Image Dataset. However, keep in mind the end goal and where your algorithm will be deployed or used.
- Because of something called domain gap, an algorithm trained on a specific dataset may not perform well on another. For example, a pedestrian detection algorithm trained on data gathered with a specific camera may not be able to accurately detect pedestrians on images captured with another camera.
---
#### 2022/01/02
### Exercise: Data Acquisition and Visualization
---
#### 2022/01/04
### Exploratory Data Analysis (EDA)
- Machine Learning algorithms may be very sensitive to domain shift. This domain shift can happen at different levels:

  - **Weather / light conditions**: for example, an algorithm trained only on sunny images is not going to perform well when shown rainy or night-time data.
  - **sensor**: a sensor change or different processing methods will create a domain shift.
  - **environment**: an algorithm trained on low intensity traffic data will not perform well on high intensity traffic data for example.
- An extensive Exploratory Data Analysis (EDA) is critical to the success of any ML project. Why? Because during this phase, the ML engineer gets acquainted with the dataset and discovers any potential challenges with the data. The EDA is such an important part of the project that ML engineers spend a few days on it alone. For a vision problem, it requires looking at 1,000s of images in your dataset!

### Cross Validation
- The goal of our ML algorithm is to be deployed in a production environment. For example, the object detection algorithm you will create in the final project could be deployed directly in a self driving car. But before we can deploy such algorithms, we need to be sure that it will perform well in any environments it will encounter. In other words, we want to evaluate the generalization ability of our model.

- We are going to introduce three new concepts:
  - overfitting: when the model does not generalize well
  - bias-variance tradeoff: why is it hard to create a balanced model
  - cross validation: a technique to evaluate how well the model generalizes

#### Overfitting
- When a model is overfitting, it loses its power to generalize. It often happens when the chosen model is too complex and starts extracting noise instead of meaningful features. For example, a car detection model is overfitting when it starts extracting brand specific features of the cars in the dataset (e.g., car logo) instead of broader features (wheels, shape etc).

- Overfitting raises a very important question. How do we know if our model will generalize properly or not? Indeed, when a single dataset is available, it will be challenging to know if we created a model that overfits or simply performs well.

#### Training vs. Test Datasets
- For now, we will use the terms training data to describe the data used to teach and create our algorithm and test data for any new, unseen data.

#### Bias & Variance Trade-off
- The **bias-variance tradeoff** illustrates one the most important challenges in Machine Learning. How do we create a model that performs well while keeping its ability to generalize to new, unseen data? The performance of our algorithm on such data is quantified by the test error. The test error can be decomposed in further into the bias and the variance.

- The **bias** quantifies the quality of the fit of our model on the training data. A low bias means that our model has a very low error rate on the training dataset.

- The **variance** quantifies the sensitivity of the model to the training data. In other words, if we were to replace our training dataset with another one, how much would the training error rate change? A low variance means that our model is not sensitive to the training data and generalizes well.

#### Validation Sets & Cross Validation
- Cross validation is a set of techniques to evaluate the capacity of our model to generalize and alleviate the overfitting challenges. In this course, we will leverage the validation set approach, where we split the available data into two splits:
  - a training set, used to create our algorithm (usually 80-90% of the available data)
  - a validation set used to evaluate it (10-20% of the available data)
- Use the validation set to select the best parameters or compare models.
- Test set: never evaluated on until the cross-validation is done.
- Careful of data leakage:
  - by aiming to get the best possible performances on the validation set, we leak information from training to validation.
  - If the splits are not perfromed correctly.

- In further videos, we will see how we can leverage this approach to alleviate the overfitting problem.
- Other cross validation methods exist, such as LOO (Leave One Out) or k-fold cross validation but they are not suited to Deep Learning algorithms. You can read more about these other two techniques [here](https://www.cs.cmu.edu/~schneide/tut5/node42.html).

#### 2021/01/07
### TFRecord
- Tf rerords are TensorFlow custom data format
- They are not required to train a model with TensorFlow but may help to speed up data loading
- Their structure is defined by proto files
- TF records are created using Protocol buffers (protobuf), a mechanism to serialize data
- For some pre-existing TensorFlow APIs, such as the object detection API that we will use for the final project, a TF Record format is required to train models.

#### Waymo Open Dataset vs. TensorFlow Object Detection API
- In the final project of this course, you will use data from the Waymo Open Dataset with the TensorFlow Object Detection API to perform object detection on camera images. While each use .tfrecord files, there is a difference in the structure of each. As such, the upcoming exercise will have you take a .tfrecord from the Waymo Open Dataset and convert it into a new .tfrecord useable by the TensorFlow Object Detection API.
- While also linked in the exercise itself, you'll need a few resources to be able to do so more easily.
 - First, [this repository](https://github.com/Jossome/Waymo-open-dataset-document) gives some additional information around the Waymo Open Dataset itself (note that Waymo link to [https://waymo.com/open/data/] therein now should be [https://waymo.com/open/data/perception], as Waymo has also added a "motion" component to the previous perception-only dataset).
 - Secondly, [this tutorial for the TF Object Detection API](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/training.html#create-tensorflow-records) for converting from .xml to .tfrecord also shows certain steps that will apply in our case as well.
 - This exercise will require some research on your own of the above documentation (and potentially other documentation) to reach a converted file; however, if you get stuck, it is perfectly reasonable to skip ahead to the solution video for some assistance.

#### Additional Resources
- [Using TFRecord and tf.train.Example from the TensorFlow documentation](tensorflow.org/tutorials/load_data/tfrecord)
- The above documentation will be useful to refer to as you work on the upcoming exercise.

#### 2021/01/17
### Model Selection
- Establishing **baselines** prior to building models will allow you to better assess your model's performances.
  - ML Engineers get very excited about creating new models. However, before diving into this step of the ML workflow, one must set realistic expectations, by setting up baselines.
- Baseline could be an **upper bound**
  - How a human would perform at this task?
  - An **upper bound baseline** gives you a sense of the maximum expected performance. If a client comes to you and asks for an algorithm that classifies images correctly 100% of the time, you can safely let them know that it won't happen. Human performance is a good upper bound baseline. For a classification problem, you should try to manually classify 100s of images to get an idea of what level of performance your algorithm could reach.
- Baseline could be an **lower bound**
  - If it were to randomly guess predictions, what would be the performance?
  - A **lower bound baseline** gives you an idea of a minimum expected performance. If you are getting metrics below such baseline, a red flag should be raised and should be concerned that something is wrong with your training pipeline. For example, for a classification problem, the random guess baseline is a good lower bound. Given C classes, the accuracy of your accuracy of your algorithm should be higher than 1/C.

- **Model selection is a dynamic part of the ML workflow**. It requires many iterations. Unless you have some prior knowledge of the task, it is recommended to start with simple models and iterate on complexity (For example, Random guess -> Linear/Logistic Regression -> Polynomial Regression -> Neural Networks). **Keep in mind that the validation set should remain the same during this phase!**

### Error Analysis
- Two great indicators of performances : **loss** and **accuracy** (or other metrics)
- Sorting images based on loss
- Find **patterns** in error
- **Understand metrics** value

- Validation set metrics are a good indicator of **global performances** of the model but we often need a finer understanding. A metric like accuracy won't tell you if a certain class of objects is always misclassified, for example. For these reasons, one must perform an in-depth error analysis before iterating on the model.

- Sorting predictions based on the metric or loss values is always a useful way to identify error patterns.

- Helpful question : Given that the training accuracy and the validation accuracy are similar and based on your observations, how would you improve your model?
  - The model may be underfitting. I would try to improve the model's complexity.
  - I would try to improve the size of the training set.
  - If the training dataset is missing examples of data that occurs in the validation set, you should try to increase its size.

### Lesson Conclusion
- The Machine Learning workflow is organized as follow:
  - **Frame the problem**: understand the stakes, and define relevant metrics.
  - **Understand the data**: perform an Exploratory Data Analysis, and extract patterns from the dataset.
  - **Iterate on the model**: create a validation set, set up baselines, and iterate on models from simpler to more complex.

- Glossary
  - Accuracy: classification metric.
  - Bias-Variance tradeoff: the challenges how creating a ML model that performs well while keeping an ability to generalize to new data.
  - Cross validation: set of techniques to evaluate a model
  - Domain gap: difference between dataset distributions.
  - Exploratory Data Analysis (EDA): the process of analyzing a new dataset and extracting any relevant informations to the ML problem.
  - Inference time: time taken by a model to output a prediction.
  - Overfitting: when a model has good performances on a dataset but does not generalize well
  - Precision: the number of correctly classified instances divided by the number of these instances.
  - Recall: the number of images classified correctly divided by the total number of images.
  - TfRecord: Tensorflow custom data format.
  - Training set: dataset used to train a ML model.
  - Validation set: dataset used to evaluate a ML model's performance.