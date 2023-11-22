# Lab 4 - Conversational AI with Bot Service using Power Virtual Agents

This lab covers Power Virtual Agents as the hero bot service and demonstrates how to use the Copilot option to create a bot.

## Task 1 - Explore lab scenario

The power of Machine Learning also comes into play when dealing with human-to-machine interfaces. While classical interfaces like native or web applications are ubiquitous, the new approaches based on conversational AI are becoming increasingly popular. Having the capability to interact with intelligent services using natural language is quickly becoming the norm rather than the exception. Using Conversational AI, analysts can find the research of interest by using simple natural language phrases.

With Machine Learning (ML) and Natural Language Processing (NLP), Human Machine Interface (HMI) technologies are enjoying an increased adoption year over year. By 2021, [the growth of chatbots in this space is expected to be 25.07%](https://www.technavio.com/report/chatbot-market-industry-analysis).


The way organizations are building conversational systems is evolving, with bots being built and maintained by a mix of technical and non-technical roles. Power Virtual Agents has the capability to extend its capabilities by allowing pro-code users to create dialogs/topics using the Azure Bot Framework Composer today. This experience allows technical and non-technical teams to build and host their solutions on a single platform.

![Architecture for Lab 4](media/ai-workflow.png)

## Task 2 - Setting up Microsoft Copilot Studio and Create your first Copilot

1. Navigate to **[Microsoft Copilot Studio page](https://www.microsoft.com/en-us/copilot/microsoft-copilot-studio)** and select **Try Free**. 

   ![](media/L4T2S1.png)

3. On the **Let's get you started**, enter your azure username **(1)** and select **Next (2)**. Then click on **Sign in.** 

   ![](media/L4T2S2.png)
   ![](media/L4T2S2.2.png)

5. Once **Signed in**, under Create your account, **choose your respective region (1)** from the drop-down menu and enter phone number and click on **Get Started (2)**.
   
   ![](media/L4T2S3.png)
   
6. Under the **Confirmation details (1)**, click on **Get Started (2)**.

    ![](media/upd-l3-t3-s4.png)

7. You have now successfully signed up for **Microsoft Copilot Studio**.

8. On the **Welcome to Microsoft Copilot Studio (1)** page, choose your respective region and select **Get Started (2)**.

   ![](media/L4T2S6.png)

9. On the **Create a Copilot** page enter the following details:

   - **Copilot name (1)**: Enter **AI-Bot-<inject key="DeploymentID" enableCopy="false"/>**.
   - **What language will your bot speak? (2)**: Select **English (US)** from the dropdown.

   Now select **Create (3)**.

   ![](media/L4T2S7.png)

10. Once the Bot is created you will see the Copilot Studio page.

   ![](media/L4T2S8.png)

## Task 3 - Create a New Topic

1. One the **Microsoft Copilot Studio** page, select **Topics** **(1)**, **Add** **(2)**, click on **Topic** **(3)** from the drop down menu select **Create from description** **(4)**.

   ![](media/L4T3S1.png)

2. In Create it with Copilot pane, Name your topic as **Meal delivery options** **(1)**. In Create a topic to ..., enter the given phrase "**Checking for food options based on the city you are in**" **(2)**, then click on **Create** **(3)**.

   ![](media/cai-l4-t4-s2.png)

3. Once you are in the topic pane, **close** the edit with copilot pane from right-side.

4. On the **topics** pane, click on **+** at the bottom of the **Question** node to **Add node**.

   ![](media/L4T3S4.png)

5. Select **Ask a question** from the drop-down while adding a node.

   ![](media/L4T3S5.png)

6. Enter the question as "**What type of food would you like to order?**" **(1)** and under options for users, click on **New option** **(2)** to add types of food. Add **Chinese** and **Italian** **(3)** as shown in the below screenshot.

    ![](media/cai-l4-t4-s6.png)
   
7. Now under Condition of Chinese, click on **+** to Add node.

   ![](media/cai-l4-t4-s7new.png)

8. Select **Send a message** from the drop-down while adding a node.

   ![](media/cai-l4-t4-s8.png)

9. Enter the Chinese food items given here in the message section: **Noodles, Spring Rolls, Fried Chicken**

   ![](media/cai-l4-t4-s9.png)

10. Now under Condition of Italian, click on **+** to Add node.

    ![](media/cai-l4-t4-s10.png)

11. Select **Send a message** from the drop-down while adding a node.

    ![](media/cai-l4-t4-s11.png)

12. Enter the Italian food items given here in the message section: **Pizza, Pasta, Truffles**

    ![](media/cai-l4-t4-s12.png)

13. Review the topic trigger, and click on **Save** from the right-top corner to save the topic.

    ![](media/cai-l4-t4-s13new.png)

## Task 4 - Test your Copilot

1. Once the Topic is saved, click on **Test Copilot** from the right-top corner.

   ![](media/L4T4S1.png)

2. In the Test copilot pane, enter the given phrase ```What are my meal delivery options?``` and then enter the city name as ```Seattle```. 

   ![](media/L4T4S2.png)

3. You can select the type of food that you are looking for i.e., Chinese or Italian. 

4. Your chatbot should display the names of the meals as shown below.

   ![](media/L4T4S4.png)

Now you have successfully created and tested the Microsoft Copilot.
