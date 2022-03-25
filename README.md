# azure_pipeline_YAML

Azure Pipelines can automatically build and validate every pull request and commit to your Azure Repos Git repository. Azure Pipelines can be used with Azure DevOps public projects and Azure DevOps private projects. Start slowly and create a pipeline that echoes "Hello world!" to the console. No technical course is complete without a hello world example.

```
name: 1.0$(Rev:.r)

# simplified trigger (implied branch)
trigger:

- main

# equivalents trigger
# trigger:
#  branches:
#    include:
#    - main

variables:
  name: martin

pool:
  vmImage: ubuntu-latest

jobs:

- job: helloworld
  steps:

    - script: echo "Hello, $(name)"
    
  ```
  <a href=“https://docs.microsoft.com/en-us/learn/modules/integrate-azure-pipelines/2-describe-anatomy-of-pipeline“>Azure DevOps</a>

  
