# Simple Example of Cross-stack Resources Sharing
some ideas on naming conventions and how to organize cloud formation nested stacks in a folder structure

Cross-stack Resource Sharing Steps:
1.	Identify a resource which should be shared as a component for other stacks to consume.
a.	Create a cloudformation template to define the stack.  
i.	Follow the naming convention for shared resources described in Section 8.  
ii.	It should be stored in the ‘shared-resources folder’.    Do not put a shared resource template in the folder belonging to any individual application, since it will be shared by multiple apps.
b.	Modify the Outputs section to include an Export section.   In the example below, four properties of shared resource stack are identified for export.


![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)

Note the export statement, which is added to each property, to make it sharable.

c.	Build the component stack from the template.  Note: the stack name you choose will be used to import properties in the consumer stacks in section 2 below.


![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)


		Exported values are available as outputs, just like any other stack.

2.	For each stack which consumes a shared resource:
a.	Include the component stack as a parameter in the consuming stack.  The example below shows how a network stack is imported into a consuming stack.   


![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)

Important:  the user will enter the stack name (1c above) for this parameter, not the template name.

b.	For each property which is consumed from the shared component stack, import the property using the ImportValue statement.  The example below shows the security group and subnet properties being imported into an EC2 resource.

![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)


