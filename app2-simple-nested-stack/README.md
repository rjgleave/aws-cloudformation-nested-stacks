# Simple Nested Stack Example
some ideas on naming conventions and how to organize cloud formation nested stacks in a folder structure

Steps for Implementing Nested Stacks:
1. The Nested Stack  
	* Create a cloudformation template to define the nested stack.  
    	* Store the template in the ‘resources folder’ where the root (‘main’) stack template resides.  
    	* Follow the naming convention for nested stack resources described in Section 8.

![Nested Stack Folder Structure](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/nested-stack-folder-structure.png)

	The example above shows an application folder structure with a nested EC2 resource.
	
	* Define any outputs you wish to make available to the root template.   In the example below, four properties are defined as outputs.     

![Nested Template Outputs](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/Nested-template-outputs.png)

	Note:  nothing out of the ordinary is done to these properties when defining them as outputs.
 
	* Build the nested stack from the cloudformation template you created.   This actual stack will not be used.   You may delete it when it is built.    It is only done to validate the template design and to archive the template in S3.  
	* Once the stack builds successfully, copy the path of the template which was stored in S3.   

![S3 Bucket Templates](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/S3-bucket-template-path.png)
 
	Copy the Link above to the template.   You will need this in a step below.

2. The Root Stack  
	* Create a cloudformation template to define the root (‘main’) stack.  
		* Follow the naming convention defined in Section 8.
		* Put the template at the same level as the ‘resources’ folder (see 1a above) 
	* Copy all of the needed parameters from the nested stack into the root stack.  For example,the InstanceType parameter below was also a parameter for the EC2 nested stack.   These parameters will be passed to the nested stack.

![Root Stack Parameters](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/root-stack-parameters.png)
 
	* Define a resource in the root stack to represent the nested stack.    Notice in the example below how the AWS::CloudFormation::Stack keyword is used to define this unique resource type.

![Root Stack Resources](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/root-stack-resource-definition.png)
 
	Copy the S3 template URL which you saved in step 1d above into the TemplateURL property

	* If you wish to expose any of the output properties from the nested stack in the root stack, include them in the Outputs section of the root template.   Note in the example below how 

![Root Stack Outputs](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/root-stack-output-definition.png)
 
	* Build the root stack from the root template.   It will automatically build any nested stacks first.   If any of them fail, the root stack will fail.    Once the nested stacks are built, the root stack is built.    In the example below you can see how nested stacks are identified differently than the root stack on the Cloudformation Build Screen.

![Building the Root Stack](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/root-stack-build-screen.png)
 
	Notice how the resources folder contains the nested stack
