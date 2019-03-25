# FloydHub quick start project
[Website](http://www.floydhub.com) • [Docs](https://docs.floydhub.com) • [Forum](https://forum.floydhub.com) • [Twitter](https://twitter.com/floydhub_) • [We're Hiring](https://angel.co/floydhub) • [Write for FloydHub ✏️](https://blog.floydhub.com/write-for-floydhub)

This is the example model training project used in FloydHub's [quick start guide](http://docs.floydhub.com/getstarted/quick_start).

We will train a simple convolutional neural network (CNN) model to recognize handwritten digits using Tensorflow and the MNIST dataset. For more details on the data and the model, please refer to the [TensorFlow tutorial](https://www.tensorflow.org/get_started/mnist/pros).


### Quick Start Steps

1. Login your FloydHub account

    ```
    floyd login
    ```

2. Initialize the Project on Your locally Machine

    ```
    cd quick-start
    floyd init quick-start
    ```

3. Get the Dataset

    We have the MNIST dataset pulicly available on <https://www.floydhub.com/mckay/datasets/mnist/1>. When you start working on your own projects, you'll eventually want to upload your own dataset. 

4. Running Your First Job

    ```
    floyd run --cpu --data mckay/datasets/mnist/1:mnist --env tensorflow-1.3 "python train.py"
    ```

    Now you start a job named `your-name/projects/quick-start/1`.

5. Monitoring Your Job

    ```
    # show the status of all jobs in the current project
    floyd status
    # show the status of a single job
    flody status your-name/projects/quick-start/1
    ```

    You can also view status by URL: <https://www.floydhub.com/your-name/projects/quick-start/1>

6. Viewing Your Job's Logs

    ```
    floyd logs -t
    ```

    You can also view logs by URL: <https://www.floydhub.com/your-name/projects/quick-start/1>

7. Storing Your Model for Future Use

    We want to save the model we trained so we can use it later, maybe to iterate on it or to check its accuracy using an evaluation script.

    To save something during our job that we want to save for later, we just need to make sure it gets saved in the current working directory during our job.

8. Evaluate Your Model

    We need run second job to evaluate our model. FloydHub allows us to reuse a job's output in another job, and to specify the place the data will be located during the second job.

    ```
    floyd run --cpu --env tensorflow-1.3 --data mckay/datasets/mnist/1:mnist --data your-name/quick-start/1:model "python eval.py"
    ```

9. Iterating on Your Model

    At this point, you can edit your Python code locally to make improvements or adjustments to your training script, and then kick off a new job with the `floyd run` command. The floyd-cli will upload the newest versions of your code and submit another job to the FloydHub servers. Along the way, FloydHub will be managing and tracking of all the iterations of jobs within your project.

    You can always view details on all of the jobs in your current project with the floyd status command from your terminal, or by visiting the Project URL in your browser.

### Credits

The example code used here is derived from [aymericdamien/TensorFlow-Examples](https://github.com/aymericdamien/TensorFlow-Examples)