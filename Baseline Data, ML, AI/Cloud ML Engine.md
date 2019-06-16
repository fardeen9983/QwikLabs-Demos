# Cloud ML Engine
Objective:

Deploy a [TensorFlow](http://tensorflow.org/) wide and deep model to CloudML. Uses Deep Neural Net and TensorFlow class "DNNCombinedLinearClassifier" 

Dataset used : [United States Census Income Dataset](https://archive.ics.uci.edu/ml/datasets/Census+Income)

Wide and deep models use deep neural nets (DNNs) to learn high-level abstractions about complex features or interactions between such features. These models then combine the outputs from the DNN with a linear regression performed on simpler features. This provides a balance between power and speed that is effective on many structured data problems.

Income Categories predicted : Less than and greater than $50,000

Tasks
* Create a TensorFlow training application and validate it locally.
* Run your training job on a single worker instance in the cloud.
* Run your training job as a distributed training job in the cloud.
* Optimize your hyperparameters by using hyperparameter tuning.
* Deploy a model to support prediction.
* Request an online prediction and see the response.
* Request a batch prediction.

Steps
1. Install Tensorflow on gcloud shell
    ```py
    pip install --user --upgrade tensorflow
    ```
2. Verify the installation
    ```py
    python -c "import tensorflow as tf; print('TensorFlow version {} is installed.'.format(tf.VERSION))"
    ```
3. Clone the [Cloud ML sample repo](https://github.com/GoogleCloudPlatform/cloudml-samples)
    ```py
    git clone https://github.com/GoogleCloudPlatform/cloudml-samples.git
    ```
4. Navigate to the said folder
    ```bash
    cd cloudml-samples/census/estimator
    ```
5. Create a new directory and store the relevant data files for the model
    ```bash
    mkdir data
    gsutil -m cp gs://cloud-samples-data/ml-engine/census/data/* data/
    ```
6. Now set local paths for the training and testing data files
    ```bash
    export TRAIN_DATA=$(pwd)/data/adult.data.csv
    export EVAL_DATA=$(pwd)/data/adult.test.csv
    ```
7. Open adult.data.csv file:
    ```bash
    head data/adult.data.csv
    ```
8. Install all the required dependencies from the requirements.txt file
    ```sh
    pip install --user -r ../requirements.txt
    ```
9. Run a local training job : 
    
    A local training job loads your Python training program and starts a training process in an environment that's similar to that of a live Cloud ML Engine cloud training job.

    Create an output directory and set the variable MODEL_DIR on it
    ```bash
    export MODEL_DIR=output
    ```

    Locally train the model:
    ```sh
    gcloud ai-platform local train \
    --module-name trainer.task \
    --package-path trainer/ \
    --job-dir $MODEL_DIR \
    -- \
    --train-files $TRAIN_DATA \
    --eval-files $EVAL_DATA \
    --train-steps 1000 \
    --eval-steps 100
    ```

    By default, verbose logging is turned off. You can enable it by setting the --verbosity tag to DEBUG. A later example shows you how to enable it.
10. Inspect the summary logs using Tensorboard:

    To see the evaluation results, you can use the visualization tool called [TensorBoard](https://www.tensorflow.org/programmers_guide/summaries_and_tensorboard). With TensorBoard, you can visualize your TensorFlow graph, plot quantitative metrics about the execution of your graph, and show additional data like images that pass through the graph. Tensorboard is available as part of the TensorFlow installation.

    * Launch TensorBoard:
        ```sh
        tensorboard --logdir=$MODEL_DIR --port=8080
        ```
    * Click on the Web Preview icon, then Preview on port 8080. A new tab will open with TensorBoard running.
    * Click on Accuracy to see graphical representations of how accuracy changes as your job progresses.
    * Type CTRL+C in Cloud Shell to shut down TensorBoard.
11. Running model prediction locally (in Cloud Shell)
    
    The " output/export/census " directory holds the model exported as a result of running training locally. List that directory to see the generated timestamp subdirectory:
    ```sh
    ls output/export/census/
    ```
    Use the timestamp in the command below to predict data
    ```sh
    gcloud ai-platform local predict --model-dir output/export/census/<timestamp> --json-instances ../test.json
    ```
    Output
    ```
    CLASS_IDS  CLASSES  LOGISTIC               LOGITS                 PROBABILITIES
    [0]        [u'0']   [0.08181176334619522]  [-2.4179813861846924]  [0.918188214302063, 0.08181176334619522]
    ```
    Where class 0 means income <= 50k and class 1 means income >50k.

    We used the trained model with data provided in the test.json file

Now its time to run the model on cloud
1. Set up some variables first
   ```sh
    PROJECT_ID=$(gcloud config list project --format "value(core.project)")
    BUCKET_NAME=${PROJECT_ID}-mlengine
    echo $BUCKET_NAME
    REGION=us-central1
   ```
2. Create new google storage bucket
    ```sh
    gsutil mb -l $REGION gs://$BUCKET_NAME
    ```
3. Upload the data and json files to the bucket
    ```sh
    gsutil cp -r data gs://$BUCKET_NAME/data
    gsutil cp ../test.json gs://$BUCKET_NAME/data/test.json
    ```
4. Set the variables to point to these files:
    ```sh
    TRAIN_DATA=gs://$BUCKET_NAME/data/adult.data.csv
    EVAL_DATA=gs://$BUCKET_NAME/data/adult.test.csv
    TEST_JSON=gs://$BUCKET_NAME/data/test.json
    ```
5. Run a single-instance trainer in the cloud
    
    * Select a name for the initial training run that distinguishes it from any subsequent training runs
        ```sh
        JOB_NAME=census_single_1
        ```
    * Specify a directory for output generated by Cloud ML Engine by setting an OUTPUT_PATH variable to include when requesting training and prediction jobs. The OUTPUT_PATH represents the fully qualified Cloud Storage location for model checkpoints, summaries, and exports
        ```sh
        OUTPUT_PATH=gs://$BUCKET_NAME/$JOB_NAME
        ```
    * Run the following command to submit a training job in the cloud that uses a single process. This time, set the --verbosity tag to DEBUG so that you can inspect the full logging output and retrieve accuracy, loss, and other metrics. The output also contains a number of other warning messages that you can ignore for the purposes of this sample:
        ```sh
        gcloud ai-platform jobs submit training $JOB_NAME \
        --job-dir $OUTPUT_PATH \
        --runtime-version 1.10 \
        --module-name trainer.task \
        --package-path trainer/ \
        --region $REGION \
        -- \
        --train-files $TRAIN_DATA \
        --eval-files $EVAL_DATA \
        --train-steps 1000 \
        --eval-steps 100 \
        --verbosity DEBUG
        ```
      You can monitor the progress of your training job by watching the logs on the command line:
        ```sh
        gcloud ai-platform jobs stream-logs $JOB_NAME
        ```
        Or monitor in the Console: ML Engine > Jobs.
1. In cloud training, outputs are produced in Cloud Storage. In this sample, outputs are saved to OUTPUT_PATH; to list them, run:
   ```sh
   gsutil ls -r $OUTPUT_PATH
   ```

### Deploy your model to support prediction
By deploying your trained model to Cloud ML Engine to serve online prediction requests, you get the benefit of scalable serving. This is useful if you expect your trained model to be hit with many prediction requests in a short period of time.

Steps:
1. Create a Cloud Ml engine model
    ```sh
    MODEL_NAME=census
    gcloud ai-platform models create $MODEL_NAME --regions=$REGION
    ```
2. Select the exported model to use, by looking up the full path of your exported trained model binaries.
   ```sh
   gsutil ls -r $OUTPUT_PATH/export
   ```
3. Copy timestamp and add it to the following command to set the environment variable MODEL_BINARIES to its value:
    ```sh
    MODEL_BINARIES=$OUTPUT_PATH/export/census/<timestamp>/
    ```
4. Run the following command to create a version v1 of your model:
    ```sh
    gcloud ai-platform versions create v1 \
    --model $MODEL_NAME \
    --origin $MODEL_BINARIES \
    --runtime-version 1.10
    ```
5. It may take several minutes to deploy your trained model. When done, you can see a list of your models using the models list command:
    ```sh
    gcloud ai-platform models list
    ```
6. Send an online prediction request to the deployed model
    ```sh
    gcloud ai-platform predict \
    --model $MODEL_NAME \
    --version v1 \
    --json-instances ../test.json
    ```
    The response includes the probabilities of each label (>50K and <=50K) based on the data entry in test.json, thus indicating whether the predicted income is greater than or less than 50,000 dollars

Next steps
* Sign up for the full [Coursera Course on Machine Learning](https://www.coursera.org/learn/serverless-machine-learning-gcp/).
* Learn more about [TensorFlow Wide & Deep](https://www.tensorflow.org/tutorials/wide_and_deep)
* You can read more about wide and deep models in the Google Research Blog post named [Wide & Deep Learning: Better Together with TensorFlow](https://ai.googleblog.com/2016/06/wide-deep-learning-better-together-with.html).
* Get your own version of [Tensorflow](https://www.tensorflow.org/install/).