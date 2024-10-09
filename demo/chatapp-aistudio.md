
# Create enterprise chat app with your data 

Refer to below tutorial in AI Studio 
https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-chat-web-app


## 1. Open Azure Portal 

https://ms.portal.azure.com/#home

Create resource group : "phil-ai-02" 
    location : EASTUS 2 


## 2. Open Azure AI Studio Portal 

https://ai.azure.com/ 

Login in with same Azure account / password 

Create new project:  "phil-aiproject-02"
Choosse "Customize"

### Below is only for reference, you can have your own naming : 

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


###　Create new model Deployment : 
    Deploy base model : gpt-4o
    Increase token limit 
    Open in Playground
    

## 3. Open Chat in AI Studio Playground 

Download all product info data in : 
https://github.com/philipcaffeine/copilotdemo/tree/main/data/aistudio-dataset/product-info

Choose "Add your data" 
Upload all the "product-info_X.md" 
Choose "Connect to a AI Search resource" 

After creation, choose "Connect to other AI search resource
Input index name "product-info"


## (skip) 4. Create proper role assignment before deploy to Web

### Enable "Identity" in created AI service, AI search, and enable "API Access control" as "both" in AI Search 

https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/use-your-data-securely#role-assignments

1. Azure AI search -> Access control -> Add role assignment  -> managed identity -> AI service 
2. enable System assigned identities in AI service "identity"


## 4. Deploy as a web app (using step 5. as workaround for now)

Create a new resource group 

name: phil-aistudio-web02
resource group : the group you created
location : EAST US 2 
pricing plan : Standard (S1)

Note: Check "Enable chat history in the web app" to create Cosmos DB 

Note: One click deploy chat web app is currently failed with some issue 
https://learn.microsoft.com/en-us/answers/questions/2036599/azure-openai-webapp-deploy-failed

https://learn.microsoft.com/en-us/answers/questions/2099867/azure-ai-studio-deploy-chat-webapp-failed?comment=question#newest-question-comment



## 5. Create web app from one click sample 

Create web app follow "deploy" button in below link 

https://github.com/microsoft/sample-app-aoai-chatGPT?tab=readme-ov-file#one-click-azure-deployment


### Input below columns in deployment GUI

Azure Search Service : phil-aisearch-02018032638575
Azure Search Index : hr-faq-index

Azure Search Key :　
Azure Open AI Resource : ai-philaihub02018032638575
Azure Open AI Model : gpt-4o

Azure Open AI Model Name：empty 
Azure Open AI Key : 

Azure Open AI Embedding Name : text-embedding-ada-002
Web App Enable Chat History  : true


## 6. Enable Authentication of your App service 

### 1. Create app registration

Azure Portal >> Entra >> App registration >> Create new >> 

This tenant login only 
Add client secret 
Add redirect web url as App service url 

    https://your_app_service_name.azurewebsites.net/.auth/login/aad/callback

Check "Implicit grant and hybrid flows" > "ID tokens (used for implicit and hybrid flows)"

Keep below info: 

Application (client) ID
Secret ID

### 2. Enable authentication 

Follow below link to enable chat app authentication 
https://learn.microsoft.com/en-us/azure/app-service/scenario-secure-app-authentication-app-service?tabs=workforce-configuration#3-configure-authentication-and-authorization

Add "identity" in new create App Service

### 3. [Azure Portal]Using Data Explore in Cosmos DB account to watch chat history 


