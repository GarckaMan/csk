# Create an ACK Pro cluster

Clusters of Container Service for Kubernetes \(ACK\) Pro are developed based on clusters of ACK Managed Edition. ACK Pro clusters provide higher reliability, security, and schedulability. ACK Pro clusters are covered by terms of service-level agreement \(SLA\) for customer compensation. ACK Pro clusters are suitable for enterprises that require higher security and stability for their large-scale business deployed in a production environment. This topic describes how to create an ACK Pro cluster in the ACK console.

Resource Access Management \(RAM\) is activated in the [RAM console](https://ram.console.aliyun.com/). Auto Scaling \(ESS\) is activated in the [ESS console](https://essnew.console.aliyun.com).

**Note:**

When you create a cluster of Container Service for Kubernetes \(ACK\), note the following limits:

-   SLB instances that are created together with the ACK cluster support only the pay-as-you-go billing method.
-   ACK clusters support only Virtual Private Cloud \(VPC\) networks.
-   Each account can consume only a limited amount of computing resources. You fail to create clusters if you do not have sufficient computing resources. When you create clusters, make sure that you have sufficient resources.
    -   For more information about the maximum numbers of clusters and nodes that can be created with each account, see [Quota limits on ACK](/intl.en-US/Product Introduction/Limits.md).

        **Note:** By default, you can add up to 48 route entries to each VPC network in an ACK cluster. This means that you can deploy up to 48 nodes in an ACK cluster that uses Flannel. An ACK cluster that uses Terway is not subject to this limit. To increase the quota of route entries for a VPC network, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

    -   You can create up to 100 security groups under each account.
    -   You can create up to 60 pay-as-you-go SLB instances under each account.
    -   You can create up to 20 elastic IP addresses \(EIPs\) under each account.

1.  Log on to the [ACK console](https://cs.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**.

3.  In the upper-right corner of the Clusters page, click **Create Kubernetes Cluster**. In the Select Cluster Template dialog box, find Professional Managed Cluster \(Preview\) and click **Create**.

4.  On the **ACK managed edition** tab, configure the cluster.

    1.  Configure basic settings of the cluster.

        |Parameter|Description|
        |---------|-----------|
        |**Cluster Name**|Enter a name for the cluster of Container Service for Kubernetes \(ACK\).

**Note:** The name must be 1 to 63 characters in length, and can contain digits, letters, and hyphens \(-\). |
        |**Cluster specifications**|Select a cluster type. **Standard edition** and **Professional \(Preview\)** are supported. |
        |**Region**|Select a region to deploy the cluster. |
        |**Resource Group**|Move the pointer over **All Resources** at the top of the page and select the resource group to which the cluster belongs. The name of the selected resource group appears on the page.

![Resource Groups](../images/p127165.png) |
        |**Kubernetes Version**|Select **1.14.8-aliyun.1** or **1.16.9-aliyun.1** for ACK Standard clusters. ACK Pro clusters support only **1.16.9-aliyun.1**.|
        |**Container Runtime**|**Docker** and **Sandboxed-Container** are supported. |
        |**VPC**|Select a Virtual Private Cloud \(VPC\) network to deploy the cluster. Shared VPC networks and standard VPC networks are supported.

        -   Shared VPC network: The owner of a VPC network \(resource owner\) can share VSwitches in the VPC network under the account of the owner with other accounts in the same organization.
        -   Standard VPC network: The owner of a VPC network \(resource owner\) cannot share VSwitches in the VPC network under the account of the owner with other accounts.
**Note:** ACK clusters support only VPC networks. You can select a VPC network from the drop-down list. If no VPC network is available, click **Create VPC** to create one. For more information, see [Create a VPC](/intl.en-US/VPCs and VSwitches/VPC management/Create a VPC.md). |
        |**VSwitch**|Select VSwitches. |
        |**Network Plug-in**|Select a network plug-in. Both Flannel and Terway are supported. For more information, see [Flannel and Terway](/intl.en-US/User Guide for Kubernetes Clusters/Network management/Use Terway.md).

        -   Flannel: a simple and stable Container Network Interface \(CNI\) plug-in developed by the Kubernetes community. Flannel offers a few simple features and does not support standard Kubernetes network policies.
        -   Terway: a network plug-in developed by ACK. Terway allows you to assign Alibaba Cloud elastic network interfaces \(ENIs\) to containers. It also allows you to customize Kubernetes network policies to control intercommunication among containers, and implement bandwidth throttling on individual containers.

**Note:**

            -   The number of pods that can be deployed on a node depends on the number of ENIs that are attached to the node and the maximum number of secondary IP addresses provided by these ENIs.
            -   If you select a shared VPC network for a cluster, you must select the Terway network plug-in.
            -   If you select **Terway**, an ENI is shared among multiple pods. A secondary IP address of the ENI is assigned to each pod. |
        |**Pod CIDR Block**|If you select **Flannel**, you must set **Pod CIDR Block**.

The CIDR block specified by **Pod CIDR Block** cannot overlap with that of the VPC network or existing ACK clusters in the VPC network. The CIDR Block cannot be modified after it is specified. The Service CIDR block cannot overlap with the Pod CIDR block. For more information about subnetting for ACK clusters, see [Assign CIDR blocks to resources in a Kubernetes cluster under a VPC](/intl.en-US/User Guide for Kubernetes Clusters/Network management/Assign CIDR blocks to resources in a Kubernetes cluster under a VPC.md). |
        |**Terway Mode**|If you select **Terway**, you must set **Terway Mode**.

Select or clear **Assign One ENI to Each Pod**.

        -   If you select the check box, an ENI is assigned to each pod.
        -   If you clear the check box, an ENI is shared among multiple pods. A secondary IP address provided by the ENI is assigned to each pod.
Select or clear **IPVLAN**.

        -   This option is available only when you clear Assign One ENI to Each Pod.
        -   If you select IPVLAN, IPVLAN and the extended Berkeley Packet Filter \(eBPF\) are used for network virtualization when an ENI is shared among multiple pods. This improves network performance. Only the Alibaba Cloud Linux 2 operating system is supported.
        -   If you clear IPVLAN, policy-based routes are used for network virtualization when an ENI is shared among multiple pods. The CentOS 7 and Alibaba Cloud Linux 2 operating systems are supported. This is the default setting.
**Note:** The preceding two features are available to only users in the whitelist.To use this feature, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm). |
        |**Service CIDR**|Set **Service CIDR**. The CIDR block specified by **Service CIDR** cannot overlap with that of the VPC network or existing ACK clusters in the VPC network. The CIDR block cannot be modified after it is specified. The Service CIDR block cannot overlap with the Pod CIDR block. For more information about subnetting for ACK clusters, see [Assign CIDR blocks to resources in a Kubernetes cluster under a VPC](/intl.en-US/User Guide for Kubernetes Clusters/Network management/Assign CIDR blocks to resources in a Kubernetes cluster under a VPC.md). |
        |**IP Addresses per Node**|If you select **Flannel**, you must set the number of **IP addresses per node**.

**Note:** **IP Addresses per Node** specifies the maximum number of IP addresses that can be assigned to each node. We recommend that you use the default value. |
        |**Configure SNAT**|By default, a cluster is not accessible over the Internet. If the VPC network that you select for the cluster cannot access the Internet, you can select **Configure SNAT for VPC**. Then, ACK creates a Network Address Translation \(NAT\) gateway and configures Source Network Address Translation \(SNAT\) entries to enable Internet access for the VPC network. |
        |**Public Access**|Specify whether to **expose the API server with an elastic IP address \(EIP\)**.

The ACK API server provides multiple HTTP-based RESTful APIs, which can be used to create, delete, modify, query, and monitor resources such as pods and Services.

        -   If you select this check box, an EIP is created and attached to an internal Server Load Balancer \(SLB\) instance. Port 6443 used by the API server is opened on master nodes. You can connect to and manage the cluster by using kubeconfig over the Internet.
        -   If you clear this check box, no EIP is created. You can connect to and manage the cluster only by using kubeconfig from within the VPC network. |
        |**RDS Whitelist**|Set the Relational Database Service \(RDS\) whitelist. Add the IP addresses of cluster nodes to the RDS whitelist.

**Note:** To enable an RDS instance to access an ACK cluster, you must deploy the RDS instance in the same VPC network as the ACK cluster. |
        |**Security Group**|You can select **Create Basic Security Group**, **Create Advanced Security Group**, and **Select Existing Security Group**. For more information, see [Overview](/intl.en-US/Security/Security groups/Overview.md). |
        |**Secret Encryption**|If you select **Select Key**, you can use a key created in the Key Management Service \(KMS\) console to encrypt Kubernetes Secrets. For more information, see [Use KMS to encrypt Kubernetes Secrets](/intl.en-US/User Guide for Kubernetes Clusters/Security management/Use KMS to encrypt Kubernetes Secrets.md).|

    2.  Configure advanced settings of the cluster.

        |Parameter|Description|
        |---------|-----------|
        |**Kube-proxy Mode**|IPVS and iptables are supported.

        -   iptables is a kube-proxy mode. It uses iptables rules to conduct service discovery and load balancing. The performance of this mode is restricted by the size of the cluster. This mode is suitable for clusters that run a small number of Services.
        -   IPVS is a high-performance kube-proxy mode. It uses Linux Virtual Server \(LVS\) to conduct service discovery and load balancing. This mode is suitable for clusters that run a large number of Services. We recommend that you use this mode in scenarios where high-performance load balancing is required. |
        |**Labels**|Attach labels to nodes. Enter keys and values, and then click **Add**.

**Note:**

        -   Key is required. Value is optional.
        -   Keys are not case-sensitive. A key must be 1 to 64 characters in length, and cannot start with aliyun, http://, or https://.
        -   Values are not case-sensitive. A value must be 1 to 128 characters in length, and cannot start with http:// or https://.
        -   The keys of labels that are attached to the same resource must be unique. If you add a label with a used key, the label overwrites the one using the same key.
        -   You can attach up to 20 labels to each resource. If you attach more than 20 labels to a resource, all labels become invalid. You must detach unused labels for the remaining labels to take effect. |
        |**Cluster Domain**|Set the cluster domain.

**Note:** The default cluster domain is **cluster.local**. You can enter a custom domain. A domain consists of two parts. Each part must be 1 to 63 characters in length, and can contain only letters and digits. |
        |**Custom Certificate SANs**|You can enter custom subject alternative names \(SANs\) for the API server of the cluster to accept requests from specified IP addresses or domains. |
        |**Service Account Token Volume Projection**|**Service account token volume projection** reduces security risks when pods use service accounts to access the API server. This feature enables kubelet to request and store the token on behalf of the pod. This feature also allows you to configure token properties, such as the audience and validity duration. For more information, see [Deploy service account token volume projection](/intl.en-US/User Guide for Kubernetes Clusters/Security management/Use service account token volume projection.md). |
        |**Deletion Protection**|Specify whether to enable deletion protection. If you select this check box, the cluster cannot be deleted in the console or by calling the API. This allows you to avoid user errors. |

5.  Click **Next:Worker Configurations** to configure worker nodes.

    1.  Set **worker instances**.

        -   If you select **Create Instance**, you must set the parameters that are listed in the following table.

            |Parameter|Description|
            |---------|-----------|
            |**Billing Method**|The **pay-as-you-go** and **subscription** billing methods are supported. If you select **pay-as-you-go**, you must set the following parameters:

            -   **Duration**: You can select 1, 2, 3, or 6 months. If you require a longer duration, you can select 1 to 5 years.
            -   **Auto Renewal**: Specify whether to enable auto-renewal. |
            |**Instance Type**|You can select multiple instance types. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md). |
            |**Selected Types**|The selected instance types are displayed. |
            |**Quantity**|Specify the number of worker nodes to be created. |
            |**System Disk**|**ESSDs**, **SSDs**, and **ultra disks** are supported.

**Note:** You can select **Enable Backup** to back up disk data. |
            |**Mount Data Disk**|**ESSDs**, **SSDs**, and **ultra disks** are supported. You can enable disk **encryption** and **backup** when you add data disks. |
            |**Operating System**|The CentOS and Alibaba Cloud Linux operating systems are supported. |
            | | |
            | |

        -   If you select **Add Existing Instance**, you must select ECS instances that are deployed in the region where the cluster is deployed. Then, set **Operating System**, **Logon Type**, and **Key Pair** based on the preceding settings.
    2.  Configure advanced settings of worker nodes.

        |Parameter|Description|
        |---------|-----------|
        |**Node Protection**|Specify whether to enable node protection.

**Note:** By default, this check box is selected. This way, cluster nodes cannot be deleted in the console or by calling the API. This allows you to avoid user errors. |
        |**User Data**|For more information, see [Prepare user data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md). |
        |**Custom Image**|You can select a custom image, and then use the image to deploy all nodes in the cluster. For more information about how to create a custom image, see [Create a Kubernetes cluster by using a custom image](/intl.en-US/Best Practices/Cluster/Create a Kubernetes cluster by using a custom image.md).

**Note:** This feature is available to only users in the whitelist. If you are not in the whitelist, [submit a ticket](https://selfservice.console.aliyun.com/ticket/scene/ecs/%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20ECS/detail). |
        |**Custom Node Name**|Specify whether to use a **custom node name**.

A node name consists of a prefix, an IP substring, and a suffix.

        -   Both the prefix and suffix can contain one or more parts that are separated with periods \(**.**\) and must start and end with a lowercase letter or digit. These parts can contain lowercase letters, digits, and hyphens \(-\), and must start and end with a lowercase letter or digit.
        -   The IP substring length specifies the number of digits to be truncated from the end of the returned node IP address. Valid values: 5 to 12.
For example, if the node IP address is 192.1xx.x.xx, the prefix is aliyun.com, the IP substring length is 5, and the suffix is test, the node name will be aliyun.com00055test. |
        |**CPU Policy**|Set the CPU policy.

        -   none: This policy indicates that the default CPU affinity is used. This is the default policy.
        -   static: This policy allows pods with certain resource characteristics on the node to be granted with enhanced CPU affinity and exclusivity. |
        |**Taints**|Add taints to worker nodes in the cluster. |

6.  Click **Next:Component Configurations** to configure components.

    |Parameter|Description|
    |---------|-----------|
    |**Ingress**|Specify whether to install Ingress controllers. By default, **Install Ingress Controllers** is selected. For more information, see [Configure an Ingress](/intl.en-US/User Guide for Kubernetes Clusters/Network management/Ingress management/Configure an Ingress.md). |
    |**Volume Plug-in**|Select a volume plug-in. Flexvolume and CSI are supported. ACK clusters can be automatically bound to cloud disks of Alibaba Cloud, Network Attached Storage \(NAS\) volumes, and Object Storage Service \(OSS\) volumes that are mounted to pods. For more information, see [Storage management-Flexvolume](/intl.en-US/User Guide for Kubernetes Clusters/Storage management-Flexvolume/Overview.md) and [Storage management-CSI](/intl.en-US/User Guide for Kubernetes Clusters/Storage management-CSI/Overview.md). |
    |**Monitoring Agents**|Specify whether to install the Cloud Monitor agent. By default, **Install CloudMonitor Agent on ECS Instance** and **Enable Prometheus Monitoring** are selected. After the Cloud Monitor agent is installed on ECS nodes, you can view monitoring information about the nodes in the Cloud Monitor console. |
    |**Log Service**|Specify whether to activate Log Service. You can select an existing Log Service project or create a Log Service project.

By default, **Enable Log Service** is selected. When you create an application, you can activate Log Service through a few steps. For more information, see [Use Log Service to collect container logs](/intl.en-US/User Guide for Kubernetes Clusters/Log management/Use Log Service to collect container logs.md).

By default, **Install node-problem-detector and Create Event Center** is selected. You can also specify whether to **create Ingress dashboard** in the Log Service console. |
    |**Workflow Engine**|Specify whether to activate Alibaba Cloud Genomics Compute Service \(AGS\).

    -   If you select this check box, the system automatically installs the AGS workflow plug-in when it creates the cluster.
    -   If you clear this check box, you must manually install the AGS workflow plug-in. For more information, see [Introduction to AGS CLI](/intl.en-US/User Guide for Genomics Service/AGS workflow/Introduction to AGS CLI.md). |

7.  Click **Next:Confirm Order**.

8.  Read and select **Terms of Service**, and then click **Create Cluster**.

    **Note:** It takes about 10 minutes to create an ACK cluster that contains multiple nodes.


-   After the cluster is created, you can find the cluster on the Clusters page in the console.
-   Click **View Logs** in the **Actions** column. On the Log Information page, you can view cluster logs. To view detailed log information, click **Stack events**.

-   Click **Details** in the **Actions** column. On the details page, click the **Basic Information** tab to view the basic information about the cluster and click the **Connection Information** tab to view the connections to the cluster.

