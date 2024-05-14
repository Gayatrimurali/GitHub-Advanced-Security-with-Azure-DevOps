# Lab 05: Microsoft Defender for Cloud DevOps security

## Lab Scenario

In this lab, we connect the Azure DevOps environment to Microsoft Defender for Cloud to enhance DevOps security. We will explore the DevOps security findings and inventory provided by Microsoft Defender for Cloud to review their security posture.

## Lab Objectives

In this lab, you will perform the following:

- Task 1: Connect Azure DevOps Environment to Microsoft Defender for Cloud
- Task 2: Understand your DevOps security

## Estimated Timing: 30 minutes

## Architecture Diagram

  ![AD](media/ard05.png)

### Task 1: Connect Azure DevOps Environment to Microsoft Defender for Cloud

1. Sign in to the Azure portal, using the below credentials

   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

   - **Password:** <inject key="AzureAdUserPassword"></inject>

1. Search and select **Microsoft Defender for Cloud** from the portal

    ![alert_detected](media/mls2.png)

1. Select **skip** on **Getting started** tab.

    ![alert_detected](media/mls1.png)

1. Select **Environment settings** under Management > **+Add environment** > **Azure DevOps**

    ![alert_detected](media/advlab51.png)

1. On the **Azure DevOps Connection** page, under **Account details**, provide the below settings.

   | Setting  | Value |
   -----------|---------
   | Connector name | AzureDevopsconnector |
   | Subscription | Choose the default subscription |
   | Resource group | Lab-VM |
   | Location | Select any supporting region |

    ![alert_detected](media/advlab52.png)

1. Select **Next: Configure access**

1. Select **Authorize**. Ensure you're authorizing the correct Azure Tenant using the drop-down menu in Azure DevOps and by verifying you're in the correct Azure Tenant in Defender for Cloud.

1. In the popup dialog, read the list of permission requests, and then select **Accept**.

    ![alert_detected](media/advlab53.png)

1. Leave all other settings as default.

1. Select **Next: Review and generate**.

1. Review the information, and then select **Create**.

1. Wait for some time to view the connector on the **Environment settings** page.

    ![alert_detected](media/advlab54.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - Click the Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation Page.
> - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="c52850e5-7c62-4d01-a624-175043de84b6" />

### Task 2: Understanding your DevOps security

1. Navigate to **DevOps Security** under **Cloud Security**.

    ![alert_detected](media/advlab55.png)

1. The **DevOps security findings** and **DevOps security results** are listed on the page, which helps to review the DevOps security posture.

    ![alert_detected](media/m51.png)

   >**Note:** It might take upto 8hrs to reflect the real-time status.

1. Navigate to **DevOps workbook** and change the toggle to **Yes**, which provides an overview of the tabs provided below

    ![alert_detected](media/m55.png)

    ![alert_detected](media/m52.png)

1. Navigate to the **Code** tab and scroll down, click on the **Severity** section to open the individual findings, and click on **Information** which in turn provides detailed findings and the issue location.

    ![alert_detected](media/m53.png)

1. Similarly, navigate to the **OSS Vulnerabilities** tab and identify the issues, then take note of the recommendations provided to resolve the issues.

    ![alert_detected](media/m54.png)

 Please feel free to go through these links for further understanding: [Application Security](https://info.microsoft.com/US-DevOps-VDEO-FY24-02Feb-12-GitHub-and-AI-A-Powerful-Duo-for-Application-Security-Testing-SRGCM11732_LP01-Registration---Form-in-Body.html) and [Email Reactor](https://developer.microsoft.com/en-us/reactor/series/S-1311/?wt.mc_id=promotional_S-1311_email_reactor)

## Review
In this lab, you have completed the following:

-  Connected Azure DevOps Environment to Microsoft Defender for Cloud.
-  Understood your DevOps security.

