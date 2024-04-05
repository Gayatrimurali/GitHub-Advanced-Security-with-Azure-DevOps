## Lab 01: Configure GHASDO in Azure DevOps

### Task 1: Configuring the eShopOnWeb team project

1. Open Edge browser and navigate to https://dev.azure.com and select **Start Free** and sign in with the credentials provided in the Environment variables.

      ![setup](media/lab1-image1.png)

1. On **Get Started with Azure DevOps** page, ensure that Project visibility is set to **Private** and enter the provided **captcha** click on **Continue**.

      ![setup](media/last99.png)

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

### Task 2: Configure the approvals and checks in environments

Once you provision the project follow the below steps to configure the approvals and checks

1. Navigate to **Pipelines** section and select **Environments**

    ![](media/select_environment.png)

1. Select **Production** environment

    ![](media/navigate_production.png)

1. Navigate to **Approvals and checks** and select **Approvals**
    
    ![](media/add_approvals.png)

1. Choose **<inject key="AzureAdUserEmail"></inject>** as a approver and click on create

    ![](media/choose_approver.png)

1. To select additional checks, click on **+ Add new** button

    ![](media/add_additiona_checks.png)

1. Select **Required tempalte** and click on Next

    ![](media/choose_require_tempalte.png)

1. Click on + button to add tempalte

    ![](media/required_tempalte.png)

1. Input the values in the Required YAML template fields and click on **Add required template** button

    - Choose **Azure Repos** radio button
    - Repository: **eShoponweb**
    - Ref: **refs/heads/main**
    - Path to required YAML template: **template.yaml**

   ![](media/input_values.png)

1. Repository will be pointing to the main branch, click on **Create** button.

    ![](media/click_create.png)

1. Choose the Kebab menu &#8942; and select **Security** option to configure the environment security.

    ![](media/Prod_env_security.png)

1. On the **Pipeline permission** section choose **+** button and select the pipeline.
Repeat the same for **Test** environment.

    ![](media/select_pipeline.png)

### Task 3: Create Azure Resource Manager service connection
> To create Azure Resource Manager service connection, you must be the owner or co-owner of the Azure Subscription

1. Sign in to your organization and select your project

1. Navigate to **Project Settings** and select **Service connections**

1. Select **Create service connection**, select the type of service as **Azure Resource Manger**, and then select **Next**

1. Choose an authentication method, and then select **Next**

    ![](media/Choose_ARM.png)

1. Choose the Authentication type as **Service principal (automatic)** and then select **Next**

    ![](media/Choose_SPN_Automated.png)

1. Choose the default Subscription and Provide the service connection name as **eShopOnWeb** and select **Save**


    ![](media/Choose_your_subscription.png)

> Service connection with the same name is already present in the YAML pipeline, no need to modify the pipeline.

### Task 4: Grant Permission to Pipeline

1. Open **eShopOnWeb** service connection created in the previous task

    ![](media/Open_eShopOnWeb_Connection.png)

1. Choose Security option on the Kebab menu &#8942;
    
    ![](media/Choose_Security.png)

1.  Under the **Pipelines permission** section, choose **+** button and select the pipeline **eShopOnWeb**. This grants the permission to the YAML pipeline to use the service connection.

    ![](media/Choose_pipeline.png)

### Task 5: Enable Advanced Security from Portal

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

### Task 6: Setup Advanced Security permissions

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
  


