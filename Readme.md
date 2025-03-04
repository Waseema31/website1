<h1>🚀 Static Website Deployment on Azure Storage with CI/CD using GitHub</h1>

<h3>📌 Overview</h3>

<p>This project demonstrates how to deploy a static website on an Azure Storage Account and set up a CI/CD pipeline using GitHub Actions for automated deployment. With this setup, any changes pushed to the repository are automatically deployed to Azure Storage.</p>



## Setting Up Monitoring for Static Website with Azure Application Insights and Log Analytics
**Step1:Create a Log Analytics Workspace
Go to Azure Portal:**

Open Azure Portal.
Create a Log Analytics Workspace:

    - In the search bar, type “Log Analytics” and select Log Analytics Workspaces.
    - Click + Create to create a new workspace.
    - Fill out the required details:
        - Subscription: Select your subscription.
        - Resource Group: Choose the same resource group you’re using for other resources or create a new one.
        - Name: Provide a unique name for the workspace (e.g., StaticWebsiteLogWorkspace).
        - Region: Select the region where you want to create the workspace.
    - Click Review + Create and then Create.

**Step 2: Add Diagnostic Settings to the Azure Storage Account**

Go to Your Storage Account:

    - In the Azure Portal, go to Storage Accounts and select your storage account (e.g., storage244).
    - Enable Diagnostic Settings:

    - Under Monitoring, select Diagnostic settings.
    - Click + Add diagnostic setting.
    - Fill in the details:
        - Name: Provide a name (e.g., LogToWorkspace).
        - Send to Log Analytics: Select Send to Log Analytics and choose your Log Analytics Workspace (created in Step 1).
        - Select logs: Ensure you select Read, Write, and Delete logs or other relevant options.
    - Click Save to enable diagnostics.


**Step 3: Create Alerts
Go to Azure Monitor:**

In the Azure Portal, go to Monitor in the left sidebar.
    - Create a New Alert Rule:

    - Click Alerts > + New Alert Rule.
    - Select the Resource:
    - Under Resource, select the Log Analytics Workspace or your Storage Account depending on what you want to monitor.

    - Set Alert Condition:
        - Click Add Condition and choose the log query or performance metric you want to monitor (e.g., errors, failed requests).
        - Set the condition (e.g., if there are any error logs in the last 5 minutes, trigger an alert).
       - Set Alert Actions:

    - Click Add Action Group to create an action group (e.g., email, SMS, or webhook notifications).
    - Review and Create:
    - Review your alert settings and click Create.

**Step 4: Set Up Application Insights**

- Create an Application Insights Resource:
In the Azure Portal, search for Application Insights and click Create.

- Fill out the form with the required details (Subscription, Resource Group, Name, Region) and click Create.

**Step 5: Add an Availability Test in Application Insights**

Open Your Application Insights Resource:

    - After creating the Application Insights resource, go to the resource.
    - Navigate to the Availability Tab:
    - In the left pane, select Availability under Monitoring.
    - Add a New Test:
    - Click + Add Test to create a new availability test.
    - Configure the Availability Test:
        - Test Type: Choose Standard (URL Ping Test).
        - Test Name: Enter a name (e.g., StaticWebsiteUptime).
        - URL: Enter the URL of your static website (e.g., https://storage244.z13.web.core.windows.net/).
        - Test Locations: Choose multiple global locations (e.g., UK, US, Europe).
        - Test Frequency: Set the test frequency (e.g., every 5 minutes).
        - Success Criteria: Set the failure criteria (e.g., failure if the response code is 400+).
    - Create and Save the Test:
    - Click Create to enable the availability test.

**Step 6: Set Up Alerts in Application Insights (Optional)**

Go to Application Insights Alerts:

In Application Insights, go to the Alerts section.
Create a New Alert Rule:

    - Click + New Alert Rule to create an alert based on availability test failures.
    - Select Your Application Insights Resource:
    - Under Resource, select your Application Insights resource.
    - Set Alert Condition:
        - Add a condition to monitor for Availability Test Failures and define your alert criteria (e.g., trigger if there are more than 1 failure within 5 minutes).
        - Configure Action Group:
        - Click Add Action Group to set up notifications like email, SMS, or webhook.
    - Review and Create:
    - Review your settings and click Create.

**Final Monitoring Setup:**
Monitor Log Analytics Workspace:
- Use Log Analytics queries to analyze logs for any issues related to your static website, such as request failures or error logs.
- Monitor Application Insights Availability:
- View test results in Application Insights > Availability to monitor your website’s uptime and performance.
- Trends and Insights:
- Use Metrics Explorer in Application Insights and Logs in Log Analytics to monitor trends in uptime, performance, and error logs.

By following these steps in this sequence, i was  able to effectively monitor the  static website, set up alerts, and gather performance insights using both Log Analytics Workspace and Application Insights.

Here’s a simple breakdown of what I’ve done so far to set up monitoring for my static website on Azure Storage:
________________________________________
**1. Created a Log Analytics Workspace**
- I created a Log Analytics Workspace to store and analyze logs for my website.
- This is where all the data (like errors or performance metrics) from my resources will be sent for monitoring.
________________________________________
**2. Set Up Diagnostics for Your Static Website**
- I went to my Azure Storage account (where my static website is hosted).
- I enabled Diagnostic Settings, which sends data (like requests, responses, and performance data) to the Log Analytics Workspace.
- This helps us track how well my website is performing and spot any issues.
________________________________________
**3. Set Up Alerts (Optional)**
- I created Alert Rules to notify me if something goes wrong with my website (e.g., if it’s down or slow).
- These alerts can be sent via email, SMS, or other channels, so i can quickly act if there’s a problem.
________________________________________
**4. Started Monitoring with Application Insights**
- I set up Application Insights to monitor the availability (up/down status) of my website.
- I added a test that checks if my website is online at regular intervals (like every 5 minutes). If your website is down, i get notified.
________________________________________
Now, I have tools in place to monitor  website’s health, check its performance, and get notified if there’s any downtime or issue. All this is done using Azure Monitor tools like Log Analytics and Application Insights.
