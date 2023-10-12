# Exercise 2 - Overview of supporting apps for Production Process Designer

In this exercise, we will have a quick dive into the apps that support the Production Process Designer (PPD). 
The below apps will be covered in this exercise:
1. Monitor Production Processes
2. Manage Service Registry
3. Manage Automatic Triggers

Note that the scope of this exercise is to provide a quick overview of the apps and their capabilities. 
All these will be used in Exercise 3

## Exercise 2.1 Overview of **Monitor Production Processes**

After completing these steps you will have the ability to monitor the production processes, track their execution statuses, parameters and investigate issues, if any.

1. Open the SAP Digital Manufacturing UI in your browser.
2. Go to the app **Monitor Production Processes**. _Tip - Use the Search at the top of the UI to find the app_.
3. Notice the filter criteria, especially the Date Range. This is the date range for which the production processes will be displayed.
4. Set suitable filters and click on **Go**.
5. Notice the list of production processes displayed.
6. You should see the ones executed in the previous exercises.
7. Click on a row. This takes you to the details of the production process execution.
8. Click through the steps and notice the details displayed.
9. Notice the icons on the right of the **Detailed Information** section. Click through these to gain a better understanding of the details provided under these sections.
   1. Graphic View - This shows the graphic view of the production process
   2. Log View - This shows the log of the production process execution
   3. Process Parameter View - This shows the input and output parameters of the production process execution

## Exercise 2.2 Overview of **Manage Service Registry**

After completing these steps you will have a better understanding of the workings of PPD and the service registry. You'll gain insights into how the Services and Processes are made available in PPD and how to expose Production Processes as a services.
For the scope of the exercise, the focus will be the API Services

1. Open the SAP Digital Manufacturing UI in your browser.
2. Go to the app **Manage Service Registry**. _Tip - Use the Search at the top of the UI to find the app_.
3. Under the API Services tab, notice the list of services.
4. Click on the drop down for the **Group** filter and notice the list of groups.
   1. The **DMC** group contains the APIs provided by SAP DM
      1. Search for the term **Auto Assemble** and notice the API **Auto Assemble**. This is the API that was used in the previous exercises.
      2. Notice the Group Path. This is the path that we had traversed to select this service in PPD
   2. The **Production Process** group contains the APIs provided by PPD
      1. Use the search to find the Production Process we created in the earlier exercise.
      2. The service being available in the Service Registry is a result of Exercise 1.2
      3. Click on the row to view the details of the service.
      4. Note the URL/Path.
      5. Click on the DMC_Cloud under the Web Server property. This takes us to the details of the Web Server. Note the Host URL from this app.
      6. HostURL/Path is the URL that we can use to invoke the service.
   3. As an optional exercise, you can use a client like Postman to invoke this service
      1. Open Postman
      2. Create a new request
      3. Set the URL to the HostURL/Path noted in the previous step
      4. Set the HTTP Method to POST
      5. Set the Content-Type to application/json
      6. Set the Body to the following JSON
      ```json
      {
        "PLANT": "PlantValue",
        "SFC": "SFCValue",
        "OPERATION": "LA-WELDING",
        "OPERATION_VERSIOn": "ERP001",
        "RESOURCE": "ARCWELD-3"
      }
      ```
      7. Set the Authorization Type to *OAuth 2.0*. The Access Token URL, Client ID and Client Secret can be obtained from the Service Key from BTP Cockpit.
         1. For the exercise, the speakers will share these details. More details on this can be found in the [help documentation](https://help.sap.com/docs/sap-digital-manufacturing/operations-guide/prepare-for-api-integration).
         2. Use these details to obtain the Access Token.
         3. Set the Access Token in the request.
         4. Click on **Send**.
      8. Verify the behavior in the SAP Digital Manufacturing UI. You should see a new production process executed in **Monitor Production Processes**. The business logic of the production process can be verified as on Exercise 1.


## Exercise 2.3 Overview of **Manage Automatic Triggers**

After completing these steps you will have a better understanding of the workings of PPD and the automatic triggers. You'll gain insights into how the automatic triggers are configured and how they are used in SAP DM.
For the scope of the exercise, the focus will be the **Business Rules**

1. Open the SAP Digital Manufacturing UI in your browser.
2. Go to the app **Manage Automatic Triggers**. _Tip - Use the Search at the top of the UI to find the app_.
3. Under the Business Rules tab, click on **Create**.
4. Notice the properties available under the below:
   1. Trigger Type
   2. Event Type
   3. Action Item
5. Various interactions in SAP DM can lead to trigger of events. This app allows to trigger additional business logic when these events are triggered. This is the simplest approach to extend the standard business logic in SAP DM. A Production Produciton process can be the Action Item triggered.
6. We will use all of the above in Exercise 3
7. 
## Summary

You now have a basic understanding of the apps that support the Production Process Designer. You can now proceed to Exercise 3 where we put all of these learnings to practice.

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)
