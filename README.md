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
According to [Azure](https://docs.microsoft.com/en-us/learn/modules/integrate-azure-pipelines/2-describe-anatomy-of-pipeline) the most pipelines will have these components:

Name – though often it's skipped (if it's skipped, a date-based name is generated automatically).

Trigger – more on triggers later, but without an explicit trigger. There's an implicit "trigger on every commit to any path from any branch in this repo."

Variables – "Inline" variables (more on other types of variables later).

Job – every pipeline must have at least one job.

Pool – you configure which pool (queue) the job must run on.

Checkout – the "checkout: self" tells the job which repository (or repositories if there are multiple checkouts) to check out for this job.

Steps – the actual tasks that need to be executed: in this case, a "script" task (the script is an alias) that can run inline scripts.

```
trigger:
  branches:
    include:

    - main
 ```
This trigger is configured to queue the pipeline only when there's a commit to the main branch. What about triggering for any branch except main? You guessed it: use exclude instead of include:

```
trigger:
  branches:
    include:

    - feature/*
  paths:
    include:

    - webapp/**
```

Jobs:

```
jobs:

- job: A
  steps:
  # steps omitted for brevity


- job: B
  steps:
  # steps omitted for brevity
  
 jobs:

- job: A
  steps:

  - script: echo' job A.'


- job: B
  dependsOn: A
  steps:

  - script: echo' job B.'


- job: C
  dependsOn: A
  steps:

  - script: echo' job C.'


- job: D
  dependsOn:

  - B
  - C
  steps:

  - script: echo' job D.'


- job: E
  dependsOn:

  - B
  - D
  steps:

  - script: echo' job E.'
  
  ```
  
  
  
