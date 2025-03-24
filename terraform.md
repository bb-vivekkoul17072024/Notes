# Notes
**Terraform**:
Allows to automate and manage the resource in the aws or azure using code.It basically is IAC in which we use code to automate the task of creation and 
deletion of resources.We can manage the wholem platform and its services.
It is a infra provisioning tool.
Terrafrom can cover vast varieties like k8s,aws and other cloud providers and then to same SaaS also.
Two approaches are there in this declarative and Imperative:
In declarative we give the terraform a declaration that we want these things at the end i.e we define the desired state of the infrastructure and in imperative we
define what things we want i.e we specify each step to achieve the desired state.Terrafrom works in declarative approach.


**Terraform Providers:** 
Terraform relies on plugins called providers to interact with cloud providers, SaaS providers, and other APIs.
Terraform configurations must declare which providers they require so that Terraform can install and use them. Additionally, some providers require 
configuration (like endpoint URLs or cloud regions) before they can be used.
Each provider adds a set of resource types and/or data sources that Terraform can manage.
Every resource type is implemented by a provider; without providers, Terraform can't manage any kind of infrastructure.
Most providers configure a specific infrastructure platform (either cloud or self-hosted). Providers can also offer local utilities for tasks like generating random numbers for unique resource names.

**Terraform Resource:**
Resources are the most important element in the Terraform language. Each resource block describes one or more infrastructure objects, such as virtual networks, compute instances, or higher-level components such as DNS records.

**variables:**
this value can be used at multiple things. 
Addpoint:Terraform is used for creating the infra and sometimes configure it and ansible is used to configure that infra like deploying etc both as IAC.


**TERRAFORM COMMANDS:**
->**refresh**:query infra provider to get current state.
->**terrafrom plan**:provides an overview of what will happen before running the command.
->**RESOURCE**:reate resources like ec2,bucket etc.
resource "aws_instance" "terraformtest" {
  ami="ami-0e35ddab05955cf57"
  instance_type = "t3.micro"
  tags = {
    Name = "Cloudnauts"
  }
  
}

Terraform init: initializes a working directory and downloads the necessary provider plugins and modules and setting up the backend for storing your infrastructure's state. Terraform plan: creates a dry-run, determining what actions are necessary to achieve the desired state defined in the Terraform configuration files.

**terraform init**:initialize the repo
**terraform plan**:gives the summary of what will happen after execution.
**terraorm apply**: used to apply the config file created.
**terraform destroy**:used to destroy the things in the configmap.
**terraform validate**:The terraform validate command is used to check whether your Terraform configuration files are syntactically and structurally correct before applying them.
**terrafrom workflow: practitioner->infra as code -> plan -> apply ->cloud providers->deploy**


**Terraform Config:**
-It uses .tf extension
-Format is HCL (Hashicorp Config Language)
-Declarative Language
-State Management(Modification of created resource like ami id,name,etc is there.When we apply terraform creates a **.tfstate** file which contains the current state of the resource so in this way it contains the current state of the resource and when we need to update it,it does so by seeing this file.Like if we want to change the ami of a resource it first checks the .tfstate file and then update that particular  correspondingly.Once applied, Terraform stores the resource state in a state file (terraform.tfstate), which helps manage infrastructure changes in the future.





