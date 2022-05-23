# Standard Logic App's callback URL


Since Microsoft has launched Logic App standard, developers are struggling to get the callback URLs for workflows.

    {
        "basePath": "https://{logicappname}.azurewebsites.net/api/{workflowname}/triggers/manual/invoke",
        "method": "POST",
        "queries": {
          "api-version": "2020-05-01-preview",
          "sig": "{sig}",
          "sp": "/triggers/manual/run",
          "sv": "1.0"
        },
        "value": "https://{logicappname}.azurewebsites.net:443/api/{workflowname}/triggers/manual/invoke?api-version=2020-05-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig={sig}"
    }
     
