# Cloudformation Nested Stack Examples

This project contains some suggestions about naming conventions and how to organize cloud formation nested stacks in a reasonable folder structure.   

The repo here depicts a prototypical folder structure for 3 sample applications and a set of shared services to support them.   It does not attempt to represent a fully-baked application folder structure for something complex like a NodeJs solution.   It only represents the organization of the Cloudformation templates.

The stacks represented here have been tested and do build successfully, however they represent bare-bones implementations of services, just to illustrate the principles of component-based stack composition.

Style Guidelines displayed by this repo include the following: 

Naming Conventions
* Folder names
  *	All lower case
  * Use hyphens to separate logical words and terms 
  *	For products, lead with the application name
  *	Examples
    * shared-resources  (main repo for sharing patterns and templates)
    * my-web-app (example product/application folder)
    * resources (example sub-folder for cloudformation resources)
* Templates
  * All cloudformation includes the prefix – ‘cf’  
  * Use hyphens to separate words, names and terms 
  * For products, include the application name in CamelCase (e.g  cf-myWebApp-)
  * Differentiate root templates by the identifier ‘main’  (e.g. cf-myWebApp-main.yaml)
  * For nested resources, include the AWS resource name in lower case (e.g. cf-myWebApp-rds.yaml). Further details about the resource type may be added after the resource name (e.g. cf-myWebApp-rds-mysql.yaml)
  * Shared resources should include the identifier ‘shared’ (e.g. cf-shared-subnet-public.yaml) 

Always try to adopt a component-based approach to building cloudformation stacks.   This will provide many benefits, such as feature isolation and will also promote reusability and ease of maintenance.

The two main approaches for component based assembly which are showcased here are:
1. Cross-stack Resource Sharing
    * Good for cases where a resource should be defined once and consumed by other resources which are dependent on it.
    * Good examples are networking resources for a given architecture – e.g. vpc, subnet, security group.   
    * Exposed properties are exported from the component stack and imported into the consuming stack. 
    * Cross-stack resource sharing is a good practice, but should be used judiciously, as it creates tight-coupling between the component stack and those stacks which are dependent on it.  Component stacks cannot be deleted or changed without considering impacts to dependent stacks. 

2. Nested Stacks
    * In this case, only the definition is reused, not the actual instantiated resource object.
    * A root stack will reference the nested (child) stack, passing it the required parameters and optionally exposing outputs at the root level.
    * This is creates a loosely-coupled relationship between the root stack and nested child stacks.   This is good, allowing patterns to be reused and still customized as needed.
    * When a root stack templates is built, it first builds all nested child stacks to which it refers.   All changes to child stacks should be rebuilt from the root stack down.

    NOTE:  in both of the cases above the component resource consists of a stand-alone stack, which can be built and used independently if desired.  

![Component Stack Types](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/nested-stacks.png)
