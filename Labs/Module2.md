# Lab 02: Secret Scanning 

## Lab Scenario

In this lab, we implement secret scanning in Azure DevOps to identify and mitigate potential exposures. We learn to view, fix, and dismiss secret scanning alerts, enhancing security measures within their development environment.

## Lab Objectives

In this lab, you will perform the following:

- Task 1: Viewing alerts of the repository
- Task 2: Fixing secret scanning alerts
- Task 3: Dismissing secret scanning alerts
  
## Estimated Timing: 30 minutes

## Architecture Diagram

  ![AD](media/ard02.png)
  
Secret Scanning scans your codebase and other resources to identify potential secrets that may have been inadvertently committed and provides alerts to mitigate the risk of exposure. Push protection also prevents credentials from being leaked in the first place.

Once this is toggled on, it starts off a background scan of this repo and looks for exposed credentials. The scan doesn't just look at the tip of the main, since attackers would look through all the branches and the entire commit history.

### Task 1: Viewing alerts of repository

The Advanced Security Alert Hub is where all alerts are raised and where we gain insights, specifically under the category of Secrets. When a secret is found, you can click on it to access more information. The secret may be located in different places, including various commits. 

1. Go to the **Repos** tab and click on the **Advanced Security** menu item at the bottom.

   ![setup](media/lab1-image16.png)

1. Click on **Secrets (1)** to see a list of all the exposed secret alerts that have been found. This includes the alert and introduced dates. Click on the **Azure DevOps personal access token (PAT) (2)** to see more details about the alert and what you can do to clean up the secret.

   ![Secrets page](media/secv1.png)

1. Notice that this includes the Recommendation, Locations found, Remediation steps, Severity, and the Date it was first introduced. We can easily clean this up and dismiss the alert.

   ![Secret Details](media/remv.png)

### Task 2: Fixing secret scanning alerts

Once a credential touches the repo, it's too late. Hackers might have already exploited it. The only way forward is to permanently eliminate these leaks and find all the places they're being used in production.

 **Note:** Good news! GHAzDO focuses on preventing this in the first place. Bad news! These need to be manually fixed. There isn't an easy button.

#### Push Protection

Push Protection helps protect your repository by preventing unauthorized or malicious code from being pushed to your repository's branches.

#### Updating Secrets:

You can follow these steps to update a file. 

1. While viewing the alert details, click on the line of code, _Constants._ _cs_.

    ![Click on File](media/editv.png)

1. Click on **Edit** to edit the file. This will open the code editor and highlight the exact location of the secret. In this case, it's in the .cs file.

   ![setup](media/06-26-2024(10).png)

1. On line 5, update the variable name to **AZDO_PAT (1)**, then click **Commit (2)** to save the changes.
    
     ![setup](media/azdov.png)

1. Enter **PATDetails (1)** for the branch name and then click on **Commit (2)** again.

     ![setup](media/branchv.png)

1. The commit was rejected because the repository has secret protection enabled. This is a good thing! It's preventing us from checking in on the exposed secret. Let's fix this.
   
    ![Commit Rejected](media/comv.png)

    > **Note:** The code went up to the server, was analyzed, rejected, and not stored anywhere. Using Secret push scanning, it catches secrets right before they become a problem.

    > **ProTip!** This can't happen during a Pull Request. Once the code has been pushed into a topic branch, it's too late. PR analysis is best for dependency scanning but not secret push scanning. They are different.

#### Bypass push protection

1. Update your comment with **skip-secret-scanning:true** and click **Commit**.

    ![Commit Bypass](media/skipv.png)

    >**Note:** Bypassing flagged secrets isn't recommended because bypassing can put a company’s security at risk.

#### Fixing Exposed Secrets

You can follow these steps to fix the exposed secret. 

1. Click on **Edit**.

    > **Note**: This scenario is all too common. Developers often forget to remove the connection string from the appsettings.json file when testing an application, exposing the secret in the repo and allowing exposed credentials to remain in history, resulting in a significant security hole. This is a common issue when testing local applications.

    ![setup](media/06-26-2024(10).png)

1. On line 5, replace the PAT value with **#{PAT}#** **(1)** and click on **Commit (2)** to save changes.

    ![setup](media/varv.png)

1. Enter **SecretFix** for the branch name and link the **Work item** created earlier from the list.

    ![Remove STORAGE_ID](media/secv.png)

    > **Note:** This step is necessary since the main branch is protected by a pull request pipeline.

1. Navigate to **User settings (1)** > **Personal access token (2)**.

   ![Remove STORAGE_ID](media/06-26-2024(7).png)

1. Select the existing token and select **Regenerate** twice and **copy** the token value to the notepad.

    ![Remove STORAGE_ID](media/regv.png)

    ![Remove STORAGE_ID](media/copyv.png)

1. Next, we need to update the build pipeline to add a variable. Click on **Pipelines (1)** and select **eShoponWeb (2)**.

    ![setup](media/06-26-2024(8).png)

1. Click on **Edit** to edit the pipeline. Change the branch to the **SecretFix (1)** branch and click on **Variables (2)**.

     ![setup](media/lab1-image20.png)
   
     ![Remove STORAGE_ID](media/advsc44.png)
 
1. Once the **Variables** pane opens, click on **+** to create a new variable.

     ![setup](media/lab1-image21.png)

1. Enter **PAT (1)** for the name and paste the secret **value (Regenerated value) (2)** from Notepad into the value field. Click on **Keep this value secret (3)** to hide the value, then click **OK (4)** and **Save (5)**.

   ![setup](media/patv.png)
   
1. Click on **Repos (1)**, click **Pull Requests (2)**, and click on **New pull request (3)** to merge the changes from branch **SecretFix** into branch **main**.

    ![Pipeline Save](media/06-26-2024(11).png)

1. For the title, enter the **Fixed secret (2)** and click on **Create (3)**. This will run the **eShoponWeb** pipeline to validate changes. 

    ![Pipeline Save](media/06-26-2024(12).png)

    >**Note:** Make sure you add a work item link from the dropdown created earlier if it is not added automatically for the pipeline to run successfully.

1. Once the **eShoponWeb** pipeline has been completed, click **Approve**, and then click on **Complete**.

1. Change the Merge Type to **Squash commit (1)** and check both **Complete associated work items after merging (2)** and **Delete SecretFix after merging (2)**. Finally, click **Complete merge (3)** to merge the changes into the main branch.

    ![Completing merge](media/advlab25.png)

### Task 3: Dismissing secret scanning alerts

You can follow these steps to dismiss the alert.

1. Once the pipeline eShoponWeb has been completed, from the left navigation pane under **Repos**, go to the Azure DevOps **Advanced Security** dashboard and click on **Secrets**. 

1. Click on the following item, **Azure DevOps personal access token(PAT)** to see the exposed secret and how we easily dismiss the alert. 

1. Click on **Close alert (1)** to dismiss the alert. Select **Revoked (2)**, and then click on **Close (3)**.
    
    ![Closing Alert](media/advlab24.png)

    >**Note**: Once the code is merged into the main, GHAzDO starts a background scan of this repo and looks for exposed credentials. The scan doesn't just look at the tip of the main, since attackers would look through all the branches and the entire commit history.

1. Go to the Azure DevOps Advanced Security dashboard, click on **Secrets**, and subsequently click on **View other alerts**. You will see a list of other exposed secret alerts that have been found. 

1. You will see that the alert **Azure DevOps personal access token(PAT)** no longer exists, as it is now revoked.

    >**Note**: Anyone with contributor permissions for a repository can view a summary of all alerts for a repository, but only the project administrator and project collection administrator  can dismiss Advanced Security alerts.

## Review
In this lab, you have completed the following:

- Viewed alerts of the repository.
- Fixed secret scanning alerts.
- Dismissed secret scanning alerts.

Click on **Next** to proceed with the next lab.
