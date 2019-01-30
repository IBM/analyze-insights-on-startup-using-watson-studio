 

# Building a Dashboard 

Create the custom control widget using Javascript. The custom control developed for this pattern: 

  * asks to provide the value of required parameters as an input for the WML model.
  * calls REST API which in-turn invokes WML model using the provided input parameters.
  * API sends response back to custom control in Cognos.
  * parses the output (confidence score) and display as a d3 pie chart on Cognos Dashboard. 

In this repository, custom control code is available at `./custom-control-code`. Update the URL in `report1.js ` file as shown and save the file.

![](https://github.com/IBM/invoke-wml-using-cognos-custom-control/blob/master/images/custom-control-API.png)
  
Here, copy the URL of your node application deployed in previous step.
