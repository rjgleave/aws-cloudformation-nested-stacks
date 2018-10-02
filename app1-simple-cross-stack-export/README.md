# A Simple Example of Cross-stack Resources Sharing
Cross-account sharing allows an instantiated stack to be consumed by other stacks. This is not an approach where you are reusing code.  You are not creating a new stack.   You are simply sharing the resource outputs of an existing stack within other stacks.

Cross-stack Resource Sharing Steps:
1. Identify a resource which should be shared as a component for other stacks to consume.
	* Create a cloudformation template to define the stack.  
		* Follow the naming convention for shared resources described in Section 8.  
		* It should be stored in the ‘shared-resources folder’.    Do not put a shared resource template in the folder belonging to any individual application, since it will be shared by multiple apps.
	* Modify the Outputs section to include an Export section.   In the example below, four properties of shared resource stack are identified for export.


![Export Statements](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/exported-resources.png)

	Note the export statement, which is added to each property, to make it sharable.

	* Build the component stack from the template.  Note: the stack name you choose will be used to import properties in the consumer stacks in section 2 below.


![Shared Stack](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/component-stack-outputs.png)


	Exported values are available as outputs, just like any other stack.

2. For each stack which consumes a shared resource:
	* Include the component stack as a parameter in the consuming stack.  The example below shows how a shared network stack is imported into a consuming stack.   

![Define the Shared Resource as a Parameter](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/shared-resource-parameter-definition%20.png)

	Important:  the user will enter the stack name (1c above) for this parameter, not the template name.

	* For each property which is consumed from the shared component stack, import the property using the ImportValue statement.  The example below shows the security group and subnet properties being imported into an EC2 resource.

![Imported Properties](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/cross-stack-imported-property.png)
