# BITCANNA TOOLS
Tools for Bitcanna Network

## Terraform
Deploy a fulllnode for Bitcanna validator to your AWS account

### Prerequisites
* Terraform 0.13 or later
* aws-cli installed
* aws account with access-key and secret-key
* ssh key called user in aws region 

### Parameters to configure
terraform.tfvars     
* image_id      = "ami-0d7b738ade930e24a" # ubuntu 20.04 ami in eu-west-3 region
* instance_type = "t2.medium" # 2 cpu and 4gb ram
* ssh_key       = "user"      # aws ssh keyname    
* user          = "ubuntu"    # aws instance username
* vpc_name      = "agoric"    # vpc name 
* region        = "eu-west-3" # select your prefered aws region
* profile       = "sandbox"   # your aws profile from ~/.aws/credentials

### Instruction
* Navigate to terraform directory
* Edit variables file terraform.tfvars 
* run *terraform init* to initialize modules
* run *terraform apply* to run the configuration
* type *yes* when prompted
* enjoy the action :-)

### How it works
* You registers an account in AWS and choose your prefered region. 
* You create or import the ssh key for future use
* You change the parameters listed above
* You run commands listed above
* Terraform creates a VPC network with private and public subnets
* After VPC is created terraform creates ec2 instance with additional 50GB disk volume for agoric blockchain data directory
* In addition to instance creation, 3 security groups should be created to allow ingress traffic for port 22, 26656 and 26660
* After instance is create, terraform will run provision script to install software dependencies and agoric node binaries
* When terraform finishes the installation job you can ssh to host with user ubuntu and check the sync status with *journalctl -u bcnad.service -f*
