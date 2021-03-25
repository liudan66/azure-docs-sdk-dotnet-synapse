---
title: Azure Synapse Analytics libraries for .NET
description: The Azure Synapse Analytics libraries for .NET offer a convenient interface for making calls to Azure Synapse Analytics.
ms.date: 03/24/2021
ms.topic: reference
ms.service: synapse-analytics
---

# Azure Synapse Analytics libraries for .NET

## Overview

[Azure Synapse Analytics](/azure/synapse-analytics/overview-what-is) is an enterprise analytics service that accelerates time to insight across data warehouses and big data systems. Azure Synapse Analytics brings together the best of SQL technologies used in enterprise data warehousing, Spark technologies used for big data, Pipelines for data integration and ETL/ELT, and deep integration with other Azure services such as Power BI, CosmosDB, and AzureML.

The Azure Synapse Analytics for .NET offers a convenient interface for making calls to Azure Synapse Analytics. 

## Libraries for data access 

The .NET SDK library enables you to program against Synapse Analytics using .NET. Use the library to manage artifacts, workspace access control.  

The latest version is version 4.x.x. Microsoft recommends using version 4.x.x for new applications.

If you cannot update existing applications to version 4.x.x, then Microsoft recommends using version 3.x.x.

### Version 4.x.x

The version 4.x.x libraries for .NET are part of the Azure SDK for .NET. The source code for the Key Vault libraries for .NET is available on [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault).

Use the following version 4.x.x libraries to work with certificates, keys, and secrets:

| Library | Reference | Package | Source |
|----------------------------------------|-------------------------------------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
|    Azure.Security.KeyVault.Administration    |      [Reference](https://docs.microsoft.com/dotnet/api/azure.security.keyvault.administration)       |    [Nuget](https://www.nuget.org/packages/Azure.Security.KeyVault.Administration/)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Azure.Security.KeyVault.Administration)    |
|    Azure.Security.KeyVault.Certificates    |      [Reference](https://docs.microsoft.com/dotnet/api/azure.security.keyvault.certificates)       |    [Nuget](https://www.nuget.org/packages/Azure.Security.KeyVault.Certificates/)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Azure.Security.KeyVault.Certificates)    |
|    Azure.Security.KeyVault.Keys    |     [Reference](https://docs.microsoft.com/dotnet/api/azure.security.keyvault.keys)    |    [Nuget](https://www.nuget.org/packages/Azure.Security.KeyVault.Keys/)      |     [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Azure.Security.KeyVault.Keys)|
|    Azure.Security.KeyVault.Secrets    |    [Reference](https://docs.microsoft.com/dotnet/api/azure.security.keyvault.secrets)    |    [Nuget](https://www.nuget.org/packages/Azure.Security.KeyVault.Secrets/)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Azure.Security.KeyVault.Secrets)    |

### Version 3.x.x

The source code for the Azure Key Vault libraries for .NET is available on [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault).

Use the following version 3.x.x libraries to work with certificates, keys, and secrets:

| Library | Reference | Package | Source |
|--------------------------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
|    Microsoft.Azure.KeyVault.Core    |    [Reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault.core)    |    [Nuget](https://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Microsoft.Azure.KeyVault.Core)    |
|    Microsoft.Azure.KeyVault.Cryptography    |    [Reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault.cryptography)    |    [Nuget](https://www.nuget.org/packages/Microsoft.Azure.KeyVault.Cryptography)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Microsoft.Azure.KeyVault.Cryptography)    |
|    Microsoft.Azure.KeyVault.Extensions    |      |    [Nuget](https://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Microsoft.Azure.KeyVault.Extensions)    |
|    Microsoft.Azure.KeyVault.WebKey    |    [Reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault.webkey)    |    [Nuget](https://www.nuget.org/packages/Microsoft.Azure.KeyVault.WebKey)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Microsoft.Azure.KeyVault.WebKey)    |
|    Microsoft.Azure.KeyVault    |    [Reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault)    |    [Nuget](https://www.nuget.org/packages/Microsoft.Azure.KeyVault)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Microsoft.Azure.KeyVault)    |

### Code Example

This example instantiates  and creates a streaming job.

```csharp
/* Include these 'using' directives:
using Microsoft.Azure.Management.StreamAnalytics;
*/
SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

// Get credentials
ServiceClientCredentials credentials = GetCredentials().Result;

// Create Stream Analytics management client
StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
{
    SubscriptionId = subscriptionId
};

// Create a streaming job
StreamingJob streamingJob = new StreamingJob()
{
    Tags = new Dictionary<string, string>()
    {
        { "Origin", ".NET SDK" },
        { "ReasonCreated", "Getting started tutorial" }
    },
    Location = "West US",
    EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
    EventsOutOfOrderMaxDelayInSeconds = 5,
    EventsLateArrivalMaxDelayInSeconds = 16,
    OutputErrorPolicy = OutputErrorPolicy.Drop,
    DataLocale = "en-US",
    CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
    Sku = new Sku()
    {
        Name = SkuName.Standard
    }
};
StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
```


> [!div class="nextstepaction"]
> [Explore the data access APIs](/dotnet/api/overview/azure/streamanalytics/management)


## Samples

- [Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

## Libraries for resource management 

The Synapse management SDK for .NET provides classes and methods that allow you to manage your Synapse resource. It includes operations to create, delete, update, list. 

Use the following library to work with the Azure Synapse Analytics resource provider:

|    Library    |    Reference    |    Package    |    Source    |
|------------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
|    Microsoft.Azure.Management.KeyVault    |    [Reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.keyvault)    |    [Nuget](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault/)    |    [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Microsoft.Azure.Management.KeyVault)    |

## Samples

- [Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package


> [!div class="nextstepaction"]
> [Explore the resource management APIs](/dotnet/api/overview/azure/streamanalytics/management)
