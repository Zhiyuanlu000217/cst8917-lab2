youtube link: https://youtu.be/J2NpaexHReI

> [!Note]
> This repo is duplicated from [Intellegent-PDF-Summerizer](https://github.com/Azure-Samples/Intelligent-PDF-Summarizer/tree/main)

# Prerequisites

- Azure CLI
- VS Code Plugins
    - Azure
    - Azure function
- OpenAI Account
- Azure resources
    - Storage Account
    - Function App
    - Azure AI service
- Python 3.10

First, create a `local.settings.json` at root directry, which will contain the credentials will be used in the project
```json
{
  "IsEncrypted": false,
  "Values":  
  {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "AzureWebJobsFeatureFlags": "EnableWorkerIndexing",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    // Make sure this is the connection string, not the endpoint
    "BLOB_STORAGE_ENDPOINT": "<STORAGE_ACCOUNT_CONNECTION_STRING>",
    // e.g. https://cst8921-lab2.cognitiveservices.azure.com/
    "COGNITIVE_SERVICES_ENDPOINT": "<AZURE_COGNITIVE_SERVICE_ENDPOINT>", 
    "CHAT_MODEL_DEPLOYMENT_NAME": "gpt-4", // by default the model is gpt-4
    "OPENAI_API_KEY": "<OPEN_AI_API_KEY>"
  }
}
```

Then, go to Storage Account, create two containers, names `input` and `output`, they will be used to place the PDF being processed and the output of the result.

# Run the app locally

1. In VSCode, use the shortcut `FN + F5` to run the function locally
2. Once the function is started, go to Azure > Storage Account > Containers > input
3. Upload a PDF file
4. You can see the trigger is being triggered, and logs are generated, it may take more than 30 seconds to process
5. Once the function is finished processing, checkout the `output` container, there should be a `.txt` file with the exact same name, which contains the summerization of the given PDF

# Deploy the app to Azure

1. In VSCode, use the shortcut `Command/Ctrl + Shift + P` to open the command palette
2. Choose "Azure functions: Deploy to function app", then follow the instruction
3. Once done, wait for couple minutes to allow the functions deployed
4. Try again with step 2-5 above, the output is generated as expected