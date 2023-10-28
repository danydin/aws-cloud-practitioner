# aws-cloud-practitioner
## concepts - ELI5:

### S3 bucket

### ec2 
#### ami
##### amazon-machine-image is required to launch an instance in AWS. it convenient way to launch instances with pre-configured software and settings, This allows you to launch instances with the same configuration as the original AMI, including the same hardware resources and network settings. You can choose from a variety of pre-configured AMIs provided by AWS or the AWS Marketplace, or create your own custom AMI to meet your specific needs.


### VPC
#### subnets - 
#####
#### nacl (network access control list)
##### is the firewall at the subnet level / boundary, it comes with a default one when creating every subnet which allows BY DEFAULT all inbound and outbound traffic but you can create a custom nacl and attach/assoicate it with your subnet. you can attach multiple subnets to NACL, but only 1 nacl can be attached to each subnet. nacl are stateless and required specific rules for inbound and outbound traffic
#### security groups
##### is a firewall on a INSTANCE-AMI level(app-alogirthm, website, db, etc). the default security group that attached to each instance-ami denys all inbound and allows all outbound traffic. security groups are statefull and allows responses to inbound traffic automatically without the need to configure outbound traffic and same for vice versa. unlike NACL where if one rule allows the traffic it will pass (sorted by order from 100 which is the strongest, 200 weaker then 300 etc), in security groups all the rules are evulated before deciding whether to allow traffic in / out or not, traffic can be restricted by ip type (ssh,), protocol (tcp, http), port range (80, 443), traffic soucce (cidr-classless inter domain routes ips)
##### example of using security groups: webserver instance allows inbound traffic from internet 0.0.0.0/0 for https port 443. the application instance allows http port 80 from the webserver instance only. the database instance allows inbound traffic on tcp port 3306 from application instance ip only. and remmeber secuirty groups are stateful so no need to configure outbound rules as it's automatically sent back. this creates very safety network as even if someone hacks the webserver and wants to steal data they still can't access the database directly.
#### routes table
#####
#### internet gateway - igw
#####
#### nat gateway - nat - network address translation
##### you need a nat gateway in the PUBLIC subnet to allow internet access the internet & prevent the internet to access the private subnet via the igw (without going through the nat first).
##### the source ip address in the private subnet transform to the nat gateway address in the public subnet, similarly when the response is received from the iternet the nat gateway transalte/transform it back to the private ip address of the private subnet.
##### to setup the nat gateway you mention the public subnet that the nat gateway should reside, you must also specificy an elastic ip while creating the NAT gateway. after creating the NAT gateway you must add to the route table of the PRIVATE subnet the 0.0.0.0 IP destination with the target as nat-gwy-id** (ipv4 only) for ipv6 use egress-only-igw which allows connection from private subnets to the internet in your vpc which also blocks direct communication between the internet to the private subnet and add to the private subnet route table the ::/0 - eigw-id** , egress only is stateful so it remmbers who it sent the content to and allows automatically to get back a response from the destination if inbound premission isn't allowed to the private subnet
#### VPC PEERING
##### connecting different vpcs to each other (also from different aws accounts), so data-information can be transferred between varies vpc's instaces. you add to the route table of the requester vpc: 1. destination=the cidr block of the reciever vpc. 2. target=pcx-** (peering connection). only a direct connection between peers exists (if both VPC A & C connects to VPC B via peering, A and C CAN NOT communicate with each other) aka tranitive or edge to edge routing 
#### ROOT USER VS IAM USER
##### In AWS, the root user is the initial user account that is created when you first create an AWS account. The root user has full access to all AWS services and resources in the account, and can perform any action on those resources. As such, it is recommended that you do not use the root user for day-to-day activities, but instead create and use IAM (Identity and Access Management) users. IAM users are separate user accounts that you can create and manage within your AWS ROOT account. IAM users have specific permissions that you can control and manage, allowing you to grant or restrict access to AWS services and resources as needed. IAM users can be assigned to groups, which can simplify the process of managing permissions for multiple users. this provides improved security (limit scope to your resources), accountability (track and audit actions taken by individual users), management (can control access of all users to every resource from one account)