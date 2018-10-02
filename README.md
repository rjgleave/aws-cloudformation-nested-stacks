# Cloudformation Nested Stack Examples
some ideas on naming conventions and how to organize cloud formation nested stacks in a folder structure

Basic principles:

Naming Conventions
•	Folder names
o	All lower case
o	Use hyphens to separate logical words and terms 
o	For products, lead with the application name
o	Examples
	shared-resources  (main repo for sharing patterns and templates)
	my-web-app (example product/application folder)
	resources (example sub-folder for cloudformation resources)
•	Templates
o	All cloudformation includes the prefix – ‘cf’  (e.g. cf)
o	Use hyphens to separate words, names and terms (e.g. cf-)
o	For products, include the application name in CamelCase (e.g  cf-myWebApp-)
o	Differentiate root templates by the identifier ‘main’  (e.g. cf-myWebApp-main.yaml)
o	Nested resources include the AWS resource in lower case (e.g. cf-myWebApp-rds.yaml)
o	Nested resources may include added details  (e.g. cf-myWebApp-rds-mysql.yaml)
o	Shared resources should include the name ‘shared’ (e.g. cf-shared-subnet-public.yaml) 

As stated previously, adopt a component-based approach to building cloudformation stacks.   This will provide many benefits, such as feature isolation and will also promote reusability and ease of maintenance.

The two main approaches for component based assembly are:
•	Cross-stack Resource Sharing – 
o	good for cases where a resource should be defined once and consumed by other resources which are dependent on it.
o	Good examples are networking resources for a given architecture – e.g. vpc, subnet, security group.   
o	Exposed properties are exported from the component stack and imported into the consuming stack. 
o	Cross-stack resource sharing is a good practice, but should be used judiciously, as it creates tight-coupling between the component stack and those stacks which are dependent on it.  Component stacks cannot be deleted or changed without considering impacts to dependent stacks. 
•	Nested Stacks
o	In this case, only the definition is reused, not the actual instantiated resource object.
o	A root stack will reference the nested (child) stack, passing it the required parameters and optionally exposing outputs at the root level.
o	This is creates a loosely-coupled relationship between the root stack and nested child stacks.   This is good, allowing patterns to be reused and still customized as needed.
o	When a root stack templates is built, it first builds all nested child stacks to which it refers.    All changes to child stacks should be rebuilt from the root stack down.
NOTE:  in both of the cases above the component resource consists of a stand-alone stack, which can be built and used independently if desired.  
