# Exercise 3 - Extending standard DM business processes using the Production Process Designer and related apps

In this exercise, we will extend SAP DM with a custom business process. 
Let's assume that we have a business requirement as below:
1. We have some orders where we'd like to automatically release more quantity for execution in case the current work in progress gets scrapped.
2. The above is applicable only to some orders which have to be tagged suitably.
3. We will use the Custom Data capabilities in SAP DM to tag the orders that need this functionality.
4. We will use the Production Process Designer to create a custom business process that will be triggered when the above condition is met.
5. We will then invoke this production process using an automatic trigger on scrap of an SFC

## Exercise 2.1 Create sample orders for our tests using **Manage Orders** app

1. Open the SAP Digital Manufacturing UI in your browser.
2. Go to the app **Manage Orders**. _Tip - Use the Search at the top of the UI to find the app_.
3. Go into an existing order or create a new order. Note that you can Copy an order to create a new order.
4. Go to the **Custom Data** tab.
5. Set the value of the Data Field **Auto Release on Scrap** to **true**.
6. Save the order.
7. Release a quantity of 10 for this order using the **Release In Backgroud** button.
8. Create another order following the steps above. Set the value of the Data Field **Auto Release on Scrap** to **false**.
9. Release a quantity of 10 for this order using the **Release In Backgroud** button.

## Exercise 2.2 Create a Production Process using **Production Process Designer** app that implements the custom logic for our requirement

1. Open the SAP Digital Manufacturing UI in your browser.
2. Go to the app **Design Production Processes**. _Tip - Use the Search at the top of the UI to find the app_
3. Click on the **Create** button
4. Provide the mandatory details in the **Create Production Process Design** dialog box.
   - **Name** - Enter a Name for the Production Process Design. For example, **User_Exercise3**.
   - **ID** - Enter an ID for the Production Process Design. For example, **User_Exercise3**.
   - **Description** - Enter a Description for the Production Process Design(Optional). For example, **PPD created for Exercise 3 for TechEd2023-DT160**
   - **Version** - Enter a Version for the Production Process Design. Keeping the default value is recommended.
5. Click on the **Create** button
   1. This will create a **Production Process Design**. A Production Process Design can have one or more Production Processes in it.
6. Click on the **Create** button on the Welcome tab. Alternatively, you can click on the **+** icon on the right-hand side of the screen
7. Provide the mandatory details in the **Create Production Process** dialog box
   - **Name** - Enter a Name for the Production Process. For example, **User_Exercise3**
   - **ID** - Enter an ID for the Production Process. For example, **User_Exercise3**
   - **Description** - Enter a Description for the Production Process (Optional). For example, **PPD created for Exercise 3 for TechEd2023-DT160**
   - **Runtime Type** - Select **Cloud** from the drop-down list.
   - **Runtime Environment** - Will be automatically set to DMC_Cloud on selection of the Runtime Type as Cloud.
8. Click on the **Create** button
   1. You will be taken to the **Cloud Process** tab. This is where you will design the Production Process.
   2. 

## Summary

You now have a basic understanding of the apps that support the Production Process Designer. You can now proceed to Exercise 3 where we put all of these learnings to practise.

Continue to - [Exercise 4 - Excercise 4 ](../ex4/README.md)
