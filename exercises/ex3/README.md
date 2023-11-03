# Exercise 3 - Extending standard DM business processes using the Production Process Designer and related apps

In this exercise, we will extend SAP DM with a custom business process. 
Let's assume that we have a business requirement as below:
1. We have some orders where we'd like to automatically release more quantity for execution in case the current work in progress gets scrapped.
2. The above is applicable only to some orders which have to be tagged suitably.
3. We will use the Custom Data capabilities in SAP DM to tag the orders that need this functionality.
4. We will use the Production Process Designer to create a custom business process that will be triggered when the above condition is met.
5. We will then invoke this production process using an automatic trigger on scrap of an SFC

## Exercise 3.1 Create sample orders for our tests using **Manage Orders** app

1. Open the SAP Digital Manufacturing UI in your browser.
2. Go to the app **Manage Orders**. _Tip - Use the Search at the top of the UI to find the app_.
3. Go into an existing order or create a new order. Note that you can Copy an order to create a new order.
4. Go to the **Custom Data** tab.
5. Set the value of the Data Field **Auto Release on Scrap** to **true**.
6. Save the order.
7. Release a quantity of 10 for this order using the **Release In Background** button.
8. Create another order following the steps above. Set the value of the Data Field **Auto Release on Scrap** to **false**.
9. Release a quantity of 10 for this order using the **Release In Background** button.

## Exercise 3.2 Create a Production Process using **Production Process Designer** app that implements the custom logic for our requirement

In this exercise, we'll create a production process that implements the logic as:
1. Take a production process with input as Plant, Order and Quantity
2. Retrieve the Order Details
3. Check if the Order has the Custom Data Field **Auto Release on Scrap** set to **true**
4. If yes, then release the same quantity as the quantity in the input

To achieve the above, the below steps need to be performed:

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
   2. Drag and drop the control **Start** from the **Controls** section on the left-hand side of the screen to the canvas.
   3. Click on the **Manage Parameters** button
   4. In the dialog that opens, click on the **Create** button and add the below parameters one by one
      1. PLANT - String - Required
      2. ORDER - String - Required
      3. QUANTITY - Double - Required
   5. Click on the **Save** button
   6. Drag and drop the service **Retrieve Order Detail** from the **Services and Processes** section on the left-hand side of the screen and drop it on the canvas. You can find it under DMC_Cloud -> DMC -> Order.
   7. Click on the **Start** control on the canvas. You will see ![Connector](../ex1/images/Connector.png) icon that enables you to link the different steps in the process
      1. Click on the **Connector** icon and drag it to the **Retrieve Order Detail** service
   8. Click on the **Retrieve Order Detail** service on the canvas to select it
   9. On the **INPUT** tab on the right-hand side of the screen, map the input parameters of the service to the parameters of the **Start** control
      1. plant - PLANT
      2. order - ORDER
   10. Click on the **Save** button under Cloud Processes tab
   11. Drag and drop the service **Release Order** from the **Services and Processes** section on the left-hand side of the screen and drop it on the canvas. You can find it under DMC_Cloud -> DMC -> Order.
   12. Click on the **Retrieve Order Detail** service on the canvas. 
   13. On the **INPUT** tab on the right-hand side of the screen, map the input parameters of the service to the parameters of the **Start** control
       1. plant - PLANT
       2. order - ORDER
       3. quantityToRelease - QUANTITY
   14. Drag and drop the control **Condition** from the **Controls** section on the left-hand side of the screen to the canvas.
   15. Drag and drop the control **End** from the **Controls** section on the left-hand side of the screen to the canvas.
   16. Click on the **Retrieve Order Detail** control on the canvas. You will see ![Connector](../ex1/images/Connector.png) icon that enables you to link the different steps in the process 
       1. Click on the **Connector** icon and drag it to the **Condition** control
   17. Click on the **Condition** control on the canvas. Click on the **Connector** icon and drag it to the **Release Order** service.
   18. Click on the **Condition** control on the canvas. Click on the **Connector** icon and drag it to the **End** control.
   19. Click on the **Release Order** service on the canvas to select it. Click on the **Connector** icon and drag it to the **End** control.
   20. Click on the **Condition** control on the canvas to select it.
       1. On the **Condition** tab on the right-hand side of the screen, provide the Evaluation Expression **(1)** as
          1. 'Service_Retrieve_Order#customValues[0]["attribute"]' =="AUTO_RELEASE_ON_SCRAP"  and  'Service_Retrieve_Order#customValues[0]["value"]' == "true"
          2. __Note that the above expression can be formed on the UI by selecting the suitable operators and operands from the popup that appears when you click on the ![Browse](images/F4HelpIcon.png)__
          3. This expression checks if the Order has the Custom Data Field **Auto Release on Scrap** set to **true**
       2. On the **Condition** tab on the right-hand side of the screen, provide the **True** Expression **(2)** as
          1. Else
          2. __Note that the above expression can be formed on the UI by selecting **Else** checkbox from the popup that appears when you click on the ![Browse](images/F4HelpIcon.png)__
   21. Click on the **Save** button under Cloud Processes tab
   22. Click on the ![icon](../ex1/images/More%20options.png) to open the menu with additional options
       1. Click on the **Edit Header** option
       2. In the dialog that opens, click set the **Publish to Service Registry** toggle to **ON**
       3. Click on the **Save** button
   23. On the top right of the UI, click on the **Quick Deploy** button
       1. In the dialog that opens, click on the **Deploy and Activate** button
       2. A toast message will inform on the status of the deployment
   24. Run/Debug using the order created in Exercise 3.1
   25. Once successfully tested for both the conditions for the two orders created, you can proceed to the next exercise

## Exercise 3.3 Trigger the Production Process using the Manage Automatic Triggers

In this exercise, we'll configure the Manage Automatic Triggers app with a business rule that enables the production process to be invoked when the SFC is scrapped.

1. Go to the app **Manage Automatic Triggers**. _Tip - Use the Search at the top of the UI to find the app_.
2. Under the Business Rules tab, click on **Create**.
3. Set the below properties as:
   1. Name - **User_Exercise3_TriggerOnScrap**
   2. Trigger Type - **Event**
   3. Event Type - **SFC Scrapped (Deprecated)**
   4. Condition - __Will be automatically filled with a default condition for plant__
   5. Action Item - **Production Process Created in Exercise 3.2**
4. Map the Input Parameters as below
   1. ORDER - order.order
   2. PLANT - plant
   3. QUANTITY - sfcs[0].quantity
5. Click on the **Save** button
6. Click on the **Quick Deploy** button

## Exercise 3.4 Test End to End with the Work Center POD 

1. Setting up Non Conformance Codes to be used in the Work Center POD
2. Go to the app **Manage Nonconformance Codes**. _Tip - Use the Search at the top of the UI to find the app_.
3. Search for the Nonconformance Code **SCRAPPED** and click on the row to go to the details of the Nonconformance Code
4. Set **Can Be Primary Code** to **Yes**
5. Assign **Nonconformance Disposition Routing** to **SCRAP**
6. CLick on **Save**
7. Go to the app **Work Center POD (Default)**. _Tip - Use the Search at the top of the UI to find the app_.
8. Select the Work Center **WC-LIFT** and the Resource **ARCWELD-3** from the dialogues that open when clicking on the respective input fields and click on **Go**
9. The Work List will show a list of SFCs that are available for work based on the selection criteria
10. Select a SFC from the list and click on the **Start** button
11. Click on the **Nonconformance** button
    1. This opens the NC Selection plugin and the Nonconformance Data Entry plugin
    2. On the left-hand side panel of the NC Selection plugin, select the **All** Nonconformance Group
    3. On the right-hand side panel of the NC Selection plugin, click on the **Log NC** button in the row for the Non Conformance code **SCRAPPED**
    4. In the Nonconformance Data Entry plugin, click on **Add** and then click on **Done**
12. Go to the app **Manage Orders**. _Tip - Use the Search at the top of the UI to find the app_.
13. Select the Order that was used in the previous steps and click on the row to go to the details of the order
14. Notice the change in the **Available Quantity to Release**. It should be updated as per the logic in the production process defined in the earlier exercise
15. Try the steps above for another SFC belonging to an order where the **Auto Release on Scrap** is set to **false**. Notice that the **Available Quantity to Release** is not updated
16. You can now proceed to the next exercise
       

## Summary

You now have hands-on experience with designing and running End to End integrated extensions using the Production Process Designer capabilities in SAP Digital Manufacturing. You can now proceed to Exercise 4 where we design a custom dashboard/report.

Continue to - [Exercise 4 - Excercise 4 ](../ex4/README.md)
