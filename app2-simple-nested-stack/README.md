# Simple Nested Stack Example
some ideas on naming conventions and how to organize cloud formation nested stacks in a folder structure

Steps for Implementing Nested Stacks:
1.	The Nested Stack  
a.	Create a cloudformation template to define the nested stack.  
i.	Store the template in the ‘resources folder’ where the root (‘main’) stack template resides.  
ii.	Follow the naming convention for nested stack resources described in Section 8.

![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)

The example above shows an application folder structure with a nested EC2 resource.

b.	Define any outputs you wish to make available to the root template.   In the example below, four properties are defined as outputs.     

![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)

Note:  nothing out of the ordinary is done to these properties when defining them as outputs.
 
c.	Build the nested stack from the cloudformation template you created.   This actual stack will not be used.   You may delete it when it is built.    It is only done to validate the template design and to archive the template in S3.  
d.	Once the stack builds successfully, copy the path of the template which was stored in S3.   

![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)
 
	Copy the Link above to the template.   You will need this in a step below.

2.	The Root Stack  
a.	Create a cloudformation template to define the root (‘main’) stack.  
i.	Follow the naming convention defined in Section 8.
ii.	Put the template at the same level as the ‘resources’ folder (see 1a above) 
b.	Copy all of the needed parameters from the nested stack into the root stack.  For example, the InstanceType parameter below was also a parameter for the EC2 nested stack.   These parameters will be passed to the nested stack.

![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)
 
c.	Define a resource in the root stack to represent the nested stack.    Notice in the example below how the AWS::CloudFormation::Stack keyword is used to define this unique resource type.

![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)
 
Copy the S3 template URL which you saved in step 1d above into the TemplateURL property

d.	If you wish to expose any of the output properties from the nested stack in the root stack, include them in the Outputs section of the root template.   Note in the example below how 

![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)
 

e.	Build the root stack from the root template.   It will automatically build any nested stacks first.   If any of them fail, the root stack will fail.    Once the nested stacks are built, the root stack is built.    In the example below you can see how nested stacks are identified differently than the root stack.

![S3 Bucket](https://github.com/rjgleave/aws-batch-universal-scheduler/blob/master/assets/s3-bucket.png)
 
Notice how the resources folder contains the nested stack

