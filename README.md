# Logz.io AWS ECS Collector

This integration uses Fluentd in a Docker container to forward logs from your Amazon Elastic Container Service (ECS) cluster to Logz.io.

**Note** that this repo refers to an EC2 based cluster. For Fargate based cluster see [this](https://docs.logz.io/shipping/log-sources/fargate.html).

You can deploy this integration in two ways:
* Manual deployment (Classic Console).
* Cloudformation deployment.

## Manual deployment

### 1. Download the task definition JSON

Download the task definition JSON file:

```shell
wget https://raw.githubusercontent.com/logzio/logzio-aws-ecs/master/task-definition.json
```

### 2. Configure the task

In your prefered text editor, open the JSON you downloaded in the previous step and replace the following:

| Paramater | Details |
|---|---|
| `<<LOG-SHIPPING-TOKEN>>` | **Required**. Your Logz.io account token. Replace with the [token](https://app.logz.io/#/dashboard/settings/general) of the account you want to ship to. |
| `<<LISTENER-HOST>>` | **Required**. Your Logz.io listener URL. Replace with your region's listener URL.|


### 3. Advanced settings (optional)

Since the docker image is based on Logz.io's [fluentd-docker-logs](https://github.com/logzio/fluentd-docker-logs) image, any of the environment variable mentioned [here](https://github.com/logzio/fluentd-docker-logs#parameters) can be added to the task definition JSON.


### 4. Add your task definition

1. In your [Amazon ECS Classic Console](https://console.aws.amazon.com/ecs/) menu go to **Task Definitions** and click on **Create new Task Definition**.

2. In the **Step 1: Select launch type compatibility** screen choose **EC2** and click **Next step**.

3. In the **Step 2: Configure task and container definitions** screen, scroll down and click on the **Configure via JSON** button.

4. In the test-box that opened, delete the existing text, and paste your configured task definition JSON. Press **Save**, then press **Create**.

### 5. Run the task

1. After the task was created, click on the **Actions** button, then choose **Run Task**.

2. In the **Run Task** screen, choose **EC2** as your **Launch type**.

3. In the **Run Task** screen, choose the cluster you want to ship logs from.

4. Click on **Run Task**.

### 6. Check Logz.io for your logs

Give your logs some time to get from your system to ours, and then open [Kibana](https://app.logz.io/#/dashboard/kibana).
