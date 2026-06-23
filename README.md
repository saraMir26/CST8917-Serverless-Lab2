# CST8917 – Serverless Applications

## Lab 2: Smart Image Analyzer with Durable Functions

**Student:** Sara Mirzaei    
**Course:** CST8917 – Serverless Applications     
**Lab:** Lab 2 – Smart Image Analyzer with Durable Functions    
**Date:** June 23 2026   

## Objective

The purpose of this lab was to build a serverless image analysis solution using Azure Durable Functions and the Fan-Out/Fan-In orchestration pattern. The application automatically analyzes images uploaded to Azure Blob Storage and stores the analysis results in Azure Table Storage.

## Solution Overview

The solution uses Azure Durable Functions to coordinate multiple image analysis tasks running in parallel. When an image is uploaded to the Blob Storage container, a Blob Trigger starts the orchestration process. Four activity functions execute simultaneously:

* Color Analysis
* Object Analysis
* Text (OCR) Analysis
* Metadata Analysis

After all activities complete, the results are combined into a report and stored in Azure Table Storage. A separate HTTP endpoint allows users to retrieve analysis results.

### Azure Services Used

* Azure Functions
* Azure Durable Functions
* Azure Blob Storage
* Azure Table Storage
* Azure Storage Account
* Azurite (Local Development Emulator)

### Durable Functions Pattern

This lab demonstrates the Fan-Out/Fan-In pattern.

**Fan-Out Phase**

* Analyze Colors
* Analyze Objects
* Analyze Text
* Analyze Metadata

All four activities execute in parallel using:

```python
results = yield context.task_all(tasks)
```

**Fan-In Phase**
The results from all activities are collected and passed to the report generation function.

### Testing and Validation

The application was tested locally using Azurite and then deployed to Azure.

Testing included:

1. Uploading images to the Blob Storage container.
2. Verifying orchestration execution through Function App logs.
3. Confirming parallel execution of activity functions.
4. Validating report generation.
5. Retrieving stored results through the HTTP endpoint.

The application successfully analyzed uploaded images and stored the results in Azure Table Storage.

### Challenges Encountered

Several issues were encountered during implementation:

* Azure Storage permission issues related to Microsoft Entra ID authentication.
* Configuration of storage connection strings in Azure Function App environment variables.

These issues were resolved by recreating the virtual environment using Python 3.12, installing required dependencies, assigning appropriate Azure permissions, and configuring application settings correctly.

### Conclusion

This lab successfully demonstrated the use of Azure Durable Functions and the Fan-Out/Fan-In orchestration pattern. The solution processes image analysis tasks efficiently through parallel execution and stores the results using Azure Table Storage. The project provided practical experience with serverless architecture, orchestration workflows, Azure Storage services, and cloud deployment.


## Demo Video

<sub>Click the thumbnail to watch the demo.</sub>

[![Watch the video](https://img.youtube.com/vi/Hx7HmIcT0Mw/hqdefault.jpg)](https://www.youtube.com/watch?v=Hx7HmIcT0Mw) 

