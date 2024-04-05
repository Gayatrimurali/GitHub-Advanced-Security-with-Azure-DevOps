## Lab 04: Code scanning

### Task 1: Setup Code Scanning

Code scanning in GitHub Advanced Security for Azure DevOps lets you analyze the code in an Azure DevOps repository to find security vulnerabilities and coding errors. Any problems identified by the analysis are raised as an alert. Code scanning uses CodeQL to identify vulnerabilities.

1. Select the pipeline **eShopOnweb**

   ![alert_detected](media/advlab33.png)

1. Locate the tasks related to *Advanced Security Code Scanning** which already included in the YAML pipeline file.

   ![alert_detected](media/advlab41.png)
 
1. Do not run the pipeline, code scanning set up already initiated along with dependency scanning performed in the previous lab.

### Task 2: Review Code Scanning Alert (Gain Insights)

1. Go to the **Repos** tab and click on the Advanced Security menu item at the bottom.

1. Click on **Code scanning** to see a list of all the code scanning alerts that have been found. This includes the Alert, Vulnerable code details, and First detected date.

#### Code scanning Alert Details

1. Click on the item ***Uncontrolled command line...*** to see the details about this alert.

1. This includes the Recommendation, Locations found,  Description, Severity, and the Date it was first detected. We can easily fix this threat. 

   ![code_alert_detected](media/advlab4n2.png)

1. You can also view the code that triggered the alert and what build detected it.
   
1. Click on Detections to see the different builds that detected this alert.

   ![where_detected](media/advlab4n1.png)

    **ProTip!** When a vulnerable component is no longer detected in the latest build for pipelines with the dependency scanning task, the state of the associated alert is automatically changed to Closed. To see these resolved alerts, you can use the State filter in the main toolbar and select Closed.

### Task 3: Fixing the Code to resolve the alert

1. This is simple to fix using the method using parameters with dynamic SQL described in the Remediation steps.

1. Click on Locations found to see the code that triggered the alert.

   ![Image](media/advlab4n6.png)

1. Click on the Edit button to edit the file. Line number 20 is highlighted here. 

1. The value of __{drive}__ is getting red from the line number 20.

    ![Image](media/advlab4n3.png)

1. Instead of getting the value of 
__{drive}__ using a query, we can directly define it as __C__.
    ```C#
    string drive = "C";
    ```

    ![Image](media/advlab4n4.png)

1. Click Commit to save changes. Enter *Fixalert* for branch name and check Create a pull request, then click Commit again.

    ![Image](media/advlab4n5.png)

    >Note: This step is necessary since the main branch is protected by a pull request pipeline.

1.	Click Create on the New pull request page to merge the changes into the main branch.

1. Make sure all the policies are followed and complete the pull request.

1.  This will run the **eShopOnWeb** pipeline.

    >Note: The build will run automatically, initiating the code scanning task and publishing the results to Advanced Security.

### Task 4: Dismissing the code scanning alerts 

1. Once after the completion of the build, if you navigate to the __Code scanning__ section of __Advanced Security__. You find the alert is closed automatically

