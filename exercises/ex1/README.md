# Exercise 1 - Create, deploy and run a Production Process

In this exercise, you will create a simple Production Process in SAP Digital Manufacturing.
The Production Process will be used to enhance the standard behaviour of the Complete SFC functionality and add Auto-Assembly as a step that happens before the Complete SFC is performed.

After completing this exercise, you will be able to:
1. **Create** a Production Process
2. **Publish** a Production Process to Service Registry
3. **Deploy** a Production Process
4. **Debug** a Production Process
5. **Run** a Production Process

## Exercise 1.1 - **Create** a Production Process
1. Open the SAP Digital Manufacturing UI in your browser.
2. Go to the app **Design Production Process**. _Tip - Use the Search at the top of the UI to find the app_
3. Click on the **Create** button
4. Provide the mandatory details in the **Create Production Process Design** dialog box.
    - **Name** - Enter a Name for the Production Process Design. For example, **User_Exercise1**.
    - **ID** - Enter an ID for the Production Process Design. For example, **User_Exercise1**.
    - **Description** - Enter a Description for the Production Process Design(Optional). For example, **PPD created for Exercise 1 for TechEd2023-DT160**
    - **Version** - Enter a Version for the Production Process Design. Keeping the default value is recommended.
5. Click on the **Create** button
    1. This will create a **Production Process Design**. A Production Process Design can have one or more Production Processes in it.
6. Click on the **Create** button on the Welcome tab. Alternatively, you can click on the **+** icon on the right-hand side of the screen
7. Provide the mandatory details in the **Create Production Process** dialog box
    - **Name** - Enter a Name for the Production Process. For example, **User_Exercise1**
    - **ID** - Enter an ID for the Production Process. For example, **User_Exercise1**
    - **Description** - Enter a Description for the Production Process (Optional). For example, **PPD created for Exercise 1 for TechEd2023-DT160**
    - **Runtime Type** - Select **Cloud** from the drop-down list.
    - **Runtime Environment** - Will be automatically set to DMC_Cloud on selection of the Runtime Type as Cloud.
8. Click on the **Create** button
    1. You will be taken to the **Cloud Process** tab. This is where you will design the Production Process.
9. Familiarize yourself with the menu options on the left-hand side of the screen.
    1. Hover the mouse over the icons to see the tooltip.
    2. For the exercises in this session, we'll mainly focus on the **Editor**
       <br>![Editor](exercises/ex0/images/PPD - Editor.png)
10. The rest of the screen is used for the canvas where we'll design the Production Process using the controls, services and processes available on the left.
11. Drag and drop the control **Start** from the **Controls** section on the left-hand side of the screen to the canvas.
12. Select the **Start** control on the canvas and click on the **Input Parameters** tab on the right-hand side of the screen.
    1. Click on the **Manage Parameters** button
    2. In the dialog that opens, click on the **Create** button and add the below parameters one by one
        1. PLANT - String - Required
        2. SFC - String - Required
        3. OPERATION - String - Required
        4. OPERATION_VERSION - String - Required
        5. RESOURCE - String - Required
    3. Click on the **Save** button
13. Drag and drop the service **Auto Assemble** from the **Services and Processes** section on the left-hand side of the screen and drop it on the canvas. You can find it under DMC_Cloud -> DMC -> Assembly.
    1. Notice that the input and output parameters of the service are automatically created based on the service definition.
14. Click on the **Start** control on the canvas. You will see ![Connector](../ex1/images/Connector.png) icon that enables you to link the different steps in the process
    1. Click on the **Connector** icon and drag it to the **Auto Assemble** service
15. Click on the **Auto Assemble** service on the canvas to select it
16. On the **INPUT** tab on the right-hand side of the screen, map the input parameters of the service to the parameters of the **Start** control
    1. plant - PLANT
    2. sfcs - SFC (Note - This is a list of SFCs. We'll map the input SFC with the first element of this parameter)
    3. operationActivity - OPERATION
    4. operationActivityVersion - OPERATION_VERSION
    5. resource - RESOURCE
    6. Click on the **Save** button under Cloud Processes tab
17. Drag and drop the service **Complete SFCs** from the **Services and Processes** section on the left-hand side of the screen to the canvas. You can find it under DMC_Cloud -> DMC -> SFC Production Activities.
18. Click on the **Auto Assemble** service on the canvas to select it
    1. Click on the **Connector** icon and drag it to the **Complete SFCs** service
19. Click on the **Complete SFCs** service on the canvas to select it
20. On the **INPUT** tab on the right-hand side of the screen, map the input parameters of the service to the parameters of the **Start** control
    1. plant - PLANT
    2. sfcs - SFC (Note - This is a list of SFCs. We'll map the input SFC with the first element of this parameter)
    3. operation - OPERATION
    4. resource - RESOURCE
21. Drag and Drop the **End** control from the **Controls** section on the left-hand side of the screen to the canvas.
22. Click on the **Complete SFCs** service on the canvas to select it
    1. Click on the **Connector** icon and drag it to the **End** control
23. Click on the **Save** button under Cloud Processes tab

## Exercise 1.2 - **Publish** a Production Process to Service Registry
1. In the Cloud Process tab of the process we created in exercise 1.1, click on the ![icon](../ex1/images/More%20options.png) to open the menu with additional options
    1. Click on the **Edit Header** option
    2. In the dialog that opens, click set the **Publish to Service Registry** toggle to **ON**
    3. Click on the **Save** button

## Exercise 1.3 - **Deploy** a Production Process
1. On the top right of the UI, click on the **Quick Deploy** button
2. In the dialog that opens, click on the **Deploy and Activate** button
    1. A toast message will inform on the status of the deployment

## Exercise 1.3 - **Debug** a Production Process
1. Before we can debug/test/run our production process, we need to set some data in DM so that we can use it for our test purposes
    1. Release SFCs for testing purposes using the Manage Orders app
        1. Open a duplicate tab in the browser and navigate to the **Manage Orders** app
        2. Select an order. This takes you to the Order Details
        3. You can release an order by clicking on the **Release In Background** button in the top right menu
        4. Once the order is released, you can click on the **SFCs** tab to see the list of SFCs created for the order
    2. Open the **Work Center POD (Default)** app. This app allows you to report the work being performed on SFCs
    3. Select the Work Center **WC-LIFT** and the Resource **ARCWELD-3** from the dialogues that open when clicking on the respective input fields and click on **Go**
    4. The Work List will show a list of SFCs that are available for work based on the selection criteria
    5. Select a SFC from the list and click on the **Start** button
    6. Click on the **Component List** tab. You'll notice that there's a component available for assembly, but not yet assembled - indicated by the Remaining Quantity as 1
2. Now, let's test our Production Process in Debug mode
3. In the Design Production Processes app, select the design we had created in the earlier exercises.
4. In the Cloud Process tab of the process we created in exercise 1.1, you'll now be able to see a button that enables us to Debug our Production Process. This is an easy way to test it before we integrate it with other processes/UI/tools
5. Click on **Debug** button
    1. In the dialog that opens, enter the below values for the parameters
        1. PLANT - _Plant assigned to you_
        2. SFC - _SFC started in step 1.5
        3. OPERATION - LA-WELDING
        4. OPERATION_VERSION - ERP001 (Note - This is the Operation Version of the Operation and can be found in the app **Manage Operation Activities**)
        5. RESOURCE - ARCWELD-3
    2. Click on the **Debug** button
        1. A comprehensive debug session is started with the UI showing various parameters, logs, etc.
        2. You can click on the **Next Step** button to move to the next step in the process
            1. Monitor the logs and the values of the parameters
            2. In case of errors, the logs will indicate the errors. An icon will also be displayed next to the step that has the error
            3. In order to fix any errors, you will need to **Edit** the process and fix the errors
                1. This will prompt you to create a new version of the process. You can continue with the default options pre-filled in the dialog in such a scenario
                2. Once you've fixed the errors, you can **Save** and then **Quick Deploy** the process again
                3.
        3. Once all steps are done, click on **Exit Debugging**
6. Now, let's test our Production Process
    1. Click on the **Run** button
        1. Note that you'll need to perform the steps in exercise #1.3 Step 1 before you can run the process as we'll need a new SFC to test it with
    2. In the dialog that opens, enter the below values for the parameters
        1. PLANT - _Plant assigned to you_
        2. SFC - _SFC started in step 6.1.1
        3. OPERATION - LA-WELDING
        4. OPERATION_VERSION - ERP001 (Note - This is the Operation Version of the Operation and can be found in the app **Manage Operation Activities**)
        5. RESOURCE - ARCWELD-3
    3. Click on the **Run** button
7. To verify whether the Auto-Assembly worked, you can go to the **Product Genealogy** app and check the Components tab. Note that the Product Genealogy app is planned for deprecation and the capabilities will be provided in the **SFC Report** app
    1. Alternatively, this information can also be found on the Workcenter POD by choosing the suitable selection criteria
        1. Note that the SFC will be marked as completed on the Operation that was executed in the Production Process

## Summary

Now that you have completed the first exercise, let's have a look at the key apps that enable us monitor and manage the production processes.
Continue to - [Exercise 1 - Exercise 1 Description](../ex1/README.md)
