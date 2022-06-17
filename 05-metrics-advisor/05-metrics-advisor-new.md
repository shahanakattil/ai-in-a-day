# Lab 4 - Data monitoring and anomaly detection using Metrics Advisor in Azure Cognitive Services 

This lab covers the Metrics Advisor service features from Azure Cognitive Services.

## Before the hands-on lab

**Duration**: 30 minutes

You should follow all of the steps provided in this section _before_ taking part in the hands-on lab ahead of time as some of these steps take time.

## Task 1 - Prepare Azure Machine Learning workspace

1. Navigate to [the Azure portal](https://portal.azure.com) and log in with your credentials. Then, select **Resource groups**.

    ![Open Azure resource group](media/azure-open-resource-groups.png)

2. Select the **AI-in-a-Day** resource group.

3. Select the storage account named **aiinadaystorage<inject key="DeploymentID" enableCopy="false"/>**.

    ![Locate storage account in Azure Portal](media/select-azure-storage-account01.png)

4.  Select `Access keys` from the left side menu, and then select `Show keys`. Save the storage account name, the `key1 Key` value, and the `key1 - Connection string` value for later use.

    ![Storage account name and key](media/datastore-03.png)

## Task 2 - Prepare the COVID cases per age group dataset

1. Navigate to back to the resource group `AI-in-a-Day`. Select the AML Workspace named **ai-in-a-day-<inject key="DeploymentID" enableCopy="false"/>**
  
    ![Select AML](media/select-aml-ws.png)
   
2. Click on **Launch Studio** button.

    ![Launch Studio](media/launchstudio_lab05.png)

2. In Azure Machine learning studio, select **Notebooks**. If you see any popup `What's New in Notebooks`, close that.

    ![Launch Studio](media/select-notebook-1.png)

3. In the Notebooks environment, check if `preparemetricsfeeddata.ipynb` is there in **Users\odl_user_<inject key="DeploymentID" enableCopy="false"/>** folder. If it is not there download and import using next steps.

    ![Launch Studio](media/lab-user-1.png)

4. If the folder does not contain `preparemetricsfeeddata.ipynb` notebooks, download the following items to your local machine:

    [Prepare metrics feed data](https://aiinadayaiw.blob.core.windows.net/aiinaday/preparemetricsfeeddata.ipynb)

5. Upload the file by selecting the Upload button from the top right corner of the screen, and then selecting the blue Upload button to confirm.

    ![Launch Studio](media/select-upload-1.png)
   
   - Click on `Click to browse and select file(s)` and select the file which was just dowloaded.
   - Check the "I trust contents of the File" and select upload. 
   
    ![Launch Studio](media/select-upload-2.png)

6. With the Azure Machine Learning studio and the Jupyter notebook environment open, select the `preparemetricsfeeddata.ipynb` from **Notebooks** under **Author**.

    ![preparemetricfeeddata notebook](media/notebook_05.png)

7. You have to **Choose an available Jupyter kernal**, select **Python 3.8 - AzureML** from the drop-down and then select **Start Jupyter kernal**.

    ![select kernal for preparemetricfeeddata notebook](media/AI-notebook-kernal-update.png)
    
>**Note**: Please ensure to click on **Authenticate** button if a pop-up notification comes like below.

   ![authenticate pop-up](media/AI-notebook-authenticate.png)
   
8. Make sure **Python 3.8 -AzureML** kernal selected as shown in the below screenshot.

   ![Kernal selected](media/AI-notebook-python3.8-kernal.png) 

> **Note**: Make sure you replace the `<BLOBSTORAGE_ACCOUNT_NAME>` and `<BLOBSTORAGE_ACCOUNT_KEY>` values in the variable initialization cell with the values you have noted down at the end of the previous task.

   The notebook will guide you through a list of steps needed to prepare a time series-based dataset containing JSON files to be fed into the Metrics Advisor workspace. Each JSON file will contain daily data representing the count of COVID positive cases by age group.

9. Execute the notebook cell by cell (using either Ctrl + Enter to stay on the same cell, or Shift + Enter to advance to the next cell) and observe the results of each cell execution.

## Hands-on Lab

## Task 1 - Explore dashboard of COVID-19 data

Understanding the source datasets is very important in AI and ML. To help you expedite the process, we have created a Power BI dashboard you can use to explore them at the begining of each lab.

![Azure AI in a Day datasets](../media/data-overview-01-01.png)

To get more details about the source datasets, check out the [Data Overview](../data-overview.md) section.

To explore the dashboard of COVID-19 data, open the `Azure-AI-in-a-Day-Data-Overview.pbix` file located on the desktop of the virtual machine provided with your environment.

## Task 2 - Explore lab scenario

Besides collecting data about COVID-19 cases, it is also essential to ensure the accuracy of the reporting. Accuracy check is where continuous monitoring of incoming data feeds doubled by automatic detection of anomalies plays a critical role. Data is valid for analysis as long as it is reliable and contains the minimum possible number of errors. With distributed data sources and numerous reporting entities, automatic anomaly detection is the best choice to minimize that number.

Using Cognitive Services Metrics Advisor, we will demonstrate how to improve the case surveillance data quality by identifying as early as possible anomalies in the number of daily reported cases.

The following diagram highlights the portion of the general architecture covered by this lab.

![Architecture for Lab 5](./../media/Architecture-5.png)

The high-level steps covered in the lab are:

- Explore dashboard of COVID-19 data
- Explore the lab scenario
- Onboard your time series data in the Metrics Advisor
- Explore anomalies detected in your data
- Perform root cause analysis
- Explore anomalies with hard thresholds (optional)

## Task 3 -  Deploy Azure Cognitive Services Metrics Advisior instance

1. Navigate to the Azure portal and click on the menu icon and select **+ Create a resource**

   ![](media/menu_icon.png)  

2. In the search bar type **Metrics Advisor** and then select **Create**

   ![](media/AI-metric-advisor-create.png)  

3. Under Project details on Create Metrics Advisor page provide the following details and click **Review + Create**

    * Subscription : Select the available Subscription
    * Resource Group : **Ai-in-a-Day**
    * Region : Select the available Region from the dropdown
    * Name : **metricsadvisor-<inject key="DeploymentID" enableCopy="false"/>** 
    * Pricing tier: **S0**
    * Make sure to mark checkbox ☑ for **I confirm I have read and understood the notice below**.
   
     ![](media/AI-metric-advisor-latest.png)

4. Once the validation is passed click on **Create**. The deployment could take up to **60 minutes** to complete, although it normally finishes in less than **10 minutes**. Please wait untill the deployment gets succeeded and then, you can proceed with next task.

## Task 4 - Configure the "COVID cases by age group" Metrics Advisor data feed

1. Back to the Home page in Azure Portal, in the list of your recent resources, locate the Azure Metrics Advisor workspace and select it. If you are prompted to sign-in again, use the same lab Azure credentials you used at the previous step.
![Open Azure Metrics Advisor](./media/metrics-advisor.png)

2. On the Metrics Advisor Overview page, select the `Go to workspace` link in the first section to start working with the web-based [Metrics Advisor workspace](https://metricsadvisor.azurewebsites.net/).

    ![Start the web-based workspace](./media/metrics-advisor-overview.png)

3. On the Metrics Advisor welcome page, select your Directory, subscription and workspace information and select **Get started**. You are now prepared to create your first Data feed.

   > **Note:-** If you see that **Get Started** button is not available for you, it means that the metric advisor service is not fully available yet. Please wait for 20-30 minutes and try again after refreshing the page.

    ![Connect to Metrics Advisor workspace](./media/metrics-advisor-connect.png)

4. With the Metrics Advisor workspace opened, select the **Add datafeed** option from the left navigation menu.

5. Add the data feed by connecting to your time-series data source. Start by selecting the following parameters:

    - **Source type**: `Azure Blob Storage (JSON)`
    - **Granularity**: `Daily`
    - **Ingest data since (UTC)**: `2022-02-01`
    - **Connection string**: provide the connection string from the blob storage access keys page. (`key1 - Connection string` copied on **Before the hands-on lab** part or else please  follow Task 1 of Before the hands-on lab) 
    - **Container**: `jsonmetrics`
    - **Blob template**: `%Y-%m-%d.json` (since the daily json files are provided in with naming format)
    - **JSON format version**: `v2` (since we'll be using the age group dimension in our data schema)

    ![Data feed source properties](./media/adddatafeed1.png)

6. Select the **Load data button** to validate the configured connection, y=you can find **Load Data** option just below the **JSON format version** in right side, so scroll in right to see teh button.  If there is an error at this step, check that your connection string and blob template are correct and your Metrics Advisor instance is able to connect to the data source.

7. Once the data schema is loaded and shown like below, configure the appropriate fields as Dimension, Measure or Timestamp and select **Verify schema**.

    ![Schema configuration](./media/schemconfig1.png)

8. Scroll down towards the bottom of the page. For **Automatic roll-up** settings, select the **I need the service to roll-up my data** (1) option, select the link **Set roll-up columns** and include both dimensions (3).

    ![Automatic rollup settings](./media/automaticrollup1.png)

9. In the **Advanced settings** section, inside **Ingestion options**, set **Stop retrying after** to **0** hours to stop the ingestion process after the first run. 
    
    ![Advanced settings](./media/advancedsettings.png)

10. In the **Misc** section, choose the option to **Fill previous** for anomaly detection model.

    ![Misc settings](./media/fillprevious.png)

11. Provide the **Data feed name**: `covid-ages` and select **Submit** to confirm and submit the data feed.

    ![Submit schema configuration](./media/submitdatafeed.png)

12. Wait for the ingestion progress dialog and select the **Details** link in order to observe the ingestion log by timestamp. Wait until the ingestion completes with success for all ingested json files.

    ![Check the ingestion progress](./media/ingestionprogress1.png)


## Task 5 - Explore anomalies detected in data

After the data feed is added, Metrics Advisor will attempt to ingest metric data from the specified start date. It will take some time for data to be fully ingested, and you can view the ingestion status by clicking Ingestion progress at the top of the data feed page. If data is ingested, Metrics Advisor will apply detection, and continue to monitor the source for new data.

When detection is applied, you can select one of the metrics listed in data feed to find the Metric detail page to:

- View visualizations of all time series slices under this metric
- Update detecting configuration to meet expected results
- Set up notification for detected anomalies


1. Select the **Visit data-feed: covid-ages** button to navigate to the data feed overview page.

    ![Check the ingestion progress](./media/ingestionprogress2.png)

2.  In the data feed page, select the `count` metric under the **Metrics** section.

    ![Go to the count metric details page](./media/browsemetricdata1.png)

3.  To modify the inspected time window, change the start and end time of the interval from the calendar above the graphic representations.
    
    ![Change monitoring time window](./media/AI-metric-advisor-count-overview.png)

4.  Make sure you see the ingestion process completed on recent historical data **(1)** as illustrated in the picture bellow. When all data is ingested, in the left configuration section, under the **Metric-level configuration** **(2)** change the default metric-level configuration to use Smart detection and set the sensitivity level to 81 and use this configuration:
    - Value **Out of boundary** is anomaly 
    - Do not  report anomaly until **10%** of latest **1** points are detected as anomalies.

    > **Note:-** It can take 30 minutes to completed on recent historical data, so please wait or continue with next lab and come back later and continue this lab.

    ![Metric-level configuration](./media/metric-level-configuration-smart1.png)

>Note
>
> - To view the diagnostic insights, click on the red dots **(3)** on time series visualizations, which represent detected anomalies and select the link **To incident hub**. 
>
> - Spend a few minutes to change some parameters inside the **Metric-level configuration** section and observe the change of reported anomalies (red points) on the series data representation.

5. In the metrics browser page, select the **Incidents** tab and click on the **Dimension filter**(1) to see the incidents related to number of cases that required hospitalization **hosp_ym = Yes**(2) and **Confirm**(3). 

    ![Filter incidents by hospitalization steps](./media/AI-metric-advisor-filter.png)

6. From the list select the anomaly reported for SUM of hospitalized cases.
    
    ![Filter incidents by hospitalization](./media/AI-metric-advisor-sum-yes.png)

## Task 6 - Perform root cause analysis

1.  In the incidents hub, notice the **Root cause** section where you should find reported the main contributors for the detected anomaly, age groups that contributed to the sum of cases reported as anomaly. Also, in the **Diagnostic** tree, hover on each age group node to investigate its contribution to the incident.
    ![Incident Hub diagnostics](./media/root_cause_incidents_hub1.png)

2.  In the **Diagnostics** (1) section, navigate to **Metrics drill-down** (2) and notice the current point Value (number of cases) and the **Diff**  from the identified **Baseline** (3). Choose the **age_group** dimension to drill-down by it and check the same **Delta** percent and **Diff** value from the baseline for the anomalies detected in the current point. 

     ![Metrics drill down](./media/metricdrill1.png)

    ![Metrics drill down](./media/metrics-drill-down1.png)


## Task 7 - Explore anomalies with hard thresholds (optional)

As an optional exercise, you can create a different detection configuration, based on hard thresholds rather than smart detection.

To do this, go back to the metric detection configuration screen and try a new configuration as follows **(1)**:

- **Hard threshold**
- Value **Out of range** Min: **1000** and Max: **9000** is an anomaly
- Do not report anomaly until 100% of latest **10** points are detected as anomalies

We should have marked as anomalies the points in time where number of cases is bellow or above a fixed threshold for 10 continous points in time.(Notice the yellow dots **(2)** before the reported anomalies and how the threashold is delimited by the red horizontal lines **(3)**).

![Hard threshold](./media/AI-metric-advisor-hardthreshold.png)


## Task 8 - Configure metrics and fine tune detection configuration

### Metrics

1. To browse the metrics for a specific data feed, go to the  **Data feeds**  page and select **covid-ages** from the feeds. This will display a list of metrics associated with it.

    [![Select a metric](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/select-metric.png)](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/select-metric.png#lightbox)

2. Select **count**  to see its details. In this view.

3. When you first view a metric's details, you can load a time series by letting Metrics Advisor choose one for you, or by specifying values to be included for each dimension.

4. You can also select time ranges, and change the layout of the page (1)

5. You can select the  **Incidents**  tab to view anomalies (2).

    ![Metrics drill down](./media/layout-browse.png)

## Task 9 - Tune the detection configuration

1. A metric can apply one or more detection configurations. There's a default configuration for each metric, which you can edit or add to, according to your monitoring needs.

1. The new auto-tuning feature makes this distinction between anomaly types possible. As of now, there are five supported anomaly patterns:
    
    -   Spike
    -   Dip
    -   Increase
    -   Decrease
    -   Steady


- Note

    The auto-tuning feature is only applied on the 'Smart detection' method.

### Subtask 1 - Prerequisite for triggering auto-tuning

1. After the metrics are onboarded to Metrics Advisor, the system will try to perform statistics on the metrics to categorize  **anomaly pattern**  types and  **series value**  distribution. By providing this functionality, you can further fine tune the configuration based on their specific preferences. At the beginning, it will show a status of  **Initializing**.

    [![Screenshot of Metrics Advisor U I with Initializing auto-tuning text visible.](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-initializing.png)](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-initializing.png#lightbox)

### Subtask 2 - Choose to enable auto-tuning on anomaly pattern and series value

The feature enables you to tune detection configuration from two perspectives  **anomaly pattern**  and  **series value**. Based on your specific use case, you can choose which one to enabled or enable both.

-   For the  **anomaly pattern**  option, the system will list out different anomaly patterns that were observed with the metric. You can choose which ones you're interested in and select them, the unselected patterns will have their sensitivity  **reduced**  by default.
    
-   For the  **series value**  option, your selection will depend on your specific use case. You'll have to decide if you want to use a higher sensitivity for series with higher values, and decrease sensitivity on low value ones, or vice versa. Then check the checkbox.
   

[![Screenshot with a toggle button for apply pattern preference and apply value preference selected.](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-preference.png)](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-preference.png#lightbox)

### Subtask 3 - Tune the configuration for selected anomaly patterns

If specific anomaly patterns are chosen, the next step is to fine tune the configuration for each. There's a global  **sensitivity**  that is applied for all series. For each anomaly pattern, you can tune the  **adjustment**, which is based on the global  **sensitivity**.

You must tune each anomaly pattern that has been chosen individually.

[![Screenshot of auto-tuning pattern U I within Metrics Advisor.](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-pattern.png)](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-pattern.png#lightbox)

### Subtask 4 - Tune the configuration for each series value group

After the system generates statistics on all time series within the metric, several series value groups are created automatically. As described above, you can fine tune the  **adjustment**  for each series value group according to your specific business needs.

There will be a default adjustment configured to get the best detection results, but it can be further tuned.

[![Screenshot of pattern based sensitivity U I with adjustment for anomaly patterns, spike -30 highlighted on a slider with a range from -100 to 100.](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-value.png)](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-value.png#lightbox)

### Subtask 5 - Set up alert rules

Even once the detection configuration on capturing valid anomalies is tuned, it's still important to input  **alert rules**  to make sure the final alert rules can meet eventual business needs. There are a number of rules that can be set, like  **filter rules**  or  **snooze continuous alert rules**.

[![Screenshot of setup alert rules UI within Metrics Advisor product.](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-alert.png)](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/autotuning-alert.png#lightbox)

After configuring all the settings described in the section above, the system will orchestrate them together and automatically detect anomalies based on your inputted preferences. The goal is to get the best configuration that works for each metric, which can be achieved much easier through use of the new  **auto-tuning**  capability.

### Subtask 6 - Tune the configuration for all series in current metric

This configuration will be applied to all the series in this metric, except for ones with a separate configuration. A metric level configuration is applied by default when data is onboarded, and is shown on the left panel. Users can directly edit metric level config on metric page.

There are additional parameters like  **Direction**, and  **Valid anomaly**  that can be used to further tune the configuration. You can combine different detection methods as well.

[![Configuration combination](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/configuration-combination.png)](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/configuration-combination.png#lightbox)

### Subtask 7 - Tune the configuration for a specific series or group

Select  **Advanced configuration**  below the metric level configuration options to see the group level configuration.You can add a configuration for an individual series, or group of series by clicking the  **+**  icon in this window. The parameters are similar to the metric-level configuration parameters, but you may need to specify at least one dimension value for a group-level configuration to identify a group of series. And specify all dimension values for series-level configuration to identify a specific series.

This configuration will be applied to the group of series or specific series instead of the metric level configuration. After setting the conditions for this group, save it.

[![Advanced configuration](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/advanced-configuration.png)](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/advanced-configuration.png#lightbox)

### Anomaly detection methods

Metrics Advisor offers multiple anomaly detection methods:  **Hard threshold, Smart detection, Change threshold**. You can use one or combine them using logical operators by clicking the  **'+'**  button.

**Hard threshold**

Hard threshold is a basic method for anomaly detection. You can set an upper and/or lower bound to determine the expected value range. Any points fall out of the boundary will be identified as an anomaly.

**Smart detection**

Smart detection is powered by machine learning that learns patterns from historical data, and uses them for future detection. When using this method, the  **Sensitivity**  is the most important parameter for tuning the detection results. You can drag it to a smaller or larger value to affect the visualization on the right side of the page. Choose one that fits your data and save it.

In smart detection mode, the sensitivity and boundary version parameters are used to fine-tune the anomaly detection result.

Sensitivity can affect the width of the expected value range of each point. When increased, the expected value range will be tighter, and more anomalies will be reported:

![Smart detection with high sensitivity](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/smart-detection-high-sensitivity.png)

When the sensitivity is turned down, the expected value range will be wider, and fewer anomalies will be reported:

![Smart detection with low sensitivity](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/smart-detection-low-sensitivity.png)

**Change threshold**

Change threshold is normally used when metric data generally stays around a certain range. The threshold is set according to  **Change percentage**. The  **Change threshold**  mode is able to detect anomalies in the scenarios:

-   Your data is normally stable and smooth. You want to be notified when there are fluctuations.
-   Your data is normally unstable and fluctuates a lot. You want to be notified when it becomes too stable or flat.

Use the following steps to use this mode:

1.  Select  **Change threshold**  as your anomaly detection method when you set the anomaly detection configurations for your metrics or time series.
    
    ![change threshold](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/change-threshold.png)
    
2.  Select the  **out of the range**  or  **in the range**  parameter based on your scenario.
    
    If you want to detect fluctuations, select  **out of the range**. For example, with the settings below, any data point that changes over 10% compared to the previous one will be detected as an outlier.  ![out of range parameter](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/out-of-the-range.png)
    
    If you want to detect flat lines in your data, select  **in the range**. For example, with the settings below, any data point that changes within 0.01% compared to the previous one will be detected as an outlier. Because the threshold is so small (0.01%), it detects flat lines in the data as outliers.
    
    ![In range parameter](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/in-the-range.png)
    
3.  Set the percentage of change that will count as an anomaly, and which previously captured data points will be used for comparison. This comparison is always between the current data point, and a single data point N points before it.
    
    **Direction**  is only valid if you're using the  **out of the range**  mode:
    
    -   **Up**  configures detection to only detect anomalies when (current data point) - (comparison data point) >  **+**  threshold percentage.
    -   **Down**  configures detection to only detect anomalies when (current data point) - (comparing data point) <  **-**  threshold percentage.

## Task 10 - Preset events

Sometimes, expected events and occurrences (such as holidays) can generate anomalous data. Using preset events, you can add flags to the anomaly detection output, during specified times. This feature should be configured after your data feed is onboarded. Each metric can only have one preset event configuration.

Note

Preset event configuration will take holidays into consideration during anomaly detection, and may change your results. It will be applied to the data points ingested after you save the configuration.

Select the  **Configure Preset Event**  button next to the metrics drop-down list on each metric details page.

![preset event button](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/preset-event-button.png)

In the window that appears, configure the options according to your usage. Make sure  **Enable holiday event**  is selected to use the configuration.

The  **Holiday event**  section helps you suppress unnecessary anomalies detected during holidays. There are two options for the  **Strategy**  option that you can apply:

-   **Suppress holiday**: Suppresses all anomalies and alerts in anomaly detection results during holiday period.
-   **Holiday as weekend**: Calculates the average expected values of several corresponding weekends before the holiday, and bases the anomaly status off of these values.

There are several other values you can configure:

Option

Description

**Choose one dimension as country**

Choose a dimension that contains country information. For example, a country code.

**Country code mapping**

The mapping between a standard  [country code](https://wikipedia.org/wiki/ISO_3166-1_alpha-2), and chosen dimension's country data.

**Holiday options**

Whether to take into account all holidays, only PTO (Paid Time Off) holidays, or only Non-PTO holidays.

**Days to expand**

The impacted days before and after a holiday.

The  **Cycle event**  section can be used in some scenarios to help reduce unnecessary alerts by using cyclic patterns in the data. For example:

-   Metrics that have multiple patterns or cycles, such as both a weekly and monthly pattern.
-   Metrics that don't have a clear pattern, but the data is comparable Year over Year (YoY), Month over Month (MoM), Week Over Week (WoW), or Day Over Day (DoD).



Cycle event is used to reduce anomalies if they follow a cyclic pattern, but it will report an anomaly if multiple data points don't follow the pattern.  **Strict mode**  is used to enable anomaly reporting if even one data point doesn't follow the pattern.

![preset event configuration](https://docs.microsoft.com/en-us/azure/applied-ai-services/metrics-advisor/media/metrics/preset-events.png)

## Task 11 - View recent incidents

Metrics Advisor detects anomalies on all your time series data as they're ingested. However, not all anomalies need to be escalated, because they might not have a significant impact. Aggregation will be performed on anomalies to group related ones into incidents. You can view these incidents from the  **Incident**  tab in metrics details page.

Select an incident to go to the  **Incidents analysis**  page where you can see more details about it. Select  **Manage incidents in new Incident hub**, to find the  page where you can find all incidents under the specific metric.
