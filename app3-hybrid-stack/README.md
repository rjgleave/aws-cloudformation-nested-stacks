# Hybrid Nested Stack Example - Includes Nested Stacks and Cross-Stack Sharing

Simple example of a hybrid stack.. meaning one that utilizes both Cross-stack Shared Resources and also Nested Stacks.   It is likely that some of your stacks will be composed like this.

This example uses a shared Network stack, as well as a shared SNS topic.

It also builds nested stacks of EC2 and RDS.

## Fixed vs Variable Properties
The powerful thing about nested stacks is that you can create a common RDS pattern, for instance, which is used in multiple stacks, and vary the different properties of each as needed.  You can allow some properties to be variable (as parameters) to be set by the user.  Other properties can be fixed.  And the mix of those fixed and variable properties can change from one application to another. 
