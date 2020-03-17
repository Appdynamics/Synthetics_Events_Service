# Synthetics_Events_Service

This Python scripts demonstrates how to create a custom schema and post metrics to the AppDynamics Event Service Data Store.

Once metrics are posted to the AppDynamics Event Service Data: [Dynamics Baselines](https://docs.appdynamics.com/display/PRO45/Dynamic+Baselines) are established for the metrics, [Actional Alerts](https://docs.appdynamics.com/display/PRO45/Alert+and+Respond), can be enabled and [Dashboards](https://docs.appdynamics.com/display/PRO45/Dashboards+and+Reports) created.

This working example is runnable as either an AppDynamics [Synthetics](https://docs.appdynamics.com/display/PRO45/Browser+Synthetic+Monitoring) Job, or from the command line. It provides the following functionality:
* Create and delete custom schemas
* Measure the perform of a POST/GET request to an arbitary URL
* Post metrics to the custom schema

# Create a Custom Schema

The Python script should be used to create and delete custom schems from the command line:

```python eventsServiceTest.py deleteSchema schemaA```

```python eventsServiceTest.py createSchema schemaA```

In this example script the custom schema is defined as:
```
exampleSchema = { "schema": { "testid":         "integer",
                              "status_code":    "integer",
                              "status_code_s":  "string",
                              "response_time":  "integer",
                              "url":            "string",
                              "mesid":          "string” }  }
```

In the above schema the string representation of status_code (\_s) allows for the `status_code` to be used as a Legend in dashboard charts.

Modify the schema as needed to support the use case. See [Supported Data Types](https://docs.appdynamics.com/display/PRO45/Analytics+Events+API)

For demonstration purposes the script randomly selects a URL from a list of URLs scoped for testing defined by:
```
urlList = [ "https://google.com",
             "https://yahoo.com",
             "https://appdynamics.com",
             "https://google.com/TESTERROR" ]
```

# Post Metrics
The current script performs a GET request against the selected URL and then posts the response time and status_code to the Events Data Store.

The Python script can be run from the command line or as a Synthetic Job. Run the test case `runtest1` from the command line as follows:

```python synthetics_events_service.py runtest1 schemaA```

Once this works as desired copy the script to an [AppDynamics Synthetics Job](https://docs.appdynamics.com/display/PRO45/Synthetic+Jobs) 

The full Python script is available here: [synthetics_events_service.py](https://github.com/APPDRYDER/Synthetics_Events_Service/blob/master/synthetics_events_service.py)

The `Events-API-AccountName` and `Events-API-Key` are required for the script to authenticate with the Events Service and these can applied using environment variables, inline in the code, or using the [Synthetics Credential Vault](https://docs.appdynamics.com/display/PRO45/Synthetic+Credential+Vault) when the script runs as a  Synthetics Job. See [Managing API Keys for how to create the API key](https://docs.appdynamics.com/display/PRO45/Managing+API+Keys)

# Getting Started

Clone this repository using:

`git clone https://github.com/APPDRYDER/Synthetics_Events_Service`

Modify the the file `envvar.sh` to enable authentication to an AppDynamics SaaS Controller.

Contact [AppDynamics](https://www.appdynamics.com/) if you would like further help with this.

