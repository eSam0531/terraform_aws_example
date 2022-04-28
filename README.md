# Terraform with AWS

This code was built while following along the "Learning Terraform" course found in Linkedin Learning:
https://www.linkedin.com/learning/learning-terraform-2/

## Prerequisites:
1. Terraform CLI
2. AWS CLI
3. AWS Account and Credentials

## What is Terraform?
Terraform is an Infrastructure as code (IaC) tool that allows you to manage infrastructure with configuration files rather than through a graphical user interface. It allows you to build, change, and manage your infrastructure in a safe, consistent, and repeatable way by defining resource configurations that you can version, reuse, and share.

Terraform's configuration language is declarative, meaning that it describes the desired end-state for our infrastructure (it does not require step-by-step instructions). Terraform providers automatically calculates dependencies between resources to create or destroy them in the correct order. Terraform figures out the hard part of resource ordering and lets you just treat the infrastructure as static code.

## Parts of a Terraform Configuration File:
* Terraform Block
    * The terraform block contains Terraform settings, including the required_providers Terraform will use to provision your infrastructure.
    * For each provider block, the source attribute defines an optional hostname, a namespace, and the provider type.
    * Terraform installs providers from the Terraform Registry by default.
    * The version attibute is optional, but is recommeneded so that Terraform does not install a version of the provider that does not work with our configuration.
        * If not specified, Terraform will automatically download the most recent version during initialization.
* Provider Block
    * The provider block configures the specified provider, in this example we are using AWS
    * The provider is a plugin that Terraform uses to create and manage your resources.
* Resource Block
    * The resource block defines components of your infrastructure.
    * A resource might be a physical or virutal component, or it can be a logical resource such as a Heroku application.
    * Resource blocks have two strings before the block begins:
        * Resource Type
        * Resource Name
    * Resource blocks contain arguments which you use to configure the resource.
        * Arguments can include things like machine sizes, disk image names, or VPC IDs.

## Terraform Style:
* Indent two spaces
* Single meta-arguments first
* Block meta-arguments last
* Blank lines for clarity
* Group single arguments
* Think about readability
* Line up the equal signs within a block

## Basic Terraform CLI commands:
* *terraform init*
    * Initializes a configuration directory, downloads and installs the providers defined in the configuration
        * providers are installed in a hidden subdirectory of the current working directory by the name of *.terraform*
    * Creates a lock file named *.terraform.lock.hcl* which specifies the exact provider versions used, so that you can control when you want to update the providers used for your project.
* *terraform fmt*
    * Formats your configuration and will pring out the names of the files it modified, if any.
* *terraform validate*
    * Makes sure your configuration is syntactically valid and internally consistent.
* *terraform apply*
    * Applies the configuration
        * Before configuration is applied, Terraform prints our the "execution plan" which describes the actions Terraform will take in order to chagne your infrastructure to match the configuration.
        * If the instance already exists Terraform will only execute any changes necessary.
        * If command is run and no changes have been made a *"No changes"* message will show.
        * Terraform will pause and wait for your approval before proceeding. If anything in the plan seems incorrect or dangerous, it is safe to abort here with no changes made to your infrastructure.
            * If the execution plan is acceptable type "yes" to proceed.
        * Symbols used to denote approach of changes or initialization:
            * *"+"* : creates that particular resource
            * *"-"* : destroys that particular resource
    * When configuration is applied, Terraform writes data into a file called *terraform.tfstate*
        * Here Terraform store the IDs and properties of the resources it manages so that it can update or destroy those resources as required going forward.
        * This file is the only way Terraform can track which resources it manages (**This file needs to be secured**)
        * In production it is recommended to store the state remotely with Terraform Cloud or Enterprise.
* *terraform destroy*
    * Terminates resources managed by your Terraform project.

## Additional Resources:
* Terraform Website: https://www.terraform.io/
* Terraform Language Documentation: https://www.terraform.io/language
* Terraform Providers: https://registry.terraform.io/browse/providers
* AWS CLI: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
* AWS Account: https://aws.amazon.com/free/
* AWS Credentials: https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html