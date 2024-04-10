# Lab 01: Configure GHAzDO in Azure DevOps

## Lab Scenario

In this lab, we configure GitHub Advanced Security (GHAS) within Azure DevOps, enabling enhanced security measures and permissions for the eShopOnWeb project. we set up billing, activate Advanced Security, and establish permissions for managing security alerts.

## Lab Objectives
In this lab, you will perform:
- Task 1: Sign up and configure the eShopOnWeb team project in Azure DevOps
- Task 2: Enable Advanced Security from Portal
- Task 3: Setup Advanced Security permissions

## Estimated Timing :45 minutes

### Task 1: Sign up and configure the eShopOnWeb team project in Azure DevOps

1. Open Edge browser and navigate to https://dev.azure.com and select **Start Free** and sign in with the credentials provided in the Environment variables.

      ![setup](media/lab1-image1.png)

1. On **Get Started with Azure DevOps** page, ensure that Project visibility is set to **Private** and enter the provided **captcha** click on **Continue**.

      ![setup](media/end2.png)

1. On the **Almost done** page, enter the **captcha** and click on **Continue**

      ![setup](media/end1.png)

1. Navigate to [https://azuredevopsdemogenerator.azurewebsites.net](https://azuredevopsdemogenerator.azurewebsites.net/). This utility site will automate the process of creating a new Azure DevOps project within your account that is prepopulated with content (work items, repos, etc.) required for the lab. For more information on the site, please see [https://docs.microsoft.com/en-us/azure/devops/demo-gen](https://docs.microsoft.com/en-us/azure/devops/demo-gen).

1. Click on **Sign in** and log in using the Microsoft account associated with your Azure DevOps subscription.

    ![](media/lab1-image2.png)

1. Please click on **Accept** to grant permission for accessing your subscription.

1. Click **Choose Template**.

    ![](media/lab1-image3.png)

1. Select the **eShopOnWeb** template and click **Select Template**.

    ![](media/lab1-image4.png)

1. Provide a project name **eShopOnWeb** and choose your **Organization** then click **Create Project** and wait for the process to complete.

   ![](media/lab1-image5.png)

1. Once proccess complete click on **Navigate to project**

   ![](media/lab1-image6.png)

### Task 2: Enable Advanced Security from Portal

GitHub Advanced Security for Azure DevOps includes extra permissions for more levels of control around Advanced Security results and management. Be sure to adjust individual permissions for your repository.

To ensure Azure DevOps Advanced Security is enabled in your organization, you can follow these steps:

1. On the **Azure DevOps** page at button left click on **Organization settings** then select **Billing** (opening this screen takes a few seconds).

    ![](media/lab1-image7.png)

1. From the left navigation pane select **Billing** and click **Set up billing** and on the right-hand side of the screen select the **Existing subscription** listed and click **Save** to link the subscription with the organization.

   ![](media/lab1-image8.png)

   ![](media/lab1-image9.png)

1. Once the screen shows the linked Azure Subscription ID at the top, change the number of **Paid parallel jobs** for **MS Hosted CI/CD** from 0 to **1**. Then click the **SAVE** button at the bottom.

   ![](media/lab1-image10.png)

1. In **Organization Settings** page, navigate to **Security** section and click **Policies**. Turn on the **Toggle** for **Third-party application access via OAuth**

     ![](media/lab1-image11.png)
   
      > **Note:** The OAuth setting helps enable tools such as the DemoDevOpsGenerator to register extensions. Without this, several labs may fail due to a lack of the required extensions.

1. Toggle the switch to **On** for **Allow public projects** and click on **Save** when **change policy setting** prompted.

     > **Note:** Extensions used in some labs might require a public project to allow using the free version.

1. Open the **eShopOnWeb** project and click on **Project Settings** available in the lower left corner. In the left menu area under Repos, click **Repositories**.

1. Click on the **eShopOnWeb** repository.

1. Click on Settings, then click **Advanced Security**, On to turn it on.

    ![setup](media/last2.png)

1. Click **Begin Billing**.

    ![](media/lab1-image12.png)

1. Advanced Security and Push Protection are now enabled. You can also onboard Advanced Security at [Project-level](https://learn.microsoft.com/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&tabs=yaml#project-level-onboarding) and [Organization-level](https://learn.microsoft.com/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&tabs=yaml#organization-level-onboarding) as well
 
    {% include note.html content= "GitHub Advanced Security for Azure DevOps includes extra permissions for more levels of control around Advanced Security results and management. Be sure to adjust individual permissions for your repository." %}

### Task 3: Setup Advanced Security permissions

In this task, you will configure Advanced Security permissions for the eShopOnWeb repository in Azure DevOps. This involves granting specific permissions to Project Administrators to manage security alerts and settings related to the repository.

1. In the lower-left corner, click on **Project Settings**. In the left menu area under **Repos** section, click **Repositories**.

      ![](media/lab1-image13.png)
  	
1. Click on the **eShopOnWeb** repository.

1. Select **Security** and click on **Project Administrators**.

1. Next to Advanced Security: manage and dismiss alerts, click the dropdown and select  **Allow**.

1. Next to Advanced Security: manage settings, click the dropdown and select **Allow**.

1. Next to Advanced Security: view alerts, click the dropdown and select **Allow**.

      ![allow-permissions](media/last1.png)

1. Make sure successful, a green checkmark ✅ appears next to the selected permission.
  
## Review
In this lab you have completed the following:

- Configured the eShopOnWeb team project
- Enabled Advanced Security from Portal
- Setup Advanced Security permissions

Click **Next** to proceed with the next lab.
