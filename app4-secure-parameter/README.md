# Importing Run Time Values from Parameter Store

Simple example showing how to import parameters into Cloudformation.

This illustrates two examples:
* Importing a regular parameter.
* Importing a secure string, such as a password.

## Example 1: Importing the latest version# of a parameter

You can import a parameter into a Cloudformation template from SSM Parameter Store by using the Cloudformation Type: 'AWS::SSM::Parameter::Value<String>' (see example below)

	![Define the Shared Resource as a Parameter](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/regular-parameter.png)

## Example 2: Importing a secure password

A secure password can be imported directly into a Cloudformation resource property using the following notation:   '{{resolve:ssm-secure:/dev/AppName/database/admin-password:1}}'

Note: you must include the version number when importing secure strings.    This can create a problem since there is no support at present in Parameter Store for the concept of 'latest' (getting the latest version of secure string).    To get around that problem, you can store the latest version number in a regular parameter and use that value to dynamically import the secure stream.

See how the value in Example 1 above is used to dynamically assemble the secure string import statement during the template build (see below)

	![Define the Shared Resource as a Parameter](https://github.com/rjgleave/aws-cloudformation-nested-stacks/blob/master/assets/secure-string-parameter.png)
