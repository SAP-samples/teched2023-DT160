# Exercise 4 - Extension capabilities in Manufacturing Insights

## Exercise 4.1 Creating a dashboard using Embedded SAP Analytics Cloud _(eSAC)_ capabilities in SAP Digital Manufacturing

In this exercise, we will create a dashboard using the **Manage Dashboards** app in SAP Digital Manufacturing.

1. Open the SAP Digital Manufacturing UI in your browser.
2. Go to the app **Manage Dashboards**. _Tip - Use the Search at the top of the UI to find the app._
3. Click on the **Create** button to create a new dashboard.
4. This opens the Query Designer in eSAC.
5. On the right-hand side panel, you'll notice the list of available data sources in the form of **Manufacturing Data Objects (MDOs)**
6. Expand the **Manufacturing Data Objects** and notice the list of available MDOs.
7. Drag and Drop the **SFCProductionEvents** MDO onto the canvas.
8. Click on the **SFCProductionEvents** tile on the canvas and click the **Select columns** icon ![](images/SelectColumns.png)
9. Check all of the available columns and click outside the dialog to close it.
10. _Optional_ Select the filter options and apply the plant filter to filter the results only for the plant assigned to you for the exercise
11. Click on the **Preview Query** button at the bottom right-hand side of the UI
12. This will show you the data that will be fetched by the query
13. Click on Finish. Provide a name to the Datasource in the dialog that opens, e.g. User_Exercise4_Query and click on **Save**.
14. This now takes you to the designer to create the dashboard/story.
15. Select the **Table** visualization
16. In the **Builder** panel on the right-hand side, click on the **+ Add Measures/Dimensions** link
    1. Select the below Dimensions
       1. Plant
       2. Order
       3. Sfc
       4. Material
       5. EventType
       6. EventOccurredAt
       7. Routing
       8. RoutingStep
       9. OperationActivity
       10. Resource
    2. Select the below Measures
       1. Quantity
17. You will observe the table getting updated with the selected columns
18. In order to simplify our report, let's add a few filters as well
19. From the top menu, select **Add Story Filter/Prompt**. This will add a filter to the top/left of the page. _Note that you may have to click on **More** and then **Add Story Filter/Prompt** if the option is not visible._
20. Click on the Filter icon and provide the filtering criteria as below:
    1. Dimensions --> Plant
       1. In the **Set Filters for Plant** dialog, select  **All Members** and click on **OK**
    2. Dimensions --> Order
       1. In the **Set Filters for Order** dialog, select  **All Members** and click on **OK**
    3. Dimensions --> Sfc
       1. In the **Set Filters for Sfc** dialog, select  **All Members** and click on **OK**
21. Click on the **Plant** filter and select the plant assigned to you for the exercise. Click on **Apply Selection**
22. From the top menu, select **Save*. This will open a dialog to provide a name and description for the dashboard/story. _Note that you may have to click on **More** and then **Save** if the option is not visible._
23. Provide a name and description for the dashboard/story and click on **Save**.
24. Click on the **SAP** logo on the top left of the UI to take you to the home screen.
25. Click on the **Manage Dashboards** app to see the list of available dashboards.
26. Click on the dashboard/story that you just created to view the dashboard.
27. You can now explore the dashboard and the data that is displayed in the table.
28. Set the filters for the Plant, Order and SFC to the values assigned to you for the previous exercises.
29. Verify the data displayed in the table with the interactions performed via the Workcenter POD in the previous exercises.
30. _Optional_ You can also explore the other MDOs and visualizations available in eSAC to create your own dashboards.

## Exercise 4.2 Explore the APIs on Manufacturing Data Objects

SAP Digital Manufacturing also provides the ability to use APIs to retrieve the data in MDOs and use it in custom apps. 
In this exercise, we'll use a client like Postman to explore the APIs available on the MDOs.

1. Open Postman 
2. Create a new request in a collection or scratchpad
3. Select the **Get** method
4. Use the url: https://api.test.eu20.dmc.cloud.sap/dmci/v1/extractor/$metadata?format=json
5. Set the Authorization as below:
   1. Type: **OAuth 2.0**
   2. Token: **TechEdSessionToken**
   3. In the __Configure New Token__ section, enter the details as below:
      1. Grant Type: **Client Credentials**
      2. Access Token URL: __Will be shared during the session__
      3. Client ID: __Will be shared during the session__
      4. Client Secret: __Will be shared during the session__
      5. Details for Public API Invocation 
         1. API URL: https://api.test.eu20.dmc.cloud.sap/dmci/v1/extractor/$metadata?format=json
         2. Authentication URL: https://dmcazqualityhc1.authentication.eu20.hana.ondemand.com/oauth/token
         3. Client ID: sb-b0dfa869-dab6-4d00-a00b-ef5addb18454!b1472|dmc-services-quality!b330 
         4. Client Secret: 69efe16f-6937-4085-9f3d-c516692d6b40$Aaa_8ecjdKmB1-SXv05khNRMi8MKopsLgx1Nan0Fq9g=

6. Click on **Get New Access Token** to execute the request
7. Click on **Proceed** in the dialog that opens
8. Click on **Request Token** in the dialog that opens
9. Click on **Send** to execute the request
10. You should see a response with the metadata for the available OData endpoints for the MDOs
11. Duplicate the request and change the request url to: https://api.test.eu20.dmc.cloud.sap/dmci/v1/extractor/SFCProductionEvents?format=json&$filter=(Plant eq 'TE1')
    1. **Note: Update the filter as per the plant assigned to you for the session**
12. You should see a response with the data for the SFCProductionEvents MDO
13. You can now explore the other MDOs and APIs available in SAP Digital Manufacturing
## Summary

You now have hands-on experience on building custom dashboards using the embedded SAP Analytics Cloud capabilities in SAP Digital Manufacturing. 
You also have an understanding of the APIs available on the Manufacturing Data Objects that can be used to build custom applications/dashboards/reports.

