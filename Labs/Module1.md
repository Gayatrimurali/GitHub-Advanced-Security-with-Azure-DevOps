# Lab 01: Configure GHAzDO in Azure DevOps

## Lab Scenario

In this lab, we configure GitHub Advanced Security (GHAS) within Azure DevOps, enabling enhanced security measures and permissions for the eShopOnWeb project. We set up billing, activate Advanced Security, and establish permissions for managing security alerts.

## Lab Objectives

In this lab, you will perform:
- Task 1: Sign up and configure the eShopOnWeb team project in Azure DevOps
- Task 2: Enable Advanced Security from portal
- Task 3: Setup Advanced Security permissions

## Estimated Timing: 45 minutes

## Architecture Diagram

  ![AD](media/ard01.png)

### Task 1: Sign up and configure the eShopOnWeb team project in Azure DevOps

1. Open the **Edge browser**, and navigate to **Azure DevOps** using the link below. Select **Start Free**, and sign in with the credentials provided in the Environment variables.

   ```
    https://dev.azure.com
   ```
      ![setup](media/lab1-image1.png)

1. On the **Get Started with Azure DevOps** page, click on **Continue**.

      ![setup](media/end2.png)

1. On the **Almost done** page, enter the **captcha** and click on **Continue**.

      ![setup](media/end1.png)

1. On the **Azure DevOps** page, at the button left, click on **Organization settings**. then select **Billing** (opening this screen takes a few seconds).

    ![](media/nls2.png)

1. From the left navigation pane, select **Billing** and click **Set up billing**. On the right-hand side of the screen, select the **Existing subscription** listed and click **Save** to link the subscription with the organization.

   ![](media/lab1-image8.png)

   ![](media/lab1-image9.png)

1. Once the screen shows the linked Azure Subscription ID at the top, change the number of **Paid parallel jobs** for **MS Hosted CI/CD** from 0 to **1**. Then click the **SAVE** button at the bottom.

   ![](media/lab1-image10.png)

1. On the **Organization Settings** page, navigate to the **Security** section and click **Policies**. Turn on the **Toggle** for **Third-party application access via OAuth**.

     ![](media/nls1.png)
   
      > **Note:** The OAuth setting helps enable tools such as the DemoDevOpsGenerator to register extensions. Without this, several labs may fail due to a lack of the required extensions.

1. Toggle the switch to **On** for **Allow public projects** and click on **Save** when the **change policy setting** is prompted.

     > **Note:** Extensions used in some labs might require a public project to allow using the free version.

1. Navigate to **azuredevopsdemogenerator** using the link below. This utility site will automate the process of creating a new Azure DevOps project within your account that is prepopulated with content (work items, repos, etc.) required for the lab. For more information on the site, please see [https://docs.microsoft.com/en-us/azure/devops/demo-gen](https://docs.microsoft.com/en-us/azure/devops/demo-gen).

   ```
   https://azuredevopsdemogenerator.azurewebsites.net/
   ```
  
1. Click on **Sign in** and log in using the Microsoft account associated with your Azure DevOps subscription.

    ![](media/lab1-image2.png)

1. Please click on **Accept** to grant permission to access your subscription.

1. Click **Choose Template**.

    ![](media/lab1-image3.png)

1. Select the **eShopOnWeb** template and click on **Select Template**.

    ![](media/lab1-image4.png)

1. Provide a project name, **eShopOnWeb**, and choose your **Organization**, then click on **Create Project** and wait for the process to complete.

   ![](media/lab1-image5.png)

1. Once the process is complete, click on **Navigate to the project**.

   ![](media/lab1-image6.png)

      > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
      > - Click the Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation Page.
      > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
      > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
      > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="719b12ff-b146-4cc6-b0e3-b834f797d9b1" />

### Task 2: Enable Advanced Security from Portal

GitHub Advanced Security for Azure DevOps includes extra permissions for more levels of control around Advanced Security results and management. Be sure to adjust individual permissions for your repository.

To ensure Azure DevOps Advanced Security is enabled in your organization, you can follow these steps:

1. Open the **eShopOnWeb** project and click on **Project Settings** available in the lower left corner. In the left menu area under Repos, click **Repositories**.

1. Click on the **eShopOnWeb** repository.

1. Click on **Settings**, then click on **Advanced Security**, to turn it on.

    ![setup](media/last2.png)

1. Click **Begin Billing**.

    ![](media/lab1-image12.png)

1. Advanced Security and Push Protection are now enabled. You can also onboard Advanced Security at [Project-level](https://learn.microsoft.com/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&tabs=yaml#project-level-onboarding) and [Organization-level](https://learn.microsoft.com/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&tabs=yaml#organization-level-onboarding) as well.
 
### Task 3: Setup Advanced Security permissions

In this task, you will configure advanced security permissions for the eShopOnWeb repository in Azure DevOps. This involves granting specific permissions to project administrators to manage security alerts and settings related to the repository.

1. In the lower-left corner, click on **Project Settings**. In the left menu area under the **Repos** section, click **Repositories**.

      ![](media/lab1-image13.png)
  	
1. Click on the **eShopOnWeb** repository.

1. Select **Security** and click on **Project Administrators**.

1. Next to Advanced Security: manage and dismiss alerts, click the **dropdown**, and select  **Allow**.

1. Next to Advanced Security: manage settings, click the **dropdown**, and select **Allow**.

1. Next to Advanced Security: view alerts, click the dropdown, and select **Allow**.

      ![allow-permissions](media/last1.png)

1. Make sure a green checkmark ✅ appears next to the selected permission.

## Create Work item

You can follow these steps to create a work item to link while committing the changes.

1. Navigate to the **eShopOnWeb** project and select **Boards** from the left menu and select **Work items**

      ![allow-permissions](media/nls3.png)

1. On the **Work items** page, select **+New Work Item** and select **Issue** from the drop-down menu.

      ![allow-permissions](media/nls5.png)

1. Enter **Advanced security related events** in the Title box

1. Enter **Work item to link for all the commits related to Advanced security events** in the description box and click on **Save**

      ![allow-permissions](media/nls4.png)

## Install extension

You can follow these steps to install an extension which is needed in upcoming tasks.

1. Select the **Marketplace** icon from the top right corner and select **Browse marketplace** from the list

      ![allow-permissions](media/ext1.png)

1. On the **Marketplace** window, under **Azure DevOps** search and select **replace tokens**

      ![allow-permissions](media/ext2.png)

1. Select **Get it free**

      ![allow-permissions](media/ext3.png)

1. Select **Install**

      ![allow-permissions](media/ext4.png)

1. Select **Proceed to Organization** to navigate back to **Azure DevOps**

      ![allow-permissions](media/ext5.png)

Please feel free to go through the documentation for further understanding: [GitHub Advanced Security for Azure DevOps](https://azure.microsoft.com/en-us/products/devops/github-advanced-security) and [Configure GitHub Advanced Security for Azure DevOps](https://learn.microsoft.com/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&tabs=yaml)

## Review
In this lab, you have completed the following:

- Configured the eShopOnWeb team project.
- Enabled Advanced Security from the Portal.
- Set up Advanced Security permissions.

Click on **Next** to proceed with the next lab.
