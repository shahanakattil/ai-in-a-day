# Lab 5 - Machine Learning with Azure Databricks

The lab covers Data Engineering and Machine Learning using Azure Databricks notebooks.

## Task 1 - Explore dashboard of COVID-19 data

Understanding the source datasets is very important in AI and ML. To help you expedite the process, we have created a Power BI dashboard you can use to explore them at the begining of each lab.

![Azure AI in a Day datasets](../media/data-overview-01-01.png)

To get more details about the source datasets, check out the [Data Overview](https://github.com/CloudLabsAI-Azure/ai-in-a-day/blob/main/data-overview.md) section.

To explore the dashboard of COVID-19 data, open the `Azure-AI-in-a-Day-Data-Overview.pbix` file located on the desktop of the virtual machine provided with your environment.

## Task 2 - Explore lab scenario

When data comes in natural language, a data engineering process should transform it into a numerical form useful in Machine Learning. In most cases, some input values will be off (e.g., resulting from human error) or even missing. The same process should be able to identify and handle these cases. Furthermore, analysts need to perform exploratory analysis and various other consistency checks to gain a deep understanding of the data and ensure a level of quality that makes it fit for Machine Learning.

Using Azure Databricks, we will prepare input datasets and analyze their content. We will also attempt to correlate the various datasets and clean their content. We will assess the resulting data quality using both statistical and Machine Learning-based approaches.

The following diagram highlights the portion of the general architecture covered by this lab.

![Architecture for Lab 6](./../media/Architecture-6.png)

The high-level steps covered in the lab are:

- Explore dashboard of COVID-19 data
- Explore lab scenario
- Explore source data and identify potential issues
- Perform data cleansing on research paper dataset and explore results
- Perform data cleansing on case surveillance data and explore results
- Correlate research paper and case surveillance datasets
- Use SparkML to build risk classifier on case surveillance dataset
- Assess fairness of risk classifier

## Task 3 - Start your Azure Databricks environment

1. Open the [Azure Portal](https://portal.azure.com) and sign-in with your lab credentials.

2. Navigate to your resource group `AI-in-a-Day` and locate the Azure Databricks workspace and select **launch workspace**. If you are prompted to sign-in again, use the same lab credentials you used at the previous step.

  ![Open Azure Databricks Workspace](media/rg-databricks.png)

  ![Open Azure Databricks Workspace](media/launch-workspace.png)

3. In the Azure Databricks workspace, select the `Compute` section on the left side menu.

  ![select compute](media/select-compute-not-cluster.png)

4. Under **All-purpose clusters** select the first cluster from the list, and then select `Start` to start the Azure Databricks cluster.

  ![Select Azure Databricks Cluster](media/select-compute-1.png)

  ![Start Azure Databricks Cluster](./media/start-databricks-cluster.png)

5. While the cluster is starting, select the `Workspace` section on the left side menu, select the `Users` folder, then select the folder corresponding to the user name from your lab credentials, and then select the `AI-in-a-day-Lab-6` folder.

  ![Open Azure Databricks workspace folders](media/user-select-1.png)

6. In the `AI-Lab6` folder, you should see the three notebooks that you will use in this lab.

  ![View list of notebooks in Azure Databricks workspace](./media/databricks-workspace-2.png)

7. Wait until the cluster starts, then proceed to the next tasks in the lab.

## Task 4 - Explore the surveillance dataset

1. With the Azure Databricks workspace opened and the cluster fully started, select the `1-explore-surveillance-dataset` notebook.
  
  ![View list of notebooks in Azure Databricks workspace](media/select-notebook-databricks.png)
  
2. On the `1-explore-surrveillance-dataset` notebook, click on the dropdown and select `ai-adb-lab` cluster and attach it. Ensure the notebook is connected to the running cluster.

  ![Attach cluster to the notebook](media/attach-cluster-to-notebook.png)

  ![Ensure notebook is connected to running cluster](./media/notebook1.png)

3. Execute each cell in the notebook (using Ctrl + Enter to remain on the same cell, or Shift + Enter to advance to the next cell, or **(1) selecting the arrow to run the cell**) and observe the **(2) results**.

  ![Run first cell](media/run-cell-1.png)

## Task 5 - Build a risk classifier based on surveillance data (optional)

1. With the Azure Databricks workspace opened and the cluster fully started, select the `2-surveillance-risk-classifier` notebook.

2. Ensure the notebook is connected to the running cluster.

![Ensure notebook is connected to running cluster](media/attach-cluster-to-notebook.png)

![Ensure notebook is connected to running cluster](./media/notebook2.png)

3. Execute each cell in the notebook (using either Ctrl + Enter to remain on the same cell, or Shift + Enter to advance to the next cell) and observe the results.

## Task 6 - Explore the research papers dataset (optional)

1. With the Azure Databricks workspace opened and the cluster fully started, select the `3-explore-research-paper-dataset` notebook.

2. Ensure the notebook is connected to the running cluster.

![Ensure notebook is connected to running cluster](./media/notebook3.png)

3. Execute each cell in the notebook (using either Ctrl + Enter to remain on the same cell, or Shift + Enter to advance to the next cell) and observe the results.

