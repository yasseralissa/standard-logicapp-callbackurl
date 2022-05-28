
# Standard Logic App's callback URL

Since Microsoft has launched the Logic App standard, developers are struggling to get the callback URLs for workflows. 

One major difference is that the Consumption Logic app is only a workflow, while the standard Logic app can host different workflows.

To understand how to retrieve all standard logic app workflows' URLs and other information, we can assume that standard logic apps are a group of consumption logic apps hosted on app service plans.

Let's take a look at the resource type of a consumption logic app and a workflow in a standard logic app.

    ' Standard Logic App's workflow
    Microsoft.Web/sites/hostruntime/webhooks/api/workflows

    ' Consumption Logic App's
    Microsoft.Logic/workflows

In consumption logic apps we need only to provide the name of the workflow, but in standard logic app workflow we need to provide the name of each segment of the type:

 - Microsoft.Web/sites: Logic app name, 
 - hostruntime: hardcoded 'runtime',
 - webhooks: hardcoded 'workflow', 
 - api: hardcoded 'management', 
 - and workflows: workflow's name

Now let's try to get the callback URLs for a consumption logic app and standard logic app workflow in an ARM template:

## Consumption logic app
```
"[listCallbackUrl(resourceId('Microsoft.Logic/workflows/triggers', parameters('workflowName'), 'manual'),'2021-03-01').value]"
```

## Standard logic app workflow
```
[listCallbackUrl(resourceId('Microsoft.Web/sites/hostruntime/webhooks/api/workflows/triggers', parameters('logicAppName'), 'runtime', 'workflow', 'management', parameters('workflowName'), 'manual'),'2021-03-01').value]
```
The same concept can be applied to any consumption API call that requires a resource id as a parameter or in the REST APIs.

