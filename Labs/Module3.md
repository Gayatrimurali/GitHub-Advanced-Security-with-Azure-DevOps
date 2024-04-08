# Lab 03: Dependency Scanning

## Lab Scenario

In this lab you will implement  dependency scanning in Azure DevOps to identify and mitigate potential security vulnerabilities

## Lab Objectives

In this lab you will perform the following:

- Task 1: Setup Dependency Scanning
- Task 2: Viewing alerts of repository
- Task 3: Fixing dependency scanning alerts
- Task 4: Dismissing dependency scanning alerts

## Estimated Timing:45 minutes

### Task 1: Setup Dependency Scanning

Dependency Scanning scans your project's dependencies such as libraries, frameworks, and packages, to identify any known security vulnerabilities or outdated versions that may pose a risk to your application

1. Select the pipeline **eShopOnweb** and click on **Edit**.

    ![alert_detected](media/advlab33.png)

1. Locate the task *Advanced Security Dependency Scanning*(AdvancedSecurity-Dependency-Scanning@1) which already included in the YAML pipeline file.

    ```
      - task: ms.advancedsecurity-tasks.dependency-scanning.AdvancedSecurity-Dependency-Scanning@1
        condition: and(succeeded(), ne(variables['Build.Reason'], 'PullRequest'))
        displayName: 'Dependency Scanning'
     ```

    ![alert_detected](media/advlab32.png)

1. Click **Run** to run the pipeline configuration file which will setup the dependency scanning

    ![alert_detected](media/advlab31.png)

1. The build will run automatically, initiating the dependency scanning task and publishing the results to Advanced Security. Please note that this process may take up to 15 minutes to finish. 

    **Note:** Once the build is succeeded, you can ignore the permission needed prompt under the **Test Deployment** and proceed with the next task.

### Task 2: Viewing alerts of repository

1. Go to the **Repos** tab and click on the **Advanced Security** menu item at the bottom.

1. Click on **Dependencies** to see a list of all the dependencies alerts that have been found. This includes the Alert, Vulnerable package, and First detected date. We can easily clean up the dependencies.

#### Dependency Scanning Alert Details

1. Click on the item ***Improper Input Validation in IpMatcher...*** to see the details about this alert.

1. This includes the Recommendation, Locations found,  Description, Severity, and the Date it was first detected. We can easily clean up the dependencies. 

   ![alert_detected](media/do1.png)

1. You can also view the code that triggered the alert and what build detected it.

1. Click on Detections to see the different builds that detected this alert.

   ![where_detected](media/advlab34.png)

   > **Note**  
    When a vulnerable component is no longer detected in the latest build for pipelines with the dependency scanning task, the state of the associated alert is automatically changed to Closed. To see these resolved alerts, you can use the State filter in the main toolbar and select Closed.


#### Understanding Dependency Alerts

In your repository, there are two types of dependencies: direct and transitive (also known as indirect).

- **Direct dependencies** are components in your project.

- **Transitive dependencies** are components used by direct dependencies.


### Task 3: Fixing dependency scanning alerts

You can follow the recommended steps to manually update dependencies.

When a Dependency Alert is created in Azure DevOps Advanced Security, it will contain details about the vulnerability and steps you can take to resolve it.

1. To view the alert, go to the Azure DevOps Advanced Security dashboard, scroll down and click on the alert  *Improper Input Validation in IpMatcher....*

1. Review Recommendation, Location, Description, and Severity to understand the vulnerability and how to resolve it.

   {% include tip.html content= "The recommendation will provide you with the steps to resolve the vulnerability. For this one, simply update the package version from 1.0.4.1 to 1.0.4.2 to fix the vulnerability." %}

1. Click on the Locations to see the code that triggered the alert.
 
1. From the code editor, update the package to 1.0.4.2. To do that, here we will use Visual Studio. 

1. Copy the repo URL from Azure DevOps by navigating to the **Repos** section from the left navigation pane and click on **Clone** to get the repo URL and note it in the notepad.

    ![Dependencies](media/clone1.png)

    ![Dependencies](media/clone2.png)

1. **Sign in** to the Visual studio with the credentials email address: **<inject key="AzureAdUserEmail"></inject>** and  Password:**<inject key="AzureAdUserPassword"></inject>** and later select **Start Visual studio**

    ![Dependencies](media/vs1.png)

    ![Dependencies](media/vs2.png)

1. Select **Clone a repository** under get started and enter the clone URL under **Repository location** which is copied earlier and click **Clone**	

    ![Dependencies](media/vs3.png)

    ![Dependencies](media/vs4.png)

1. While cloning the repo, Git-credentials Manager pops-up, enter the same credentials provided in the environment details tab.

1. Create a new branch to make the necesaary changes, select the **main** branch from the lower right corner and select **New branch**

    ![Dependencies](media/vs6.png)

    > **Note:**
    This step is necessary since the main branch is protected by a pull request pipeline.

1. On a create a new branch window, enter **codefix** and click **create**

    ![Dependencies](media/vs7.png)

1. Double click the **eShopOnWeb.sln** solution file  

    ![Dependencies](media/vs5.png)

1. Once the source code is opened in Solution Explorer, navigate to the **Dependencies** section under Web.(SRC>Web)

    ![Dependencies](media/advlab35.png)

1. Right-click on **Dependencies** and choose *Manage Nuget Packages...*

    ![Manage Nuget](media/advlab36.png)

1. Click on **IpMatcher** and you will be able to see a warning regarding the vulnerability in that specific version.

    ![IpMatcher](media/advlab37.png)

1. Change the version as per the suggestion that is **1.0.4.2** and select **Update**

    ![Update the Package](media/advlab38.png)

1. Switch to **Gitchanges** tab and select **Configure** to add the username and email address which is required before committing changes.

    ![Dependencies](media/vs8.png)

1. Click on **Save**

    ![Dependencies](media/vs9.png)

1. Add the required **description** and select the **Commit All and Push** option to push the changes to Origin.

    ![Dependencies](media/vs10.png)

1. Navigate to **Azure Devops** and click on Pipelines from the left navigation pane and wait until the build is complete.

1. Once the build is complete, click on **Repos** and select **Pull requests** and select **create a pull request** to push the commits from *codefix* to the *main*.

   ![Dependencies](media/vs11.png)

1. On the **New Pull request** page, add any work item from the list(which is mandatory) and click on **Create**

    ![Dependencies](media/vs12.png)

    > **Note:** The build will run automatically, initiating the dependency scanning task and publishing the results to Advanced Security and alert automatically closed.

1. Once the **eShoponWeb** pipeline has been completed, click **Approve** and then click **Complete**.

   ![Dependencies](media/do2.png)

1. Change Merge Type to **Squash commit** and check box Delete SecretFix after merging, to merge changes into the main branch.

   ![Dependencies](media/do3.png)

    >**ProTip!** Squash Merge is important. If we just commit, the exposed credential will still be in the history. To avoid this, fix code, use a Squash Merge, push it to repo, and you're done!

### Task 4: Dismissing dependency scanning alerts

1. Navigate to the Pipelines section and wait for it to complete.It might take upto 20 minutes.

1. Once the pipeline has been completed, **eShopOnWeb**, go to the Azure DevOps Advanced Security dashboard and click on Dependencies.

1. You will see that the alert *Improper Input Validation in IpMatcher....*... no longer exists, as it is now closed.

   > **Note:** This is a great way to ensure you are using the latest and greatest versions of your dependencies, and also, ensure you are not using any vulnerable versions.

## Review
In this lab you have completed the following:
- Setup Dependency Scanning
- Viewed alerts of repository
- Fixed dependency scanning alerts
- Dismissed dependency scanning alerts

Click **Next** to continue with the next lab.

