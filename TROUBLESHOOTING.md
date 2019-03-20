# Troubleshooting

1. If you an encounter an error, while running the notebook-

![](/doc/source/images/Scraping_Error.png)

Wait for about an hour and run from the point of error again.

2. If there is an issue in the data being saved back from the SPSS results to DB2 Warehouse-

* Double click on the `export` node and click on `Change Data Asset` and ensure you have kept the `Replace existing dataset` option.

![](/doc/source/images/save_to_dataset.png)

* Select some existing `csv` dataset and run the modeler flow.

![](/doc/source/images/select_dataset.png)

```
NOTE: THIS WILL REPLACE THE DATA ASSET. BE SURE TO MAKE A COPY BEFORE PERFORMING THE STEPS.
```
* Now, open the notebook in your project and move to the last cell. Click on the `10/01` tab on left-hand top corner. Select the saved dataset and click on `Insert Pandas Dataframe`.

![](/doc/source/images/dataset_to_ntbk.png)

* Run the above mentioned cell and ensure the Dataframe is named - `df_data_1`.
* Create a new cell by clicking on the `+` button on the top right corner, and add the below code to that cell-

```Python

tuple_of_tuples = tuple([tuple(x) for x in df_data_1.values])
i=1
for x in df_data_1.values:
    #print((tuple(x)))
    vals= (i,) + tuple(x)
    #print(vals)
    #print(x[0],x[1],x[2],x[3],x[4],x[5],x[6],x[7],x[8],x[9],x[10],x[11],x[12])
    sql = "INSERT INTO DASHXXXX.DATA_FOR_COGNOS VALUES"+ str(vals)
    i=i+1
    ins_sql=ibm_db.prepare(conn, sql)
    ibm_db.execute(ins_sql)
    
```

Before replacing the name, be sure to get the Schema name of your DB2 Warehouse and replace it with `DASHXXXX`.

You can find your Schema name in your DB2 Warehouse instance when you open the table like `DASHXXXX.Table_Name`-

![](/doc/source/images/Schema_Name.png)

3. If you face a missing DataSet error in Cognos-

![](/doc/source/images/Cognos_error.jpg)

Click on the `Re-link` button.
