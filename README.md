# Scrape, Analyze and Visualize insights on Startups using Watson Studio

Being in the age of start-ups. There is a rapid increase in a number of companies providing skilled services. We can scrape information about such companies and evaluate their success stories based on the number of articles or live use cases appeared in news portals.

This Code Pattern provides a tool that extracts live unstructured data about Startups and the impact they create in the industry with the help of Watson Natural Language Understanding, fed into IBM SPSS Predictive Analytics to get meaningful insights and predictions, finally fed into Cognos Dashboard which provides insights and visualisation from the provided input.


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
6. Finally, Cognos ingests, the final table generated in DB2 Warehouse giving insightful visualisation.

<!--Optionally, update this section when the video is created-->
# Watch the Video

Insert Video

# Prerequisites
* [Insert Scrape Data Tutorial]
* [Insert SPSS Tutorial]

# Steps

1. [Setup the Notebook on your Watson Studio Project](#1-setup-the-notebook-on-your-watson-studio-project)
2. [Setup the SPSS Modeler on your Watson Studio Project](#2-setup-the-spss-modeler-on-your-watson-studio-project)
3. [Setup the Embedded Dashboard on your Watson Studio Project](#3-setup-the-watson-embedded-dashboard-on-your-watson-studio-project)

## 1. Setup the Notebook on your Watson Studio Project

* Once, you have created your Waston Studio Project, click on `Add Notebook`>`From URL` and copy this URL- 
* Ensure you have created and copied the Watson Natural Language Understanding Service as instructed in the [tutorial](https://github.com/smruthi33/Scrape_Data), and paste the service credentials in your notebook in the cell below `2.1 Add your service credentials from IBM Cloud for the Watson services` section.

![](doc/source/images/NLU_credentials_notebook.png)

* Ensure you have created and connected your DB2 Warehouse instance to the current Watson Studio Project as instructed in the [tutorial](https://github.com/smruthi33/-Set-up-SPSS-Modeler-on-Watson-Studio-with-DB2-Warehouse-connection.), and insert the credentials in the section `2.2 Add your service credentials for DB2`. Ensure the credentials is saved as `credentials_1`.

![](doc/source/images/DB2_Warehouse_Credentials.png)

* Run the notebook. 

```Note: Since Data is being Scraped from the Web. Certain cells in the notebook will take some time to execute.```

## 2. Setup the SPSS Modeler on your Watson Studio Project

* Download the stream file from the repo- `Insert Stream link`
* Open your Watson Studio from IBM Cloud Dashboard and Navigate to the created project.
* Click on the `Add to Project` button and select `Modeller Flow`.

![](/doc/source/images/modeller_connection.png)

* Click on the `From File` tab and upload the downloaded stream file.

![](/doc/source/images/upload_modeller_file.png)

* Double Click on the `Data Asset` node and click on the `Change Data Asset` button.
* Move to `Connection` tab and select the `DB2 Warehouse` and select the correct `Schema` (usually starting with DASH) and the created table- `DATA_FOR_SPSS`.

![](/doc/source/images/add_DB2_Data_Asset.png)

# Sample output

![](doc/source/images/sample_output.png)

<!--Optionally, include any troubleshooting tips (driver issues, etc)-->

# Troubleshooting


## License

This code pattern is licensed under the Apache License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1](https://developercertificate.org/) and the [Apache License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache License FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)
