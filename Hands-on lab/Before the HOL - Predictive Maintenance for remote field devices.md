![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/main/Media/ms-cloud-workshop.png 'Microsoft Cloud Workshops')

<div class="MCWHeader1">
Predictive Maintenance for remote field devices
</div>

<div class="MCWHeader2">
Before the hands-on lab setup guide
</div>

<div class="MCWHeader3">
February 2022
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2022 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Predictive Maintenance for remote field devices before the hands-on lab setup guide](#predictive-maintenance-for-remote-field-devices-before-the-hands-on-lab-setup-guide)
  - [Requirements](#requirements)
  - [Before the hands-on lab](#before-the-hands-on-lab)
    - [Task 1: Download the lab files](#task-1-download-the-lab-files)
    - [Task 2: Provision a resource group](#task-2-provision-a-resource-group)
    - [Task 3: Create an Azure Databricks service](#task-3-create-an-azure-databricks-service)
    - [Task 4: Create Azure Databricks cluster](#task-4-create-azure-databricks-cluster)
    - [Task 5: Import lab notebook into Azure Databricks](#task-5-import-lab-notebook-into-azure-databricks)
    - [Task 6: Create Azure Machine Learning service workspace](#task-6-create-azure-machine-learning-service-workspace)

<!-- /TOC -->

# Predictive Maintenance for remote field devices before the hands-on lab setup guide

## Requirements

1. Microsoft Azure subscription (non-Microsoft subscription, must be a pay-as-you subscription).
2. [.NET Core 3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1)
3. [Visual Studio Code](https://code.visualstudio.com/) version 1.39 or greater
4. [C# Visual Studio Code Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
5. [Azure Functions Core Tools version 2.x (using NPM or Chocolatey - see readme on GitHub repository)](https://github.com/Azure/azure-functions-core-tools)
6. [Azure Functions Visual Studio Code Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)
7. An Azure Databricks cluster running Databricks Runtime 10.3 or above.
8. [Node.js 8.0 or above.](https://nodejs.org)

## Before the hands-on lab

Duration: 60 minutes

In the Before the hands-on lab exercise, you will set up your environment for use in the rest of the hands-on lab. You should follow all the steps provided in the Before the hands-on lab section to prepare your environment **before attending** the hands-on lab. Failure to do so will significantly impact your ability to complete the lab within the time allowed.

> **Important**: Most Azure resources require unique names. Throughout this lab you will see the word “SUFFIX” as part of resource names. You should replace this with your Microsoft alias, initials, or another value to ensure the resource is uniquely named.

### Task 1: Download the lab files

Download the lab artifacts from GitHub.

1. In a web browser, navigate to the [Predictive Maintenance for remote field devices GitHub repo](https://github.com/microsoft/MCW-Predictive-Maintenance-for-remote-field-devices).

2. On the repo page, expand the **Code**, then select **Download ZIP**.

   ![Download .zip containing the repository](media/github-download-repo.png 'Download ZIP')

3. Unzip the contents to your root hard drive (i.e., `C:\`). This will create a folder on your root drive named `MCW-Predictive-Maintenance-for-remote-field-devices-main`.

### Task 2: Provision a resource group

In this task, you will create an Azure resource group for the resources used throughout this lab.

1. Log into the [Azure Portal](https://portal.azure.com).

2. On the top-left corner of the portal, select the menu icon to display the menu.

    ![The portal menu icon is displayed.](media/portal-menu-icon.png "Menu icon")

3. In the left-hand menu, select **Resource groups**.  On its context menu, select **Create**.

   ![Add Resource Group Menu](media/add-resource-group-menu.png 'Resource Group Menu')

4. Create a new resource group with the name **Fabrikam_Oil**, ensure the proper subscription and region nearest you are selected. Then select **Review + Create**.

   ![Create Resource Group](media/create-resource-group.png 'Resource Group')

5. On the Summary blade, select **Create** to provision your resource group.

### Task 3: Create an Azure Databricks service

Azure Databricks is used to train and deploy a machine learning model that predicts an oil pump failure, based on incoming telemetry.

1. Navigate to the [Azure portal](https://portal.azure.com).

2. Expand the left menu, and select **+ Create a resource**, type in "Azure Databricks" in the search field, then select **Azure Databricks** from the results.

   ![Azure Databricks is entered in the search field and Azure Databricks is selected.](media/azure-create-databricks-search.png 'Azure Databricks')

3. Select **Create** in the Azure Databricks details page.

4. Within the **Azure Databricks Service** form, complete the following:

   | Field                          | Value                                      |
   | ------------------------------ | ------------------------------------------ |
   | Subscription                   | _select the appropriate subscription_      |
   | Resource Group                 | _select use existing, then `Fabrikam_Oil`_ |
   | Workspace name                 | _globally unique name_                     |
   | Location                       | _select the location nearest to you_       |
   | Pricing tier                   | _select Standard_                          |

   ![The form fields are completed with the previously described settings.](media/azure-create-databricks.png 'Azure Databricks Service')

5. Select **Review + Create**. On the review screen, select **Create**.

### Task 4: Create Azure Databricks cluster

1. In the [Azure portal](https://portal.azure.com), open your Azure Databricks service you created in the previous task.

2. Select **Launch Workspace**. Azure Databricks will automatically sign you in through its Azure Active Directory integration.

   ![Launch Workspace](media/databricks-launch-workspace.png 'Launch Workspace')

3. Once in the workspace, select **Compute** in the left-hand menu, then select **Create Cluster**.

   ![Compute, then Create Cluster are highlighted.](media/databricks-clusters.png 'Clusters')

4. In the **New Cluster** form, specify the following configuration options:

   | Field                      | Value                                                                                        |
   | -------------------------- | -------------------------------------------------------------------------------------------- |
   | Cluster name               | _enter `lab`_                                                                                |
   | Cluster Mode               | _select `Standard`_                                                                          |
   | Pool                       | _select `None`_                                                                              |
   | Databricks Runtime Version | _select `Runtime: 10.3 (Scala 2.12, Spark 3.2.1)`_                                         |
   | Autopilot Options          | _uncheck `Enable autoscaling` and check `Terminate after...`, with a value of `120` minutes_ |
   | Worker Type                | _select `Standard_DS3_v2`_                                                                   |
   | Driver Type                | _select `Same as worker`_                                                                    |
   | Workers                    | _enter `1`_                                                                                  |

   ![The New Cluster form is displayed with the previously described values.](media/databricks-new-cluster.png 'New Cluster')

5. Select **Create Cluster**.

### Task 5: Import lab notebook into Azure Databricks

In this task, you will import a Databricks notebook into your workspace.

1. Within your Azure Databricks service, select **Workspace**, select **Users**, select the dropdown to the right of your username, then select **Import**.

   ![The Import link is highlighted in the Workspace.](media/databricks-import-link.png 'Workspace')

2. Keep **File** selected next to **Import from**, select or drag and drop the file `C:\MCW-Predictive-Maintenance-for-remote-field-devices-main\Hands-on lab\Resources\Notebooks\Anomaly Detection.ipynb`, then select **Import**.

   ![The file import form is displayed with the Anomaly Detection.ipynb file selected.](media/databricks-import.png 'Import Notebooks')

3. After importing the notebook, select **Workspace**, then select **Users**. Select your username. You will see a new notebook named `Anomaly Detection`.

   ![The imported notebooks are displayed.](media/databricks-notebooks.png 'Imported notebooks')

### Task 6: Create Azure Machine Learning service workspace

1. Navigate to the [Azure portal](https://portal.azure.com).

2. Select **+ Create a resource**, type in "machine learning" in the search field, then select **Machine Learning** from the results.

   ![Create a resource is highlighted and Machine Learning is selected.](media/azure-create-aml-search.png 'SQL Database')

3. Select **Create** in the Machine Learning details page.

4. Within the **Machine Learning** form, complete the following:

   | Field          | Value                                      |
   | -------------- | ------------------------------------------ |
   | Subscription   | _select the appropriate subscription_      |
   | Resource Group | _select `Fabrikam_Oil`_ |
   | Workspace name | _globally unique name_                     |
   | Region         | _select the region nearest to you_         |
   | Storage account | _keep the default_ |
   | Key vault       | _keep the default_ |
   | Application insights | _keep the default_ |
   | Container registry | _None_ |

   ![The form fields are completed with the previously described settings.](media/azure-create-aml.png 'Machine Learning service workspace')

5. Select **Review + Create**. On the review screen, select **Create**.

You should follow all steps provided _before_ performing the Hands-on lab.
