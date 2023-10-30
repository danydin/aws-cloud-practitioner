# aws-cloud-practitioner
## concepts - ELI5:

test test

### S3 bucket & objects
#### acl vs public bucket policy vs access point policies
##### ACLs: ACLs are a legacy method of controlling access to S3 resources. ACLs are attached to individual S3 objects or buckets and are used to grant or deny permissions to specific users or groups. ACLs can be used to define fine-grained access control for your S3 resources, but can be difficult to manage at scale. Bucket policies: are JSON-based documents that are attached to an S3 bucket and are used to control access to the bucket and its objects. Bucket policies can be used to grant or deny permissions to specific users, groups, or AWS accounts, and can be used to define fine-grained access control for your S3 resources. Bucket policies are more flexible and easier to manage than ACLs, and can be used to define more complex access control scenarios. Access point policies: Access point policies are JSON-based documents that are attached to an S3 access point and are used to control access to the access point and its objects. Access point policies can be used to grant or deny permissions to specific users, groups, or AWS accounts, and can be used to define fine-grained access control for your S3 resources. Access point policies are similar to bucket policies, but are attached to an access point instead of a bucket. The main difference between bucket policies and access point policies is the scope of the policy. Bucket policies apply to the entire bucket and all of its objects, while access point policies apply only to the access point and its objects. This means that access point policies can be used to define more granular access control for specific access points, while bucket policies provide broader access control for entire buckets.
#### bucket policy vs user policy vs arn
##### In AWS S3, bucket policies and user policies are two types of policies that are used to control access to S3 resources. ARN (Amazon Resource Name) is a unique identifier for an AWS resource, such as an S3 bucket or object. ARNs are used to specify the resource to which the policy applies. Bucket policies are attached to an S3 bucket and are used to control access to the bucket and its objects. user policies on the other hand are attached to an IAM user or group and are used to control access to specific S3 resources, by going to IAM dashboard in the aws search console you can create an IAM USER OR GROUP and attach one or more policies to the user or group. User policies are attached to individual IAM users, while group policies are attached to IAM groups, depends on what you defined and configured at IAM DASHBOARD.
#### object writer
##### object writer is a user or application that has permission to write objects to an S3 bucket. An object writer can upload new objects to an S3 bucket, modify existing objects, or delete objects from the bucket. you edit the premissio under the bucket premission tab then choose bucket policy -> edit and enter a json format policy to grant premission by specifcing the user arn id and specify what is allowed to edit, add, remove etc. Object write permission can be granted using S3 bucket policies or IAM policies, allowing you to control access to your S3 resources and improve security.
#### sse-s3 encryption
##### (Server-Side Encryption with S3-Managed Keys) is a feature that provides encryption of S3 objects at rest. SSE-S3 automatically encrypts objects when they are stored in S3, and decrypts them when they are retrieved. When SSE-S3 is enabled, S3 uses 256-bit Advanced Encryption Standard (AES-256) encryption to encrypt objects. The encryption keys are managed by S3, and are stored separately from the objects themselves. This provides an additional layer of security for your S3 objects, as it ensures that the encryption keys are not accessible to unauthorized users. With SSE-S3 enabled, all objects that are uploaded to the bucket will be automatically encrypted with AES-256 encryption. When objects are retrieved, S3 automatically decrypts them using the encryption keys that are managed by S3. It's worth noting that there are other methods of encrypting S3 objects, such as SSE-KMS (Server-Side Encryption with AWS KMS-Managed Keys) and SSE-C (Server-Side Encryption with Customer-Provided Keys). These methods provide more granular control over encryption keys and can be used in conjunction with SSE-S3 to provide comprehensive encryption of S3 objects. the encryption is used at "REST" only which means it protects against unauthorized access or data breaches to the PHYSICAL storage device, such as a hard drive or solid-state drive ONLY.
#### bucket key - enabled
##### bucket key enabled is a feature that allows you to use AWS KMS (Key Management Service) to manage the encryption keys for your S3 objects. When bucket key enabled is enabled, S3 generates a unique data key for each object that is stored in the bucket, and then encrypts the data key using a KMS customer master key (CMK) that the aws user provided when choosing to enable this option. Bucket key enabled can be used in conjunction with SSE-S3 (Server-Side Encryption with S3-Managed Keys) to provide additional encryption of S3 objects. When both bucket key enabled and SSE-S3 are enabled, S3 uses a unique data key for each object that is stored in the bucket, and encrypts the data key using a KMS customer master key (CMK). The data itself is also encrypted using SSE-S3.
#### s3 static website hosting
##### S3, static website hosting is a feature that allows you to host static websites directly from an S3 bucket. Static websites are websites that consist of HTML, CSS, JavaScript, and other static files, and do not require server-side processing or dynamic content. With static website hosting enabled, your S3 bucket will be configured to serve your static website files as a website. You can access your website using the endpoint URL that is provided in the "Static website hosting" section of the bucket properties.  If your website requires server-side processing or dynamic content, you may need to use a different hosting solution, such as Amazon EC2 or AWS Elastic Beanstalk. Overall, static website hosting in AWS S3 is a simple and cost-effective way to host static websites directly from an S3 bucket. It's easy to set up and can be used for a variety of use cases, such as personal websites, blogs, and small business websites. S3 simply serves the static website files directly from the bucket, using the bucket like a webserver by indicating the default index.html and error.html that the user provided as the entry point for the url that aws provides.
#### s3 virtual hosted style url vs a path style url
##### In AWS S3, there are two types of URLs that can be used to access S3 objects: virtual hosted style URLs and path style URLs. Virtual hosted style URLs are URLs that use the BUCKET NAME as part of the domain name in the URL. For example, a virtual hosted style URL for an S3 object might look like this: http://mybucket.s3.amazonaws.com/myobject - Path style URLs, on the other hand, are URLs that use the bucket name as part of the PATH in the URL. For example, a path style URL for the same S3 object might look like this: http://s3.amazonaws.com/mybucket/myobject - Virtual hosted style URLs are generally preferred over path style URLs, as they provide better performance and scalability. Virtual hosted style URLs allow S3 to distribute requests across multiple servers, which can improve performance and reduce latency. Path style URLs, on the other hand, require S3 to route all requests through a single server, which can limit performance and scalability.

### ec2 (elastic compute cloud)
#### ami
##### amazon-machine-image is required to launch an instance in AWS. it convenient way to launch instances with pre-configured software and settings, This allows you to launch instances with the same configuration as the original AMI, including the same hardware resources and network settings. You can choose from a variety of pre-configured AMIs provided by AWS or the AWS Marketplace, or create your own custom AMI to meet your specific needs.
#### instance type (server type)
##### instance type is a specification that defines the hardware resources, such as CPU, memory, and storage, that are available for an EC2 instance. Each instance type is optimized for specific use cases and workloads, and provides a different balance of compute, memory, and storage resources.
#### storage gib & root volume & ebs & gp3 iops
##### Storage in EC2 is measured in gibibytes (GiB), which is a binary unit of measurement that is equivalent to 1,073,741,824 bytes. The root volume is the primary storage device that is attached to an EC2 instance and is used to store the operating system and other system files. EBS (Elastic Block Store) volumes are used to store data and can be attached and detached from instances as needed. GP3 (general purpose ssd) are EBS volumes that provide a flexible and cost-effective way to provision storage with customizable IOPS (Input/Output Operations Per Second) and throughput.
#### Compute vCPUs 
##### Compute resources in EC2 are measured in vCPUs (virtual CPUs), which are allocated to instances based on the instance type. Each instance type provides a different balance of compute, memory, and storage resources, and is optimized for specific use cases and workloads.
#### Snapshots (frequency and size changed per snapshot)
##### EBS snapshots are point-in-time copies of EBS volumes that can be used to back up and restore data. The frequency and size of EBS snapshots can be customized based on your specific backup and recovery requirements.
#### Data transfer (inbound and outbound data transfer and intraregion data transfer)
##### Inbound and outbound data transfer in EC2 is measured in gigabytes (GB) and is charged based on the amount of data transferred. Intra-region data transfer, which is data transfer between EC2 instances in the same AWS region, is typically free or charged at a lower rate than inter-region data transfer.
#### key pair
##### a key pair is a set of public and private keys that are used to securely connect to an EC2 instance. When you launch an EC2 instance, you can specify a key pair that will be used to authenticate on every connections to the instance. You do so by generating a public and private key pair using a tool such as ssh-keygen command. the public key is stored inside the instance and is used to verify every connection to the instance, so don't lose the private key as you won't be able to connect to the instance without it. You can connect to DIFFERENT INSTANCES with the same key pair AS LONG AS they are in the same REGION. keeping the key private is super important as access to it means access to the instance.
#### user data (optinal meta-data script)
##### User data is an optional feature that used to automate the configuration of an instance when it first lunch (or when stopped and lunched again if the UserData parameter is added to it - which occurs by default if you change the user data script). the user data script used to perform a wide range of tasks, such as configuring network settings, installing packages, and running scripts. (Limits: User data is limited to 16 KB in size for Linux instances and 32 KB for Windows instances)
#### instance connect vs session manager vs ssh vs serial console
##### ec2 provides a different way to connect to your EC2 instances and manage them. 1. EC2 Instance Connect: EC2 Instance Connect is a browser-based SSH connection manager that allows you to securely connect to your EC2 instances using the AWS Management Console. EC2 Instance Connect uses AWS Identity and Access Management (IAM) to control access to your instances and provides a simple and secure way to connect to your instances without the need for a separate SSH client. 2. Session Manager: Session Manager is a fully managed AWS service that allows you to manage your EC2 instances using a browser-based shell or the AWS CLI (Command Line Interface). Session Manager provides a secure and auditable way to manage your instances without the need for a separate SSH client or VPN connection. 3. SSH: SSH (Secure Shell) is a widely used protocol for securely connecting to remote servers and managing them using a command-line interface. You can use an SSH client, such as PuTTY or OpenSSH, to connect to your EC2 instances using the public IP address or DNS name of the instance. 4. Serial Console: Serial Console is a feature that allows you to troubleshoot and recover your EC2 instances using a serial connection. Serial Console provides access to the boot process and console output of your instances, and can be used to diagnose and fix issues that prevent your instances from starting up.
#### public ipv4 & private ipv4 & public ipv4 dns 
##### each EC2 instance is assigned a public IPv4 address, a private IPv4 address, and a public IPv4 DNS hostname. 1. Public IPv4 address: A public IPv4 address is a globally unique IP address that is assigned to an EC2 instance and can be used to communicate with the instance over the internet. Public IPv4 addresses are assigned dynamically by AWS and can be released and reassigned as needed. 2. Private IPv4 address: A private IPv4 address is an IP address that is assigned to an EC2 instance within a VPC (Virtual Private Cloud) and is used for communication within the VPC. Private IPv4 addresses are not accessible from the internet and are used to isolate and secure your resources. 3. Public IPv4 DNS hostname: A public IPv4 DNS hostname is a fully qualified domain name (FQDN) that is assigned to an EC2 instance and can be used to resolve the public IPv4 address of the instance. Public IPv4 DNS hostnames are assigned dynamically by AWS and can be released and reassigned as needed. the public DNS is connected to the global DNS through amazon's Route 53 service. Route 53 is a clound Domain Name System web service that gives devleopers and busisneses an easy way to route end users to their aws internet applcaiton. when you lunch an ec2 instance amazon autoamtically reates a DNS recrod in Route 53 that maps the public dns hostname to the public ipv4 address of the instnace. this dns record is propagated to dns servers around the world, allowing users to access the isntance using hte public dns hostname. when a user enters the public dns hostane into their web browser the brwoser sends a dns query to a dns server to resolve the hostname to an ip address. the dns server looks up the dns record in route 53 and returns the publci ipv4 address of the instance to the brwoser. the browser then estalbies a conention to the instance using the ipv4 address. so Route 53 service maps the hostname to the public ipv4 address of the instance. NOT all ec2 instances have a public ip, it depends if you decided to add it to the instance or not. if you don't assign pbulic ipv4 the instace will only be accisle within the virtua private cloud (vpc) in which the instance is lunched. if you want to access the internet from it you'll have to use a nat gateway or a bastion host to forward traffic to the instance. assigning ipv4 to an instance may cost money. you can create a public ipv4 to an instance even if it already exists as long as there are avilable ipv4 in the hosts part of the instance's subnet that aren't being used by other instance. if all host ips are used by instances in your subnet you can modify the CIDR of your subnet in the subnets navigation panel in action tab. e.g. changing 10.0.0.0/24 to 10.0.0.0/23 which will expand from 256 ip to 512 ips. however modiying the cidr block will rEQUIRe to update the ip addresses of any instances running in the subnet to reflect the new ip address range by stopping the instance first, then modify the network interface of the isntance to use a new ip address range & go to ec2 console selecet the instance you want to update in actions tab choose networking and then manage network interaces and select the network interace that you want to modify and press actions modify network interface.
#### nacl (network access control list)
##### is a firewall at the subnet level / boundary, it comes with a default one when creating every subnet which allows BY DEFAULT all inbound and outbound traffic but you can create a custom nacl and attach/assoicate it with your subnet. you can attach multiple subnets to NACL, but only 1 nacl can be attached to each subnet. nacl are stateless and required specific rules for inbound and outbound traffic
#### firewall security groups rules
##### security groups are a firewall on a INSTANCE level (website, db, virtual machine etc). by default the security group that attached to each instance denys all inbound and ALLOWS all outbound traffic. security groups are statefull and allows responses to inbound traffic automatically without the need to configure outbound traffic and same for vice versa. unlike NACL where if one rule allows the traffic it will pass (sorted by order from 100 which is the strongest, 200 weaker then 300 etc), in security groups all the rules are evulated before deciding whether to allow traffic in / out or not, traffic can be restricted by ip type (ssh,), protocol (tcp, http), port range (80, 443), traffic soucce (cidr-classless inter domain routes) example of using security groups: webserver instance allows inbound traffic from internet 0.0.0.0/0 for https port 443. the application instance allows http port 80 from the webserver instance only. the database instance allows inbound traffic on tcp port 3306 from application instance ip only. and remmeber secuirty groups are stateful so no need to configure outbound rules as it's automatically sent back. this creates very safety network as even if someone hacks the webserver and wants to steal data they still can't access the database directly.

### VPC
#### VPC
##### a vpc (virtual private cloud) provide a flexible and scalable way to isolate and secure your AWS resources. A VPC provides a private network that is isolated from the public internet. This allows you to securely connect your AWS resources without exposing them to the internet. and control access to your resources using security groups and network ACLs.
#### subnet
##### Within a VPC, you can create subnets that are used to segment your network resources. Each subnet is associated with a specific availability zone and provides a range of IP addresses that can be used by your resources. Each subnet can have its own security groups and network ACLs (Access Control Lists), which are used to control access to the resources in the subnet.
#### route table
##### Each subnet has its own routing table, which is used to route traffic between the resources in the subnet and between other resources in the VPC such as ec2 (virtual server instances), rds instances (relatioal database service), elastic load balancers (Load Balancers are managed load balancing services that can be launched in a VPC and are used to distribute traffic across multiple EC2 instances), nat gateway (Network Address Translation gateways are used to enable internet communication for resources in private subnets).
#### internet gateway - igw
##### an internet gateway (IGW) is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. An internet gateway provides a target in your VPC route tables for internet-routable traffic, and performs network address translation (NAT) for instances that have been assigned public IP addresses (public subnet).
#### nat gateway - nat (network address translation)
##### nat gateway translate the ip address of a private subnet into the nat gateway ip address in order to commuincate with the INTERNET from the PRIVATE subnet. when a request is sent from a private subnet or the internet that looks to reach the private subnet the nat gateway is the ONLY gateway the translate the request to / from the private ip address of the subnet. To setup a nat gateway in the public subnet, you must also specificy an elastic ip while creating the NAT gateway in a public subnet. after creating the NAT gateway you must add to the route table of the PRIVATE subnet the 0.0.0.0 IP destination with the target as nat-gwy-id** (ipv4 only) for ipv6 use egress-only-igw which allows connection from private subnets to the internet in your vpc which also blocks direct communication between the internet to the private subnet and add to the private subnet route table the ::/0 - eigw-id** , egress only is stateful so it remmbers who it sent the content to and allows automatically to get back a response from the destination if inbound premission isn't allowed to the private subnet. To allows access to the internet from / to the private subnet you MUST also configure a route table inside the private subnet to allow specific types of traffic and ips to & from the subnet. 
#### vpc peering
##### connecting different vpcs to each other (also from different aws accounts), so data-information can be transferred between varies vpc's instaces. you add to the route table of the requester vpc: 1. destination=the cidr block of the reciever vpc. 2. target=pcx-** (peering connection). only a direct connection between peers exists (if both VPC A & C connects to VPC B via peering, A and C CAN NOT communicate with each other) aka tranitive or edge to edge routing 
#### root user VS IAM user
##### In AWS, the root user is the initial user account that is created when you first create an AWS account. The root user has full access to all AWS services and resources in the account, and can perform any action on those resources. As such, it is recommended that you do not use the root user for day-to-day activities, but instead create and use IAM (Identity and Access Management) users. IAM users are separate user accounts that you can create and manage within your AWS ROOT account. IAM users have specific permissions that you can control and manage, allowing you to grant or restrict access to AWS services and resources as needed. IAM users can be assigned to groups, which can simplify the process of managing permissions for multiple users. this provides improved security (limit scope to your resources), accountability (track and audit actions taken by individual users), management (can control access of all users to every resource from one account)


### Q&A
Q: If i create an igw and added the route table to it from the public instance do i need to open security premsision or it's already acccessible to the internet?
A: If you have created an internet gateway (IGW) and added the route table to it from a public instance in your AWS VPC (Virtual Private Cloud), you may still need to configure security group rules to allow inbound traffic from the internet to your instance. 
Security groups: Security groups act as a virtual firewall that controls inbound and outbound traffic to your instances. By default, security groups deny all inbound traffic and allow all outbound traffic. 
Inbound rules: To allow inbound traffic from the internet to your instance, you must create inbound rules in your security group that allow traffic on specific ports and protocols. 
Outbound rules: To allow outbound traffic from your instance to the internet, you must create outbound rules in your security group that allow traffic on specific ports and protocols. 
Overall, while an internet gateway provides internet connectivity to instances in your VPC, you still need to configure security group rules to control access to your instances and other resources. By carefully designing your security groups and using inbound and outbound rules to control traffic, you can ensure that your resources are secure and accessible only to authorized users and applications.

Q: Why do we need VPC PEERING?
A: By default, VPCs are isolated from each other. A PVC peering connection is a networking connection between two VPCs that you can use to route traffic between them by using private ip addresses.

Q: if an instance doesn't have public ipv4 does it mean it is created inside a private subnet?
A: Not necssairly, if an EC2 instance in AWS does not have a public IPv4 address, it's possible that it was launched in a private subnet within a VPC (Virtual Private Cloud) OR the public ip hasn't been assigned yet, to assign a public ip you need to Allocate an Elastic IP address: In the AWS Management Console, navigate to the Elastic IPs page and click "Allocate new address". This will allocate a new Elastic IP address that you can use to assign to your instance. Associate the Elastic IP address with the instance: In the Elastic IPs page, select the Elastic IP address that you want to associate with your instance and click "Actions" > "Associate IP address". In the Associate Elastic IP address dialog box, select the instance that you want to associate the Elastic IP address with and click "Associate". Update the instance's security group rules: To allow inbound traffic to the instance, you must update the security group rules for the instance to allow traffic on specific ports and protocols. Note that you will also need to configure the routing tables for your VPC and subnets to allow traffic to and from the internet.

Q: how do i know if the subnet is private or public?
A: You can determine whether a subnet is public or private by checking its route table configuration.
Navigate to the VPC console: In the AWS Management Console, navigate to the VPC console. 
Select the subnet: Select the subnet that you want to check. 
Check the route table: In the "Details" tab for the subnet, check the "Route table" field. This will show you the route table that is associated with the subnet. 
Check the route table configuration: Navigate to the "Route tables" section of the VPC console and select the route table that is associated with the subnet. Check the route table configuration to see if it has a route to the internet. If the route table has a route to the internet, the subnet is a public subnet. If the route table does not have a route to the internet, the subnet is a private subnet. 
* NOTE :In AWS VPC (Virtual Private Cloud), there is NO BUTTON OPTION to make a subnet either public or private. Whether a subnet is public or private is determined by its route table configuration, which is a logical configuration that you must set up manually.

Q: Does an ec2 resides within a subnet?
A: Yes, an ec2 resides within a subnet, subnet is a range of ip addresses in your vpc.

Q: How to set a vpc peering?
A: 1. go to both the requester and accetper vpc subnet -> route tab -> route table option. copy the local CIDR range for each of the peer subnet vpc.
2. go to peering vpc column on the left menu and add the reqeust and accept vpc with the corresponding subnets that you copied earlier. 
3. accept the request from the approver account (if both vpc on same aws account no need to change account)
* peered VPCs do not necessairly accept all data between them by default. Security features, such as network access control lists and security groups, still apply. Be sure to update them accordingly as well.
4. go to insatnces menu column -> security tab -> click on security groups option. inside inbound rules tab click edit inbound rules -> add in the type custom icmp-ipv4 and in the source the CIDR of the peered vpc subnet. if you need to add different traffic types you need to change the security group accordingly.
* remmeber security groups are stateful which means the response for the request will be allowed to flow from the outbound reciever and into the inbound sender REGARDLESS if there are security groups rules that allows it!

Q:
A:

Q:
A:

Q: 
A:

Q:
A: