# Analyze using SPSS

1. [Add the DB2 Warehouse Connection in Watson Studio](#1-add-the-db2-warehouse-connection-in-watson-studio)
2. [Add the SPSS Modeller](#2-add-the-spss-modeller)
3. [Run the SPSS Modeller](#3-run-the-spss-modeller)

### 1. Add the DB2 Warehouse Connection in Watson Studio

* Open your Watson Studio from IBM Cloud Dashboard and Navigate to the created project.
* Click on the `Add to Project` button and select `Connection`.

![](/doc/source/images/add_to_project_connection.png)

* Select your `DB2 Warehouse` instance created on IBM Cloud.

![](/doc/source/images/db2_warehouse_connection.png)

* The details would already be filled and click the `Create` button.

![](/doc/source/images/create_db2_connection.png)

### 2. Add the SPSS Modeller

* Download the stream file from the repo- `Insert Stream link`
* Open your Watson Studio from IBM Cloud Dashboard and Navigate to the created project.
* Click on the `Add to Project` button and select `Modeller Flow`.

![](/doc/source/images/modeller_connection.png)

* Click on the `From File` tab and upload the downloaded stream file.

![](/doc/source/images/upload_modeller_file.png)

### 3. Run the SPSS Modeller

* Double Click on the `Data Asset` node and click on the `Change Data Asset` button.
* Move to `Connection` tab and select the `DB2 Warehouse` and select the correct `Schema` and the created table.

![](/doc/source/images/add_DB2_Data_Asset.png)
