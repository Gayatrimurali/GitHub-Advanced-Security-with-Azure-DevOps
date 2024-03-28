## Lab 01: Configure GHASDO in Azure DevOps

### Task 1: Enable Advanced Security from Portal

GitHub Advanced Security for Azure DevOps includes extra permissions for more levels of control around Advanced Security results and management. Be sure to adjust individual permissions for your repository.

 To ensure Azure DevOps Advanced Security is enabled in your organization, you can follow these steps:

1.	Sign in to your Azure DevOps account with appropriate permissions to access organization settings.

1.	Navigate to the Azure DevOps organization and Team Project you want to check.

1.	In the lower-left corner, click on **Project Settings**. In the left menu area under Repos, click **Repositories**.

1.	Click on the **eShopOnWeb** repository.

1.	Click on Settings, then click **Advanced Security**, On to turn it on.

      ![setup](media/setup-enable.png)

1.	Click Begin **Billing**.

      ![enable-billing](media/enable-billing.png)

1.	Advanced Security and Push Protection are now enabled. You can also onboard Advanced Security at [Project-level](https://learn.microsoft.com/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&tabs=yaml#project-level-onboarding) and [Organization-level](https://learn.microsoft.com/en-us/azure/devops/repos/security/configure-github-advanced-security-features?view=azure-devops&tabs=yaml#organization-level-onboarding) as well
 

   {% include note.html content= "GitHub Advanced Security for Azure DevOps includes extra permissions for more levels of control around Advanced Security results and management. Be sure to adjust individual permissions for your repository." %}

### Task 2: Setup Advanced Security permissions
1.	Select Security, under Azure DevOps Groups, and click on **Project Administrators**.

2.	Next to Advanced Security: manage and dismiss alerts, click the dropdown and select  **Allow**.

3.	Next to Advanced Security: manage settings, click the dropdown and select **Allow**.

4.	Next to Advanced Security: view alerts, click the dropdown and select **Allow**.

5.	If successful, a green checkmark ✅ appears next to the selected permission.

    ![allow-permissions](media/Allow-permissions.png)


