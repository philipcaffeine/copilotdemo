
# Create enterprise chat app with your data 

https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-chat-web-app

## 1. Deploy and test a chat model without your data.
## 2. Add your data.
## 3. Test the model with your data.
## 4. Deploy your web app.


1. Open Azure Portal 

Create resource group : phil-ai-02 
    location : EASTUS 2 

2. Open AI Studio Portal 

https://ai.azure.com/
login in with same Azure account / password 

Create new project:  phil-aiproject-02

Choosse "Customize"

Hub
Name: phil-aihub02
Subscription: MCAPS-Hybrid-REQ-71630-2024-philipchen
Resource group: phil-ai-02
Location: eastus2
Project
Name: phil-aiproject-02
Subscription: MCAPS-Hybrid-REQ-71630-2024-philipchen
Resource group: phil-ai-02
AI Services
Name: ai-phil-aihub02
AI Search
Name: phil-aisearch-02

Create new Deployment : 
    Deploy base model : gpt-4o
    Increase token limit 

    Open in Playground
    

3-1. Open Chat in AI Studio Playground 


Download all product info data in : 
https://github.com/philipcaffeine/copilotdemo/tree/main/data/aistudio-dataset/product-info

Choose "Add your data" 
Upload all the "product-infox.md" 
Choose "Create a new AI Search resource" 

After creation, choose "Connect to other AI search resource
Input index name "product-info-2"

4-1 Create proper role assignment before deploy to Web

Enable "identity" in ai service, ai search, and 
enable "API Access control" as "both" in ai search 


https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/use-your-data-securely#role-assignments


1. Azure AI search -> Access control -> Add role assignment 
 -> managed identify -> AI service 

2. enable System assigned identities in AI service "identity"



4-2 . Deploy as a web app 

Create a new resource group 

name: phil-aistudio-web02
resource group : the group you created
location : EAST US 2 
pricing plan : Standard (S1)

Note: Check "Enable chat history in the web app" 


https://learn.microsoft.com/en-us/answers/questions/2036599/azure-openai-webapp-deploy-failed




3. Open Azure Portal, in previous resource group 

Create "storage account" philaoaiblob02

    Choose "Azure Blob Storage or Azure Data Lake Storage Gen 2" 
    workload : "Other" 
    Redundancy : "LRS" 
    
    Review + Create 

Create new Containers inside Azure Portal 
    "aistudiocontainer02"

