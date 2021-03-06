---
keyword: [Knative system components, alert, Prometheus Monitoring]
---

# Use ARMS Prometheus Monitoring to monitor Knative system components and configure alerts

You can configure monitoring metrics for Knative system components by using Prometheus Monitoring in Application Real-Time Monitoring Service \(ARMS\). This topic describes how to monitor Knative system components and configure alerts.

The following metrics of Knative system components are collected:

-   Number of ready pods where the components are deployed.
-   CPU usage of the pods where the components are deployed.
-   Memory usage of the pods where the components are deployed.

Knative system components include:

-   knative-serving
    -   activator
    -   autoscaler
    -   autoscaler-hpa
    -   controller
    -   istio-webhook
    -   networking-istio
    -   webhook
-   knative-eventing
    -   eventing-controller
    -   eventing-webhook

## Step 1: Install the Prometheus Monitoring component

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Marketplace** \> **App Catalog**.

3.  On the App Catalog page, click the **Alibaba Cloud Apps** tab and click **ack-arms-prometheus**.

4.  On the App Catalog - ack-arms-prometheus page, click the **Parameters** tab.

5.  On the **Parameters** tab, set parameter cluster\_id.

    **Note:**

    The system automatically sets the value to the ID of the target cluster. To find the cluster ID, choose **Clusters** \> **Clusters** in the left-side navigation pane, find the target cluster on the **Clusters** page, and the cluster ID is displayed in the Cluster Name/ID column.

6.  On the App Catalog - ack-arms-prometheus page, go to the **Deploy** tab on the right, select the target cluster, and click **Create**.

    ![arms](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4165359951/p97042.png)

    **Note:** **Namespace** and **Release Name** are set to **arms-prom** by default.


## Step 2: View pod monitoring information

Before you set an alert policy for a pod where the components are deployed, check the monitoring information about the pod.

1.  LogonLog on to the [ARMS console](https://arms-intl.console.aliyun.com/).

2.  In the left-side navigation pane, click **Prometheus Monitoring**.

3.  On the Prometheus Monitoring page, click **k8s state** in the **Installed Plugins** column. On the page that appears, you can view the number, CPU usage, and memory usage of the pods.


## Step 3: Set alarm policies for Knative system components



1.  You can select one of the two available methods to access the Create Alert page.

    -   On the New DashBoard page of the [ARMS Prometheus Grafana dashboard](http://grafana.console.aliyun.com/), click the icon to go to the ARMS Prometheus Create Alert dialog box.
    -   In the left-side navigation pane of the console, choose **Alerts** \> **Alert Policies**. On the Alert Policies page, choose **Create Alert** \> **Prometheus** in the upper-right corner.
2.  In the Create Alarm dialog box, set the parameters.

    The activator component of Knative Serving is used in this example. If the number of ready pods is less than the configured number, an alert is triggered. In this case, the number of unavailable pods is greater than or equal to one. The following figure shows the alert policy.

    ![Alarm policy](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/1065359951/p128009.png)

    The following shows PromQL of the activator component:

    ```
    ((sum(kube_deployment_status_replicas{deployment=~"activator"}) or vector(0))) - ((sum(kube_deployment_status_replicas_available{deployment=~"activator"}) or vector(0)))
    ```

    For more information, see [Create an alert](/intl.en-US/Dashboard and alarm/Create an alert.md).

3.  Click **Save**.


