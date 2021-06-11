# shubh-s-Taskcat-Repository
### Repository to run TaskCat Tests on Cloudformation Template
---------------
## TITLE

Running/Testing an EKS Open source CloudFormation Template with  zero cost

## DESCRIPTION

To solve this challenge I launched an EKS Open Source CloudFormation Template without any resources being Deployed and then tested the template using TASKCAT.

Link to github repository Used for Taskcat :-
Link to  environment : https://console.aws.amazon.com/cloud9/ide/ce782f19c13d4437b9afeb76e1143e7f
Template URl: https://s3-external-1.amazonaws.com/cf-templates-1u3h9tu4wqweo-us-east-1/2021018Se5-new.templatezdb52ra9ngg

INSTALLATION/ USAGE INSTRUCTIONS

FOR RUNNING TaskCat AND TO PERFORM OTHER INSTRUCTIONS
 I HAVE USED  AWS CLOUD9 

TaskCat uses Python 3 so you will need to install Python, pip (the package installer for Python), and TaskCat via pip in AWS Cloud9.

Here are the instructions for installing these tools using the Cloud9 terminal:

``cd ~/environment
sudo yum -y update
python --version
curl -O https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py --user
sudo pip install --upgrade pip
pip3 install taskcat --user ``


To verify TaskCat is installed, type taskcat --version from the command line. You should see something like this returned from the command line:

 
Create a new GitHub repository:-
I created a new GitHub repository by the name “shubh-s-Taskcat-Repository’ to keep my taskcat file and cf template.


Clone the Repository:-


``cd ~/environment
git clone https://github.com/shubhgarg2401/shubh-s-Taskcat-Repository.git
cd shubh-s-Taskcat-Repository``



Create a .taskcat.yml file
From your Cloud9 terminal, type the following:
``cd ~/environment/shubh-s-Taskcat-Repository
touch .myfile.yml``

Create a CloudFormation Template

From your Cloud9 terminal, type the following:
``cd ~/environment/taskcat-example
touch myfile.yml``

Open the myfile.yml and copy the contents below and save the file.
 >     AWSTemplateFormatVersion: 2010-09-09
        Metadata:
          'AWS::CloudFormation::Designer':
            c2fa7f2d-3f32-46f8-8b78-4633ef12d4f7:
              size:
                width: 60
                height: 60
              position:
                x: 490
                'y': 110
              z: 0
              embeds: []
        Resources:
          EKSC3R7AH:
            Type: 'AWS::EKS::Cluster'
            Properties: {}
            Metadata:
              'AWS::CloudFormation::Designer':
                id: c2fa7f2d-3f32-46f8-8b78-4633ef12d4f7
            Condition: HasNot
        Outputs:
          ExportsStackName:
            Value: !Ref 'AWS::StackName'
            Export:
              Name: !Sub 'ExportsStackName-${AWS::StackName}'### Features
			  
 
Update .taskcat.yml

From your Cloud9 terminal, copy and paste the following into your .myfile.yml file and save the contents.
project:
  name: myfile
  regions:
    - us-east-1
    - us-east-2
tests:
  sqs-test:
    template: ./myfile.yml
 
This is the configuration file that TaskCat uses to know which CloudFormation templates to run and how to run them.
 
 
WORKFLOW

I used the designer Template option to create a template that does not provision any resources as an Output.
I used the EKS Open Source CF template to create the template while changing the outputs and Conditions of the template.

THIS IS THE TEMPLATE I USED:(YAML FORMAT)

		
    AWSTemplateFormatVersion: 2010-09-09
    Metadata:
      'AWS::CloudFormation::Designer':
        c2fa7f2d-3f32-46f8-8b78-4633ef12d4f7:
          size:
            width: 60
            height: 60
          position:
            x: 490
            'y': 110
          z: 0
          embeds: []
    Resources:
      EKSC3R7AH:
        Type: 'AWS::EKS::Cluster'
        Properties: {}
        Metadata:
          'AWS::CloudFormation::Designer':
            id: c2fa7f2d-3f32-46f8-8b78-4633ef12d4f7
        Condition: HasNot
    Outputs:
      ExportsStackName:
        Value: !Ref 'AWS::StackName'
        Export:
          Name: !Sub 'ExportsStackName-${AWS::StackName}'
    

OUTPUT :

Outputs:
  ExportsStackName:
    Value: !Ref 'AWS::StackName'
    Export:
      Name: !Sub 'ExportsStackName-${AWS::StackName}'

CONDITIONS :

HasNot: !Equals [ 'true', 'false' ]

------------------------------------------------------------

RUN TASKCAT
 
From your Cloud9 terminal, type the following command to run TaskCat against your CloudFormation template.
``taskcat test run``

--------------------------------------------------------------------------------------------

DATA FORMATS AND REPORTING

For this challenge I created the cf template using YAML.
I Used the aws cloud9 in the free tier eligibility criteria and installed taskcat on it.
I then simply ran the TASKCAT COMMAND “taskcat test run” 

NOW,
	I tried testing my cf template in two regions,both of which came back as success ,
I validated the template in the designer for syntax errors and got none.
The stack deletion was also a success and I incurred zero cost. 

BUT 

I Realised that the test did not do much as for testing the successful deployment of a stack i need to launch resources as well therefore my test was merely to check availability of resources in the specific region and syntax check.

While i can extend my test to various other regions,i can also automate my test using code build and coode pipeline it would still give me the same result. 
	
I could have used the cfn-linit and cfn-nag test commands to test for error as well but the “launching a cf template without any resource” part won’t allow the proper testing.

SO in conclusion i was able to create an environment to test resources in an automated way but i am still unsure if without launching the resources i can actually test the cf template.
