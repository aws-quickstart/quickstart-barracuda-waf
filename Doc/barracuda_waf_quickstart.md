Barracuda CloudGen WAF for AWS

Quick Start Reference Deployment

July 2020

\<Reese Pitman, Partner organization\>

\<Troy Ameigh, AWS Quick Start team\>\
\<Brett Wolmarans, Barrcuda team\>

> Visit our [GitHub repository](https://github.com/aws-quickstart/tbd)
> for source files and to post feedback,\
> report bugs, or submit feature ideas for this Quick Start.

Table of Contents {#table-of-contents .TOC-Heading}
=================

[Overview 1](#overview)

[Barracuda CloudGen WAF for AWS 2](#barracuda-cloudgen-waf-for-aws)

[Cost and licenses 2](#cost-and-licenses)

[Architecture 3](#architecture)

[Planning the deployment 4](#planning-the-deployment)

[Specialized knowledge 4](#specialized-knowledge)

[AWS account 4](#aws-account)

[Technical requirements 4](#technical-requirements)

[Deployment options 6](#deployment-options)

[Deployment steps 6](#deployment-steps)

[Step 1. Sign in to your AWS account
6](#step-1.-sign-in-to-your-aws-account)

[Step 2. Subscribe to the Barracuda CloudGen WAF for AWS AMI
6](#step-2.-subscribe-to-the-barracuda-cloudgen-waf-for-aws-ami)

[Step 3. Launch the Quick Start 7](#step-3.-launch-the-quick-start)

[Option 1: Parameters for deploying Barracuda Cloud Gen WAF into a new
VPC
8](#option-1-parameters-for-deploying-barracuda-cloud-gen-waf-into-a-new-vpc)

[Option 2: Parameters for deploying Barracuda CloudGen WAF for AWS into
an existing VPC
9](#option-2-parameters-for-deploying-barracuda-cloudgen-waf-for-aws-into-an-existing-vpc)

[Step 4. Test the deployment 11](#step-4.-test-the-deployment)

[Best practices for using Barracuda Cloud Gen WAF on AWS
12](#best-practices-for-using-barracuda-cloud-gen-waf-on-aws)

[Security 12](#security)

[FAQ 12](#faq)

[Send us feedback 13](#send-us-feedback)

[Additional resources 13](#additional-resources)

[Document revisions 14](#document-revisions)

This Quick Start was created by Barracuda Networks in collaboration with
Amazon Web Services (AWS).

[Quick Starts](http://aws.amazon.com/quickstart/) are automated
reference deployments that use AWS CloudFormation templates to deploy
key technologies on AWS, following AWS best practices.

Overview
========

This Quick Start reference deployment guide provides step-by-step
instructions for deploying the Barracuda CloudGen Web Application
Firewall (WAF) on the AWS Cloud.

This Quick Start is for users who use WAFs to protect applications
hosted in AWS. Typically, organizations deploy the Barracuda WAF to
protect web-facing applications they are either deploying in or
migrating to AWS. The Barracuda WAF is designed to offer a
highly-configurable set of controls, enabling easier migration and
security for formerly on-premises workloads now deployed in AWS. It
operates as a Reverse Proxy, inspecting traffic in both directions, so
it also provides Data Loss Prevention features.

Please know that we may share who uses AWS Quick Starts with the AWS
Partner Network (APN) Partner that collaborated with AWS on the content
of the Quick Start.

Barracuda CloudGen WAF for AWS
------------------------------

The WAF runs on the M4 and M5 families of EC2 instances

Cost and licenses
-----------------

You are responsible for the cost of the AWS services used while running
this Quick Start reference deployment. There is no additional cost for
using the Quick Start.

The AWS CloudFormation template for this Quick Start includes
configuration parameters that you can customize. Some of these settings,
such as instance type, affect the cost of deployment. For cost
estimates, see the pricing pages for each AWS service you will use.
Prices are subject to change.

**Tip:** After you deploy the Quick Start, we recommend that you enable
the [AWS Cost and Usage
Report](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-reports-gettingstarted-turnonreports.html).
This report delivers billing metrics to an Amazon Simple Storage Service
(Amazon S3) bucket in your account. It provides cost estimates based on
usage throughout each month and finalizes the data at the end of the
month. For more information about the report, see the [AWS
documentation](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-reports-costusage.html).

This Quick Start requires a license for Barracuda CloudGen WAF for AWS.
There are multiple licensing options to choose from. For those with
existing Barracuda WAF Licenses, a Bring Your Own License option can be
found at the following link
[BYOL](https://aws.amazon.com/marketplace/pp/Barracuda-Networks-Inc-Barracuda-CloudGen-WAF-for-/B014GEC986).
There is also a Pay As You Go option which can be found at the following
link
[PAYG](https://aws.amazon.com/marketplace/pp/B014GEC526?qid=1592267518468&sr=0-3&ref_=srh_res_product_title).
To use the Quick Start in your production environment, sign up for a
license at one of the above links before you launch the Quick Start. If
you selected the BYOL option place the license key in an S3 bucket and
remember its location.

If you don't have a license, you can deploy the Quick Start with a trial
license available in the PAYG option above. The trial license gives you
30 days of free usage, including usage in a production environment.
After this time, you can upgrade to a production license by following
the instructions at the AWS
[marketplace](https://aws.amazon.com/marketplace/pp/B014GEC526?qid=1588809962120&sr=0-2&ref_=srh_res_product_title).

The Quick Start requires a subscription to the Amazon Machine Image
(AMI) for Barracuda CloudGen WAF for AWS; you will add this AMI to your
account by clicking on one of the Licensing options above and following
the subscription process.

Architecture
============

Deploying this Quick Start for a new virtual private cloud (VPC) with
**default parameters** builds the following Barracuda CloudGen WAF for
AWS environment in the AWS Cloud.

![](media/image1.png){width="6.75in" height="4.555555555555555in"}

Figure 1: Quick Start architecture for Barracuda CloudGen WAF for AWS

As shown in Figure 1, the Quick Start sets up the following:

-   A highly available architecture that spans two Availability Zones.\*

-   A VPC configured with public and private subnets, according to AWS
    best practices, to provide you with your own virtual network on
    AWS.\*

-   In the public subnets:

```{=html}
<!-- -->
```
-   A Network Load Balancer pointing to 2 WAF instances

-   2 Barracuda WAF instances

**\*** The template that deploys the Quick Start into an existing VPC
skips the components marked by asterisks and prompts you for your
existing VPC configuration.

Planning the deployment
=======================

Specialized knowledge
---------------------

[]{#_Automated_Deployment .anchor}This Quick Start assumes familiarity
with networking, firewalls, and web security.

This deployment guide also requires a moderate level of familiarity with
AWS services. If you're new to AWS, visit the [Getting Started Resource
Center](https://aws.amazon.com/getting-started/) and the [AWS Training
and Certification website](https://aws.amazon.com/training/). These
sites provide materials for learning how to design, deploy, and operate
your infrastructure and applications on the AWS Cloud.

AWS account
-----------

If you don't already have an AWS account, create one at
[https://aws.amazon.com](https://aws.amazon.com/) by following the
on-screen instructions. Part of the sign-up process involves receiving a
phone call and entering a PIN using the phone keypad.

Your AWS account is automatically signed up for all AWS services. You
are charged only for the services you use.

Technical requirements
----------------------

Before you launch the Quick Start, your account must be configured as
specified in the following table. Otherwise, deployment might fail.

+----------------------------------+----------------------------------+
| [Resources](http:                | If necessary, request [service   |
| //docs.aws.amazon.com/general/la | quota                            |
| test/gr/aws_service_limits.html) | increases](https:                |
|                                  | //console.aws.amazon.com/service |
|                                  | quotas/home?region=us-east-2#!/) |
|                                  | for the following resources. You |
|                                  | might need to do this if an      |
|                                  | existing deployment uses these   |
|                                  | resources, and you might exceed  |
|                                  | the default quotas with this     |
|                                  | deployment. The [Service Quotas  |
|                                  | console](https:                  |
|                                  | //console.aws.amazon.com/service |
|                                  | quotas/home?region=us-east-2#!/) |
|                                  | displays your usage and quotas   |
|                                  | for some aspects of some         |
|                                  | services. For more information,  |
|                                  | see the [AWS                     |
|                                  | documentation](https:/           |
|                                  | /docs.aws.amazon.com/servicequot |
|                                  | as/latest/userguide/intro.html). |
|                                  |                                  |
|                                  |   Resource                       |
|                                  |                                  |
|                                  |             This deployment uses |
|                                  |   -----------------              |
|                                  | -------------------------------- |
|                                  | --------- ---------------------- |
|                                  |   VPCs                           |
|                                  |                                1 |
|                                  |   Elastic IP addresses           |
|                                  |                                2 |
|                                  |   AWS Identity and Access Mana   |
|                                  | gement (IAM) security groups   1 |
|                                  |   IAM roles                      |
|                                  |                                1 |
|                                  |   Auto Scaling groups            |
|                                  |                                1 |
|                                  |   Application Load Balancers     |
|                                  |                                1 |
|                                  |   M4.large instances             |
|                                  |                                2 |
|                                  |                                  |
|                                  |                                  |
+----------------------------------+----------------------------------+
| [R                               | This deployment includes         |
| egions](https://aws.amazon.com/a | Barracuda Cloud Gen WAF AMIs     |
| bout-aws/global-infrastructure/) | which are only available in the  |
|                                  | following regions. us-east-1,    |
|                                  | us-east-2, us-west-1, us-west-2, |
|                                  | sa-east-1, eu-central-1,         |
|                                  | eu-west-1, eu-west-2,            |
|                                  | ap-southeast-1, ap-southeast-2,  |
|                                  | ap-northeast-1, ap-northeast-2,  |
|                                  | and ap-south-1. For a current    |
|                                  | list of supported Regions, see   |
|                                  | [Service Endpoints and           |
|                                  | Quotas](https://doc              |
|                                  | s.aws.amazon.com/general/latest/ |
|                                  | gr/aws-service-information.html) |
|                                  | in the AWS documentation.        |
+----------------------------------+----------------------------------+
| [Key                             | Make sure that at least one      |
| pair](https:/                    | Amazon EC2 key pair exists in    |
| /docs.aws.amazon.com/AWSEC2/late | your AWS account in the Region   |
| st/UserGuide/ec2-key-pairs.html) | where you plan to deploy the     |
|                                  | Quick Start. Make note of the    |
|                                  | key pair name. You need it       |
|                                  | during deployment. To create a   |
|                                  | key pair, follow the             |
|                                  | [instructions in the AWS         |
|                                  | documentation](https://          |
|                                  | docs.aws.amazon.com/AWSEC2/lates |
|                                  | t/UserGuide/ec2-key-pairs.html). |
|                                  |                                  |
|                                  | For testing or proof-of-concept  |
|                                  | purposes, we recommend creating  |
|                                  | a new key pair instead of using  |
|                                  | one that's already being used by |
|                                  | a production instance.           |
+----------------------------------+----------------------------------+
| [IAM                             | Before launching the Quick       |
| p                                | Start, you must log in to the    |
| ermissions](https://docs.aws.ama | AWS Management Console with IAM  |
| zon.com/IAM/latest/UserGuide/acc | permissions for the resources    |
| ess_policies_job-functions.html) | and actions the templates        |
|                                  | deploy. The                      |
|                                  | *AdministratorAccess* managed    |
|                                  | policy within IAM provides       |
|                                  | sufficient permissions, although |
|                                  | your organization may choose to  |
|                                  | use a custom policy with more    |
|                                  | restrictions.                    |
+----------------------------------+----------------------------------+

Deployment options
------------------

This Quick Start provides two deployment options:

-   **Deploy Barracuda CloudGen WAF for AWS into a new VPC (end-to-end
    deployment)**. This option builds a new AWS environment consisting
    of the VPC, subnets, security groups, and other infrastructure
    components. It then deploys the Barracuda Cloud Gen WAF into this
    new VPC.

-   **Deploy Barracuda CloudGen WAF for AWS into an existing VPC**. This
    option provisions Barracuda CloudGen WAF for AWS in your existing
    AWS infrastructure.

The Quick Start provides separate templates for these options. It also
lets you configure Classless Inter-Domain Routing (CIDR) blocks,
instance types, and Barracuda CloudGen WAF for AWS settings, as
discussed later in this guide.\
\
Additionaly if you have a backup file from an existing Barracuda
CloudGen WAF deployment you can provide this file during the deployment
phase to configure your new WAF instances.

Deployment steps
================

Step 1. Sign in to your AWS account
-----------------------------------

1.  Sign in to your AWS account at <https://aws.amazon.com> with an IAM
    user role that has the necessary permissions. For details, see
    [Planning the deployment](#planning-the-deployment) earlier in this
    guide.

2.  Make sure that your AWS account is configured correctly, as
    discussed in the [Technical requirements](#technical-requirements)
    section.

Step 2. Subscribe to the Barracuda CloudGen WAF for AWS AMI
-----------------------------------------------------------

This Quick Start requires a subscription to the AMI for Barracuda Cloud
Gen WAF in AWS Marketplace.

1.  Sign in to your AWS account.

```{=html}
<!-- -->
```
1.  Open the page for the [Barracuda CloudGen WAF Pay As you
    Go](https://aws.amazon.com/marketplace/pp/B014GEC526?qid=1590536656862&sr=0-2&ref_=srh_res_product_title)
    for AWS AMI in AWS Marketplace, and then choose **Continue to
    Subscribe**.

2.  Review the terms and conditions for software usage, and then choose
    **Accept Terms**.

A confirmation page loads, and an email confirmation is sent to the
account owner. For detailed subscription instructions, see the [AWS
Marketplace
documentation](https://aws.amazon.com/marketplace/help/200799470).

1.  When the subscription process is complete, exit out of AWS
    Marketplace without further action. **Do not** provision the
    software from AWS Marketplace---the Quick Start deploys the AMI for
    you.

Step 3. Launch the Quick Start
------------------------------

**Note:** You are responsible for the cost of the AWS services used
while running this Quick Start reference deployment. There is no
additional cost for using this Quick Start. For full details, see the
pricing pages for each AWS service used by this Quick Start. Prices are
subject to change.

1.  Sign in to your AWS account, and choose one of the following options
    to launch the AWS CloudFormation template. For help with choosing an
    option, see [deployment options](#_Automated_Deployment) earlier in
    this guide.

  -------------------------------- --------------------------------
  Deploy Barracuda CloudGen WAF\   Deploy Barracuda CloudGen WAF\
  for AWS - BYOL\                  for AWS - BYOL\
  into a new VPC                   into an existing VPC

                                   

  Deploy Barracuda CloudGen WAF\   Deploy Barracuda CloudGen WAF\
  for AWS - PAYG\                  for AWS - PAYG\
  into a new VPC                   into an existing VPC
  -------------------------------- --------------------------------

**Important:** If you're deploying Barracuda CloudGen WAF for AWS into
an existing VPC, make sure that your VPC has two public subnets in
different Availability Zones for the WAF instances, and that the subnets
aren't shared. This Quick Start doesn't support [shared
subnets](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html).

Also, make sure that the domain name option in the DHCP options is
configured as explained in the [Amazon VPC
documentation](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html).
You provide your VPC settings when you launch the Quick Start.

Each deployment takes about 15 minutes to complete.

3.  Check the AWS Region that's displayed in the upper-right corner of
    the navigation bar, and change it if necessary. This is where the
    network infrastructure for Barracuda CloudGen WAF for AWS will be
    built. The template is launched in the us-west-2 Region by default.

4.  On the **Create stack** page, keep the default setting for the
    template URL, and then choose **Next**.

5.  On the **Specify stack details** page, create a stack name if
    needed. Review the parameters for the template. Provide values for
    the parameters that require input. For all other parameters, review
    the default settings and customize them as necessary.

In the following tables, parameters are listed by category and described
separately for the two deployment options:

-   [Parameters for deploying Barracuda CloudGen WAF for AWS into a new
    VPC](#option-1-parameters-for-deploying-barracuda-cloud-gen-waf-into-a-new-vpc)

-   [Parameters for deploying Barracuda CloudGen WAF for AWS into an
    existing
    VPC](#option-2-parameters-for-deploying-barracuda-cloudgen-waf-for-aws-into-an-existing-vpc)

When you finish reviewing and customizing the parameters, choose
**Next**.

### Option 1: Parameters for deploying Barracuda Cloud Gen WAF into a new VPC

[View template](https://s3.amazonaws.com/quickstart-reference/)

> *VPC network configuration:*

  ---------------------------------------------------------------------------------------------------------------
  Parameter label (name)   Default            Description
  ------------------------ ------------------ -------------------------------------------------------------------
  VPC CIDR\                192.168.0.0/16     CIDR block for the VPC.
  (VPCCIDR)                                   

  Private subnet 1 CIDR\   192.168.10.0/24    CIDR block for the private subnet located in Availability Zone 1.
  (PrivateSubnet1CIDR)                        

  Private subnet 2 CIDR\   192.168.11.0/24    CIDR block for the private subnet located in Availability Zone 2.
  (PrivateSubnet2CIDR)                        

  Public subnet 1 CIDR\    192.168.20.0/24    CIDR block for the public subnet located in Availability Zone 1.
  (PublicSubnet1CIDR)                         

  Public subnet 2 CIDR\    1092.168.21.0/20   CIDR block for the public subnet located in Availability Zone 2.
  (PublicSubnet2CIDR)                         

                                              
  ---------------------------------------------------------------------------------------------------------------

> *Barracuda WAF configuration:*

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Parameter label (name)   Default            Description
  ------------------------ ------------------ ------------------------------------------------------------------------------------------------------------------------------------------------
  Key pair name\           *Requires input*   Enter the public/private key pair you created in your preferred AWS Region; see the [Technical requirements](#technical-requirements) section.
  (KeyPairName)                               

  License Bucket\          *Optional*         The S3 Bucket you have stored your BYOL license file.
  (LicenseBUcket)                             
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> *AWS Quick Start configuration:*

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Parameter label (name)        Default                               Description
  ----------------------------- ------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Quick Start S3 bucket name\   aws-quickstart                        The S3 bucket that you created for your copy of Quick Start assets. Use this if you decide to customize the Quick Start. This bucket name can include numbers, lowercase letters, uppercase letters, and hyphens but should not start or end with a hyphen.
  (QSS3BucketName)                                                    

  Quick Start S3 key prefix\    quickstart- Barracuda-CloudGen-WAF/   The [S3 key name prefix](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html) that is used to simulate a folder for your copy of Quick Start assets. Use this if you decide to customize the Quick Start. This prefix can include numbers, lowercase letters, uppercase letters, hyphens, and forward slashes.
  (QSS3KeyPrefix)                                                     
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Option 2: Parameters for deploying Barracuda CloudGen WAF for AWS into an existing VPC

[View template](https://s3.amazonaws.com/quickstart-reference/)

*Network configuration:*

  -----------------------------------------------------------------------------------------------------------------------------------------------------
  Parameter label (name)   Default            Description
  ------------------------ ------------------ ---------------------------------------------------------------------------------------------------------
  VPC ID\                  *Requires input*   Enter the ID of your existing VPC (e.g., vpc-0343606e).
  (VPCID)                                     

  Public subnet 1 ID\      *Requires input*   Enter the ID of the private subnet in Availability Zone 1 in your existing VPC (e.g., subnet-a0246dcd).
  (PublicSubnet1ID)                           

  Public subnet 2 ID\      *Requires input*   Enter the ID of the private subnet in Availability Zone 2 in your existing VPC (e.g., subnet-b58c3d67).
  (PublicSubnet2ID)                           
  -----------------------------------------------------------------------------------------------------------------------------------------------------

*Amazon EC2 configuration:*

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Parameter label (name)   Default            Description
  ------------------------ ------------------ ------------------------------------------------------------------------------------------------------------------------------------------------
  Key pair name\           *Requires input*   Enter the public/private key pair you created in your preferred AWS Region; see the [Technical requirements](#technical-requirements) section.
  (KeyPairName)                               

  License Bucket\          *Requires Input*   The S3 Bucket you have stored your BYOL license file.
  (LicenseBUcket)                             
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> *AWS Quick Start configuration:*

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Parameter label (name)        Default                               Description
  ----------------------------- ------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Quick Start S3 bucket name\   aws-quickstart                        The S3 bucket that you created for your copy of Quick Start assets. Use this if you decide to customize the Quick Start. This bucket name can include numbers, lowercase letters, uppercase letters, and hyphens but should not start or end with a hyphen.
  (QSS3BucketName)                                                    

  Quick Start S3 key prefix\    quickstart- Barracuda-CloudGen-WAF/   The [S3 key name prefix](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html) that is used to simulate a folder for your copy of Quick Start assets. Use this if you decide to customize the Quick Start. This prefix can include numbers, lowercase letters, uppercase letters, hyphens, and forward slashes.
  (QSS3KeyPrefix)                                                     
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

6.  On the options page, you can [specify
    tags](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-resource-tags.html)
    (key-value pairs) for resources in your stack and [set advanced
    options](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-add-tags.html).
    When you're done, choose **Next**.

7.  On the **Review** page, review and confirm the template settings.
    Under **Capabilities**, select the two check boxes to acknowledge
    that the template creates IAM resources and might require the
    ability to automatically expand macros.

8.  Choose **Create stack** to deploy the stack.

9.  Monitor the status of the stack. When the status is
    **CREATE_COMPLETE**, the Barracuda CloudGen WAF for AWS cluster is
    ready.

10. Use the URLs displayed in the **Outputs** tab for the stack, as
    shown in Figure 2, to view the resources that were created.

![C:\\Users\\handans\\AppData\\Local\\Temp\\SNAGHTML55d15e82.PNG](media/image2.png){width="6.75in"
height="3.4554352580927383in"}

Figure 2: \<software\> outputs after successful deployment

Step 4. Test the deployment
---------------------------

 Note the Public IP address of the newly deployed Barracuda CloudGen
WAF. Open the browser and enter the noted IP with port 80 for HTTP:
http://IP-Address:8000

 Use "admin" and the instance-id for the WAF from the EC2 page in the
AWS console. On the CloudGen WAF GUI go to Advanced, System
Configuration and set Show Advanced Settings to Yes.

![Showing advanced settings](media/image3.png){width="6.75in"
height="0.9958333333333333in"}

 On the CloudGen WAF GUI go to Basic, Services and create a new service
for your web app. You need to provide: a service name, select the type
and port, and for the moment put a dummy IP (like 1.1.1.1) into the Real
Servers box:

 Once the service and server have created then click "Edit" alongside
the Server that was created. Change the identifier to "Hostname" and
fill in the domain name of your web app into the Hostname field.

Best practices for using Barracuda Cloud Gen WAF on AWS
=======================================================

##### 

##### Cluster for High Availability (HA) and redundancy

Due to the 24/7 nature of web traffic, it is important that any
deployments in line with the data path have added redundancy. The
Barracuda Web Application Firewalls configured in HA clusters will
automatically synchronize security and network configurations between
the clusters to provide seamless failover in response to disruptions.
This is achieved by creating an autoscaling group of WAF clusters. IF
you are using the BYOL template you will need licenses for the max
number of instances you anticipate on scaling to. For more information
on clustering, see [High
Availability](https://campus.barracuda.com/doc/4259911/). 

Security
========

The Barracuda Web Application Firewall provides features to implement
user authentication and access control. You can create a virtual private
network (VPN) tunnel to control user access to websites. The user-access
features allow you to specify who can access your websites and what
access privileges each user has. By combining these with SSL encryption,
you can create a secure VPN tunnel to your websites.

Authentication can be implemented only for HTTP or HTTPS services. The
authentication process requires users to provide a valid name and
password to gain access. A validated user has qualified access to the
website; that is, the data and services this user can access depend on
his or her authorization privileges.

FAQ
===

**Q.** I encountered a **CREATE_FAILED** error when I launched the Quick
Start.

**A.** If AWS CloudFormation fails to create the stack, we recommend
that you relaunch the template with **Rollback on failure** set to
**No**. (This setting is under **Advanced** in the AWS CloudFormation
console, **Options** page.) With this setting, the stack's state is
retained and the instance is left running, so you can troubleshoot the
issue. (For Windows, look at the log files in
%ProgramFiles%\\Amazon\\EC2ConfigService and C:\\cfn\\log.)

**Important:** When you set **Rollback on failure** to **No**, you
continue to incur AWS charges for this stack. Please make sure to delete
the stack when you finish troubleshooting.

For additional information, see [Troubleshooting AWS
CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/troubleshooting.html)
on the AWS website.

**Q.** I encountered a size limitation error when I deployed the AWS
CloudFormation templates.

**A.** We recommend that you launch the Quick Start templates from the
links in this guide or from another S3 bucket. If you deploy the
templates from a local copy on your computer or from a location other
than an S3 bucket, you might encounter template size limitations. For
more information about AWS CloudFormation quotas, see the [AWS
documentation](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html).

Send us feedback
================

To post feedback, submit feature ideas, or report bugs, use the
**Issues** section of the [GitHub
repository](https://github.com/aws-quickstart/tbd) for this Quick Start.
If you'd like to submit code, please review the [Quick Start
Contributor's Guide](https://aws-quickstart.github.io/).

Additional resources
====================

**AWS resources**

-   

-   [Getting Started Resource
    Center](https://aws.amazon.com/getting-started/)[AWS General
    Reference](https://docs.aws.amazon.com/general/latest/gr/)

-   [AWS
    Glossary](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html)

**AWS services**

-   

-   [AWS
    CloudFormation](https://docs.aws.amazon.com/cloudformation/)[Amazon
    EBS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)

-   [Amazon EC2](https://docs.aws.amazon.com/ec2/)

-   [IAM](https://docs.aws.amazon.com/iam/)

-   [Amazon VPC](https://docs.aws.amazon.com/vpc/)

**Barracuda CloudGen WAF for AWS documentation**

-   [Barracuda CloudGen WAF](https://www.barracuda.com/aws)

**Other Quick Start reference deployments**

-   [AWS Quick Start home page](https://aws.amazon.com/quickstart/)

Document revisions
==================

  Date            Change                In sections
  --------------- --------------------- -------------
  July 2020       Initial publication   ---
  October 2020.   Revised               
