# Vectra Data Connector
* [Introduction](#Introduction)
* [Folders](#Folders)
* [Installing for the users](#Installing-for-the-users)
* [Installing for testing](#Installing-for-testing)

## Introduction<a name="Introduction"></a>

This folder contains the Azure function time trigger code for Vectra Data Connector. The connector will run periodically and ingest the Vectra data into the Microsoft Sentinel logs custom tables.
## Folders<a name="Folders"></a>

1. `VectraDataConnector/` - This contains the package, requirements, ARM JSON file, connector page template JSON, and other dependencies.

2. `Detections/` - This contains the Azure function source code to ingest the data of the below mentioned endpoint.
    * Detections Data

3. `Audits/` - This contains the Azure function source code to ingest the data of the below mentioned endpoint.
    * Audits Data

4. `EntityScoring/` - This contains the Azure function source code to ingest the data of the below mentioned endpoint.
    * Entity Scoring Data

## Installing for the users<a name="Installing-for-the-users"></a>

After the solution is published, we can find the connector in the connector gallery of Microsoft Sentinel among other connectors in the Data connectors section of Sentinel.

i. Go to Microsoft Sentinel -> Data Connectors

ii. Click on the Vectra Data Connector, and the connector page will open.

iii. Click on the blue `Deploy to Azure` button.

It will lead to a custom deployment page where the user needs to select **Subscription**, **Resource Group**, and **Location**.
Then the following information is required to configure the Vectra Data Connector.
User Inputs  | Default Value
------------- | -------------
Function Name  | Vectra
Workspace ID  | None
Workspace Key  | None
Vectra Base URL  | None
Vectra Client Id  | None
Vectra Client Secret Key | None
Start Time  | None(current time)
Audits Table Name  | Audits_Data
Detections Table Name | Detections_Data
Entity Scoring Table Name  | Entity_Scoring_Data
Log Level  | INFO
Detections Schedule  | 0 2/10 * * * *
Audits Schedule  | 0 5/10 * * * *
Entity Scoring Schedule  | 0 8/10 * * * *

The connector should start ingesting the data into the tables at every time interval specified in the Schedules during configuration.


## Installing for testing<a name="Installing-for-testing"></a>


i. Log in to the Azure portal using the URL - [Azure Portal-Home](https://portal.azure.com/?feature.BringYourOwnConnector=true&feature.UseKoBladeForE2E=true#home).

ii. Go to Microsoft Sentinel -> Data Connectors

iii. Click the “import” button at the top and select the JSON file VectraCloud_API_FunctionApp.json` downloaded on your local machine from Github.

iv. This will load the connector page, and the rest of the process will be the same as the Installing for users guideline above.


Each invocation and its logs of the function can be seen in the Function App service of Azure, available in the Azure Portal outside the Microsoft Sentinel.

i. Go to Function App and click on the function which you have deployed, identified with the given name at the deployment stage.

ii. Go to Functions -> Any of our function -> Monitor

iii. By clicking on the invocation time, you can see all the logs for that run.

**Note: Furthermore, we can check logs in Application Insights of the given function in detail if needed. We can search the logs by operation ID in the Transaction search section.**
