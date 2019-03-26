# Scrape, Analyze and Visualize insights on Startups using Watson Studio

Being in the age of start-ups. There is a rapid increase in a number of companies providing skilled services. We can scrape information about such companies and evaluate their success stories based on the number of articles or live use cases appeared in news portals.

Suppose, we want to understand the current startups in a particular technology, say Machine Learning, this code pattern will evaluate its impact in the industry, on the basis of-

* How many times it has appeared on News?
* Whether it has a Wikipedia page or not?
* Whether they have Tech blogs or not?
* Whether they are active on Social Media (Twitter, Medium, etc..)?

This unstructured data once scraped(extract information from web) is processed through Watson NLU and converted to structured data. This is fed to SPSS, which can be used to understand the data and perform Analytics to determine if all the factors(as mentioned above) appear in a company, thereby computing a popularity score. Once, all the Analytics is performed this Code Pattern also provides a user friendly and interactive Dashboard visualisation of the data, giving insights of the data and complete ease to simplify the decision making process.

```
Note: The Company Names have been Anonymised and replaced with names of Plants. 
This Pattern does not wish to put down any Company, only provides a methodology to perform Analytics
on any Data from the Web.
```

When the reader has completed this Code Pattern, they will understand how to:

* Create and Run a Python Notebook on Watson Studio.
* Scrape data using BeautifulSoup.
* Use Watson Natural Language Understanding to extract metadata from Python Notebook.
* Generate a csv and Convert to a Table in DB2 Warehouse.
* Load and analyze data in SPSS Modeler.
* Load and Visualize data in Cognos Dashboard.


<!--add an image in this path-->
![](doc/source/images/Architecture_Diagram.png)

<!--Optionally, add flow steps based on the architecture diagram-->
## Flow

1. The user creates and runs a Python Notebook on Watson Studio.
2. The Notebook scrapes latest news on Startups.
3. The Scraped Information is sent to Watson Natural Language Understanding to extract Keywords, Entities, Sentiments and its respective confidence scores.
4. The Results of NLU are compiled into a csv file which is further converted to a table in DB2 Warehouse.
5. The table created is ingested in SPSS to do some analytics and return a score against each company. The updated table is then saved back to DB2 Warehouse.
6. Finally, the table generated in DB2 Warehouse is fed to the Dashboard, giving insightful visualisation.

<!--Optionally, update this section when the video is created-->
# Watch the Video

[![](https://img.youtube.com/vi/AqX9D2I9nJw/0.jpg)](https://www.youtube.com/watch?v=AqX9D2I9nJw)

# Prerequisites
* [Scrape data from the web using Python and AI](https://developer.ibm.com/tutorials/scrape-data-from-the-web-using-watson-studio/)
* [Predictive analytics using SPSS with database warehouse connection](https://developer.ibm.com/tutorials/set-up-spss-modeler-on-watson-studio-with-db2-warehouse-connection/)
* In the file- [company_list](https://github.com/IBM/analyze-insights-on-startup-using-watson-studio/blob/master/companies_list.json). Fill up information about the companies by replacing in the same format as the given template-

![](doc/source/images/company_list_template.png)

# Steps

1. [Setup the Notebook on your Watson Studio Project](#1-setup-the-notebook-on-your-watson-studio-project)
2. [Setup the SPSS Modeler on your Watson Studio Project](#2-setup-the-spss-modeler-on-your-watson-studio-project)
3. [Setup the Embedded Dashboard on your Watson Studio Project](#3-setup-the-embedded-dashboard-on-your-watson-studio-project)

## 1. Setup the Notebook on your Watson Studio Project

* Once, you have created your Waston Studio Project, click on `Add Notebook`>`From URL` and copy this URL- https://github.com/IBM/analyze-insights-on-startup-using-watson-studio/blob/master/code/Scrape_Startup_Insights.ipynb
* Ensure you have created and copied the Watson Natural Language Understanding Service as instructed in the [Scrape data from the web using Python and AI](https://developer.ibm.com/tutorials/scrape-data-from-the-web-using-watson-studio/), and paste the service credentials in your notebook in the cell below `2.1 Add your service credentials from IBM Cloud for the Watson services` section.

![](doc/source/images/NLU_credentials_notebook.png)

* Ensure you have created and connected your DB2 Warehouse instance to the current Watson Studio Project as instructed in the [Predictive analytics using SPSS with database warehouse connection](https://developer.ibm.com/tutorials/set-up-spss-modeler-on-watson-studio-with-db2-warehouse-connection/), and insert the credentials in the section `2.2 Add your service credentials for DB2`. Ensure the credentials is saved as `credentials_1`.

![](doc/source/images/DB2_Warehouse_Credentials.png)

* In your `credentials_1` variable note down the `username` field, like DASHXXXX. This will be later used in various instances in this pattern.
* On the top right corner click on the `10/01` tab and click on `browse`. Download the file- [company_list](https://github.com/IBM/analyze-insights-on-startup-using-watson-studio/blob/master/companies_list.json) and upload this file from your file system.
* In section 3 of the notebook, the cell under ` Insert Pandas Dataframe of the company_list.json file`. Ensure the dataframe is saved as `df_data_1`.
* In the notebook go to the last section `Store and Add table in DB2 Warehouse`, and replace DASHXXXX with the your Schema name-

![](/doc/source/images/notebook_config.png)

* Run the notebook. 

```Note: Since Data is being Scraped from the Web. Certain cells in the notebook will take some time to execute.```

## 2. Setup the SPSS Modeler on your Watson Studio Project

* Download the stream file from the repo- https://github.com/IBM/analyze-insights-on-startup-using-watson-studio/blob/master/code/Analyze_Startup_Data.str
* Open your Watson Studio from IBM Cloud Dashboard and Navigate to the created project.
* Click on the `Add to Project` button and select `Modeller Flow`.

![](/doc/source/images/modeller_connection.png)

* Click on the `From File` tab and upload the downloaded stream file.

![](/doc/source/images/upload_modeller_file.png)

* Once, the modeler is opened. Double Click on the `Data Asset` node and click on the `Change Data Asset` button.

![](/doc/source/images/data_import_setup.png)

* Move to `Connection` tab and select the `DB2 Warehouse` and select the correct `Schema` (usually starting with DASHXXXX) and the created table- `DATA_FOR_SPSS`.

![](/doc/source/images/add_DB2_Data_Asset.png)

* Similarly for the final node- `Data_Export` node, follow the same steps as above and select `DATA_FOR_COGNOS` table.

![](/doc/source/images/data_export_setup.png)

* Before saving the changes for the node, make sure the value for `If the datset already exists`- `Append Output to Dataset`, as shown in the image above.

* Run the Modeler Flow, by clicking the play button. The data would now be saved back to your DB2 Warehouse instance.

## 3. Setup the Embedded Dashboard on your Watson Studio Project 

* Download the [file](https://github.com/IBM/analyze-insights-on-startup-using-watson-studio/blob/master/code/Starup_Analytics_Dashboard.json), and open it in any Text Editor.
 1. Search for the term `DASH_SCHEMA_NAME` and replace any occurrences of it with your db2 Warehouse schema name. 
 
  ![](/doc/source/images/json_change_1.jpg)
 
 2. If you have changed the Table name from `DATA_FROM_COGNOS`- search for the term `DATA_FOR_COGNOS` and replace any occurrences of it with your db2 Warehouse table name.

  ![](/doc/source/images/json_change.jpg)

* Go to your Watson Studio Project and click on `Add to Project` button to add the Embedded Dashboard Analytics service.

![](doc/source/images/EDA_Add_to_Project.png)

* Select `From file` option to upload the `modified .json` file and select the dashboard service and then click on save.

![](doc/source/images/export_json_file.png)

If you don't have the `Cognos Dashboard Embedded Service` instance-

* Click on `Associate a Cognos Dashboard Embedded Service Instance`.

![](doc/source/images/new_cognos_instance.png)

* Select `Lite` or `Pay-as-you-go` plan as per your requirement and click on `Create`. 

![](doc/source/images/cognos_setup.png)

* Click on `Reload` and then `Create` button.
* While opening the Dashboard you may receive this pop-up. Click on the `Re-link` button.


![](/doc/source/images/Cognos_error.jpg)

* Next, Click on `Connections`>`DB2 Warehouse`>`Your_Schema`>`DATA_FOR_COGNOS`. This will load the Interactive Dashboard.

# Sample output

This Code Pattern provides a solution-

* That extracts live unstructured data about Startups
* The impact Startups create in the industry with the help of Watson Natural Language Understanding and converted to a structured data.
* The data is then fed into IBM SPSS Predictive Analytics to get meaningful insights and ratings.
* Finally, providing insights and visualisation from the provided input using Watson Embedded Dashboard.

The end-to-end Startup Analytics Dashboard provides users complete insights on startups and showcases the predicted information in the form of charts/widgets using IBM Watson Embedded Dashboard Service which hosted on Watson Studio. 
This enables a user to build their own sophisticated visualizations to communicate the insights from their discovered analytics data, furthermore the created dashboard can be shared among various users.
 
After completing the setup, you will see the dashboard with 4 interactive widgets as follows:

![](doc/source/images/Final_Output.png)


1. Company's Score based on Relevance: A view showing the most popular companies at a larger size than the smaller ones.
2. Total number of articles appeared in the web of a Company: A view showing the factors affecting the popularity of a startup on the web (amongst News Articles, Tech Blogs, Socail Media and so on).
3. News Concept Relevance: Gives a broad overview of main topics of the articles across the companies, by the percentage of its Relevance.
4. News Sentiment Analysis by Company: Gives an overall analysis of the tone in which the article was written, to understand the impact (whether positive or negative or neutral) a given company has in the industry.


# Troubleshooting

See [Troubleshooting.MD](https://github.com/IBM/analyze-insights-on-startup-using-watson-studio/blob/master/TROUBLESHOOTING.md)

## License

This code pattern is licensed under the Apache License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1](https://developercertificate.org/) and the [Apache License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache License FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)
