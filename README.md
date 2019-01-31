# TF_Book_Ch_1

#### Note: This is the first of series of repositories for "Terraform Up & Running" book. I will have a separate repository for each chapter. Each repository will have files with Terraform (or other tools that are discussed in the book) code and README.md with expalnation what the repository does. 

### List of files in the repository:
- `bash_webserver.sh` - bash script that installs and configures webserver. 
- `packer_webserver.json` - `packer` template code that creates VM image with webserver on it.
- `terraform_webserver.tf` - `terraform` configuration code that deploys webserver. 
---------------------------------------------------------------------------------------------------------------------------

### How to run each of the files in the repository:

 #### Running the `bash` script file:
  - execute `bash bash_webserver.sh` command (this script should be run on Ubuntu server)
  - the script updates apt-get cache, installs PHP and Apache, copy code form repository and starts Apache server.
  
---------------------------------------------------------------------------------------------------------------------------

#### Running the `packer` template file:
  - **pre-requisites**
    - first you need to install `packer` from [here](https://www.packer.io/)
    - next you need to setup Amazon Web Services (AWS) account [here](https://aws.amazon.com/)
    - next you need to configure your AWS access keys [here](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)
    - lastly you need to configure your AWS access keys as environment variables:
      ```
      export AWS_ACCESS_KEY_ID=(your access key id)
      export AWS_SECRET_ACCESS_KEY=(your secret access key)
      ```
  - execute `packer validate packer_webserver.json` - to validate the syntax and configuration of the template.
  - execute `packer build packer_webserver.json` -  to start building the VM image.
  
  - if the commands succeed the output should diplay the following:
  ```
   Build 'amazon-ebs' finished.

   ==> Builds finished. The artifacts of successful builds are:
   --> amazon-ebs: AMIs were created:
   us-east-1: ami-0123abcd456dsds34
  ```
------------------------------------------------------------------------------------------------------------------
#### Running the `terraform` configuration file:
  - **pre-requisites**
    - first you need to install `terraform` from [here](https://www.terraform.io/downloads.html)
    - next you need to setup Amazon Web Services (AWS) account [here](https://aws.amazon.com/)
    - next you need to configure your AWS access keys [here](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)
    - lastly you need to configure your AWS access keys as environment variables:
      ```
      export AWS_ACCESS_KEY_ID=(your access key id)
      export AWS_SECRET_ACCESS_KEY=(your secret access key)
      ```
  - execute `terraform init` - to initialize the working directory
  - execute `terraform plan` - to create execution plan for changes to be applied.
  - execute `terraform apply`	- to apply the desired changes.
  
  - if the commands succeed the output should diplay the following:
  ```
   aws_instance.app: Creation complete after 42s (ID: i-057dca7b92711929f)

   Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

  ```
  
 - execute `terraform destroy` - to destroy the resource that we just created.

 - if the command succeeds the output should diplay the following:
  ```
   aws_instance.app: Destruction complete after 1m52s

    Destroy complete! Resources: 1 destroyed.
  ```


  
