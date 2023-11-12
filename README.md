# aws-cloud-practitioner

## S3 bucket & objects
Q: acl vs public bucket policy vs access point policies
A: ACL (Access Control List), Public Bucket Policy, and Access Point Policies are different mechanisms in AWS S3 (Simple Storage Service) that allow you to control access to your S3 buckets and objects. Here's a brief explanation of each:
ACL (Access Control List): ACLs are a legacy method of managing access to S3 buckets and objects. With ACLs, you can grant permissions to individual AWS accounts or predefined groups (e.g., authenticated users, all users) at the bucket or object level. ACLs provide basic control over access but can become complex to manage as the number of users and resources increases.
Public Bucket Policy: A Public Bucket Policy is a JSON-based policy that allows you to define permissions for your S3 bucket and its objects. It provides more granular control than ACLs and allows you to specify rules for different types of access (e.g., read, write, list) to specific IP addresses, AWS accounts, or even anonymous users. Public Bucket Policies are commonly used to make specific buckets or objects publicly accessible.
Access Point Policies: Access Points are a feature in S3 that allow you to create unique entry points for accessing your bucket. Access Point Policies are JSON-based policies that are attached to an access point. They provide fine-grained control over access to the objects within the access point. Access Point Policies allow you to define permissions for specific AWS accounts or IAM roles, and you can also specify conditions for access (e.g., time-based access, IP address restrictions).
In summary, ACLs, Public Bucket Policies, and Access Point Policies are different mechanisms for controlling access to S3 buckets and objects. ACLs are a legacy method, while Public Bucket Policies and Access Point Policies provide more granular control and flexibility. Public Bucket Policies are used to make buckets or objects publicly accessible, while Access Point Policies are used to control access to objects through access points. It's recommended to use Public Bucket Policies or Access Point Policies for managing access to S3 resources, as they offer more advanced features and are easier to manage than ACLs.

Q: Explain Bucket Policy
A: A bucket policy attached directly to an S3 bucket in the s3 console.
It is a resource-based policy that allows you to define permissions for the bucket and its objects.
Bucket policies are written in JSON format.
Bucket policies are used to control access to the entire bucket or specific objects within the bucket.
You can grant permissions to AWS accounts, IAM users, IAM roles, or even anonymous users.
Bucket policies are commonly used to make buckets or objects publicly accessible, define cross-account access, or enforce specific access controls for the bucket.

Q: What's object writer
A: an object writer in the context of AWS S3 refers to the entity or component responsible for writing or uploading objects to an S3 bucket. It can be a person using the AWS Management Console, a user executing AWS CLI commands, an application using AWS SDKs, or a third-party tool or library.

Q: explain sse-s3 encryption & bucket key
A: SSE-S3 (Server-Side Encryption with S3) is a feature provided by AWS S3 (Simple Storage Service) that allows you to encrypt your data at rest in S3 buckets. When you enable SSE-S3 encryption, AWS automatically encrypts your objects before storing them in S3 and decrypts them when you retrieve them. at "REST" means it encrypt the data against unauthorized access / data breaches to the PHYSICAL storage device e.g. the solid-state drive.
Enabling SSE-S3 with a bucket key provides an additional layer of security by allowing you to use your own encryption key to protect your data in S3. It gives you more control over the encryption process and ensures that only you have access to the key used for encryption and decryption.

Q: s3 static website hosting
A: S3, static website hosting is a feature that allows you to host static websites directly from an S3 bucket. Static websites are websites that consist of HTML, CSS, JavaScript, and other static files, and do not require server-side processing or dynamic content. With static website hosting enabled, your S3 bucket will be configured to serve your static website files as a website. You can access your website using the endpoint URL that is provided in the "Static website hosting" section of the bucket properties.  If your website requires server-side processing or dynamic content, you may need to use a different hosting solution, such as Amazon EC2 or AWS Elastic Beanstalk. Overall, static website hosting in AWS S3 is a simple and cost-effective way to host static websites directly from an S3 bucket. It's easy to set up and can be used for a variety of use cases, such as personal websites, blogs, and small business websites. S3 simply serves the static website files directly from the bucket, using the bucket like a webserver by indicating the default index.html and error.html that the user provided as the entry point for the url that aws provides.

Q: s3 virtual hosted style url vs a path style url
A: In AWS S3, there are two types of URLs that can be used to access S3 objects: virtual hosted style URLs and path style URLs. Virtual hosted style URLs are URLs that use the BUCKET NAME as part of the domain name in the URL. For example, a virtual hosted style URL for an S3 object might look like this: http://mybucket.s3.amazonaws.com/myobject - Path style URLs, on the other hand, are URLs that use the bucket name as part of the PATH in the URL. For example, a path style URL for the same S3 object might look like this: http://s3.amazonaws.com/mybucket/myobject - Virtual hosted style URLs are generally preferred over path style URLs, as they provide better performance and scalability. Virtual hosted style URLs allow S3 to distribute requests across multiple servers, which can improve performance and reduce latency. Path style URLs, on the other hand, require S3 to route all requests through a single server, which can limit performance and scalability.

## ec2 (elastic compute cloud) & VPC
Q: What are the uses of ec2
EC2 instances can be launched in a variety of configurations, including different instance types, operating systems, and storage options. EC2 instances can also be configured to work with other AWS services, such as Amazon Elastic Block Store (EBS), Amazon Simple Storage Service (S3), and Amazon Relational Database Service (RDS).
A: Hosting websites and web applications: EC2 instances can be used to host websites and web applications, providing scalable and reliable compute resources to handle incoming traffic.
Running enterprise applications: EC2 instances can be used to run enterprise applications, such as databases, business intelligence tools, and customer relationship management (CRM) systems.
Big data processing: EC2 instances can be used to process large amounts of data, such as data analytics, machine learning, and scientific computing.
DevOps and testing: EC2 instances can be used for development, testing, and deployment of software applications, providing a flexible and scalable environment for software development teams.
Disaster recovery: EC2 instances can be used for disaster recovery, providing a backup environment for critical applications and data in case of a disaster or outage.
Gaming: EC2 instances can be used to host online games, providing scalable and 
EC2 instances can be launched in a variety of configurations, including different instance types, operating systems, and storage options. EC2 instances can also be configured to work with other AWS services, such as Amazon Elastic Block Store (EBS), Amazon Simple Storage Service (S3), and Amazon Relational Database Service (RDS).

Q: what's ami?
A: amazon-machine-image is required to launch an instance in AWS. it convenient way to launch instances with pre-configured software and settings, This allows you to launch instances with the same configuration as the original AMI, including the same hardware resources and network settings. You can choose from a variety of pre-configured AMIs provided by AWS or the AWS Marketplace, or create your own custom AMI to meet your specific needs.
instance type (server type)
instance type is a specification that defines the hardware resources, such as CPU, memory, and storage, that are available for an EC2 instance. Each instance type is optimized for specific use cases and workloads, and provides a different balance of compute, memory, and storage resources.
storage gib & root volume & ebs & gp3 iops
Storage in EC2 is measured in gibibytes (GiB), which is a binary unit of measurement that is equivalent to 1,073,741,824 bytes. The root volume is the primary storage device that is attached to an EC2 instance and is used to store the operating system and other system files. EBS (Elastic Block Store) volumes are used to store data and can be attached and detached from instances as needed. GP3 (general purpose ssd) are EBS volumes that provide a flexible and cost-effective way to provision storage with customizable IOPS (Input/Output Operations Per Second) and throughput.
EBS snapshots are point-in-time copies of EBS volumes that can be used to back up and restore data. The frequency and size of EBS snapshots can be customized based on your specific backup and recovery requirements.
Data transfer (inbound and outbound data transfer and intraregion data transfer)
Inbound and outbound data transfer in EC2 is measured in gigabytes (GB) and is charged based on the amount of data transferred. Intra-region data transfer, which is data transfer between EC2 instances in the same AWS region, is typically free or charged at a lower rate than inter-region data transfer.
key pair
a key pair is a set of public and private keys that are used to securely connect to an EC2 instance. When you launch an EC2 instance, you can specify a key pair that will be used to authenticate on every connections to the instance. You do so by generating a public and private key pair using a tool such as ssh-keygen command. the public key is stored inside the instance and is used to verify every connection to the instance, so don't lose the private key as you won't be able to connect to the instance without it. You can connect to DIFFERENT INSTANCES with the same key pair AS LONG AS they are in the same REGION. keeping the key private is super important as access to it means access to the instance.
user data (optinal meta-data script)
User data is an optional feature that used to automate the configuration of an instance when it first lunch (or when stopped and lunched again if the UserData parameter is added to it - which occurs by default if you change the user data script). the user data script used to perform a wide range of tasks, such as configuring network settings, installing packages, and running scripts. (Limits: User data is limited to 16 KB in size for Linux instances and 32 KB for Windows instances)
instance connect vs session manager vs ssh vs serial console
ec2 provides a different way to connect to your EC2 instances and manage them. 1. EC2 Instance Connect: EC2 Instance Connect is a browser-based SSH connection manager that allows you to securely connect to your EC2 instances using the AWS Management Console. EC2 Instance Connect uses AWS Identity and Access Management (IAM) to control access to your instances and provides a simple and secure way to connect to your instances without the need for a separate SSH client. 2. Session Manager: Session Manager is a fully managed AWS service that allows you to manage your EC2 instances using a browser-based shell or the AWS CLI (Command Line Interface). Session Manager provides a secure and auditable way to manage your instances without the need for a separate SSH client or VPN connection. 3. SSH: SSH (Secure Shell) is a widely used protocol for securely connecting to remote servers and managing them using a command-line interface. You can use an SSH client, such as PuTTY or OpenSSH, to connect to your EC2 instances using the public IP address or DNS name of the instance. 4. Serial Console: Serial Console is a feature that allows you to troubleshoot and recover your EC2 instances using a serial connection. Serial Console provides access to the boot process and console output of your instances, and can be used to diagnose and fix issues that prevent your instances from starting up.

Q: explain public ipv4 VS private ipv4 VS ipv4 dns 
A: 1. Public IPv4 address: A public IPv4 address is a globally unique IP address that is assigned to an EC2 instance and can be used to communicate with the instance over the internet. Public IPv4 addresses are assigned dynamically by AWS and can be released and reassigned as needed. 
2. Private IPv4 address: A private IPv4 address is an IP address that is assigned to an EC2 instance within a VPC (Virtual Private Cloud) and is used for communication within the VPC. Private IPv4 addresses are not accessible from the internet and are used to isolate and secure your resources. 
3. IPv4 DNS hostname: A IPv4 DNS hostname used to resolve the public IPv4 address of the instance. Public IPv4 DNS hostnames are assigned dynamically by AWS and can be released and reassigned as needed. the public DNS is connected to the global DNS through amazon's Route 53 service. Route 53 is a clound Domain Name System web service that gives devleopers and busisneses an easy way to route end users to their aws internet applcaiton. when you lunch an ec2 instance amazon autoamtically reates a DNS recrod in Route 53 that maps the public dns hostname to the public ipv4 address of the instnace. this dns record is propagated to dns servers around the world, allowing users to access the isntance using hte public dns hostname. when a user enters the public dns hostane into their web browser the brwoser sends a dns query to a dns server to resolve the hostname to an ip address. the dns server looks up the dns record in route 53 and returns the publci ipv4 address of the instance to the brwoser. the browser then estalbies a conention to the instance using the ipv4 address. so Route 53 service maps the hostname to the public ipv4 address of the instance. NOT all ec2 instances have a public ip, it depends if you decided to add it to the instance or not. if you don't assign pbulic ipv4 the instace will only be accessible within the virtua private cloud (vpc) in which the instance was lunched. if you want to access the internet from it you'll have to use a nat gateway or a bastion host to forward traffic to the instance. assigning ipv4 to an instance may cost money. you can create a public ipv4 to an instance even if it already exists as long as there are avilable ipv4 in the hosts part of the instance's subnet that aren't being used by other instance. if all host ips are used by instances in your subnet you can modify the CIDR of your subnet in the subnets navigation panel in action tab. e.g. changing 10.0.0.0/24 to 10.0.0.0/23 which will expand from 256 ip to 512 ips. however modiying the cidr block will rEQUIRe to update the ip addresses of any instances running in the subnet to reflect the new ip address range by stopping the instance first, then modify the network interface of the isntance to use a new ip address range & go to ec2 console selecet the instance you want to update in actions tab choose networking and then manage network interaces and select the network interace that you want to modify and press actions modify network interface.

Q: explain nacl (network access control list)
A: netowrk acl is a firewall at the subnet level, aws creates a default acl for every subnet that is created which allows BY DEFAULT all inbound and all outbound traffic but you can create a custom nacl and attach/assoicate it to your subnet instea dof the default one. you can attach multiple subnets to a NACL, but only 1 nacl can be attached to each subnet. nacl are stateless and required specific rules for inbound and outbound traffic. * NACL are sorted by order where the lowest number of a rule <rule number> has the highest priority and if a rule is passed by the priority order the traffic will pass WITHOUT checking the other rules (only in nacl it's like this)

Q: Explain security groups rules
A: security groups are a firewall resides on your VPC on an INSTANCE level (ec2, rds etc). by default the security group that attached to each instance denys all inbound and ALLOWS all outbound traffic. security groups are statefull and allows responses to inbound traffic automatically without the need to configure outbound traffic and same for vice versa. unlike NACL, in security groups all the rules are evulated indivudally before deciding whether to allow traffic in / out or not, traffic can be restricted by ip type (ssh,), protocol (tcp, http), port range (80, 443), traffic soucce (cidr-classless inter domain routes) example of using security groups: webserver instance allows inbound traffic from internet 0.0.0.0/0 for https port 443. the application instance allows http port 80 from the webserver instance only. the database instance allows inbound traffic on tcp port 3306 from application instance ip only. and remmeber secuirty groups are stateful so no need to configure outbound rules as it's automatically sent back. this creates very safety network as even if someone hacks the webserver and wants to steal data they still can't access the database directly. 
* security groups are NOT ACTIVE ubless they are assigned to an instance / resource (ec2 etc)
* the security groups you assoicate with your instances determines which traffic can access those instances / resources e.g. load balancers / your webserver etc. by using security group as the source type you don't need to specify speific addresses , so for example for the load balancer outbound you put the security group of the webservers and for inbound rule of the webservers you put the security group of the load balancers for "dobule" security.

Q: what's a vpc?
A: a virtual private cloud provide a flexible and scalable way to isolate and secure your AWS resources. A VPC provides a private network that is isolated from the public internet. This allows you to securely connect your AWS resources without exposing them to the internet. and control access to your resources using security groups and network ACLs.
subnet
Within a VPC, you can create subnets that are used to segment your network resources. Each subnet is associated with a specific availability zone and provides a range of IP addresses that can be used by your resources. Each subnet can have its own security groups and network ACLs (Access Control Lists), which are used to control access to the resources in the subnet.
route table
Each subnet has its own routing table, which is used to route traffic between the resources in the subnet and between other resources in the VPC such as ec2 (virtual server instances), rds instances (relatioal database service), elastic load balancers (Load Balancers are managed load balancing services that can be launched in a VPC and are used to distribute traffic across multiple EC2 instances), nat gateway (Network Address Translation gateways are used to enable internet communication for resources in private subnets).
internet gateway - igw
an internet gateway (IGW) is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. An internet gateway provides a target in your VPC route tables for internet-routable traffic, and performs network address translation (NAT) for instances that have been assigned public IP addresses (public subnet).

Q: explain nat gateway - nat (network address translation)
A: nat gateway translate the ip address of a private subnet into the nat gateway ip address in order to commuincate with the INTERNET from the PRIVATE subnet. when a request is sent from a private subnet or the internet that looks to reach the private subnet the nat gateway is the ONLY gateway the translate the request to / from the private ip address of the subnet. To setup a nat gateway in the public subnet, you must also specificy an elastic ip while creating the NAT gateway in a public subnet. after creating the NAT gateway you must add to the route table of the PRIVATE subnet the 0.0.0.0 IP destination with the target as nat-gwy-id** (ipv4 only) for ipv6 use egress-only-igw which allows connection from private subnets to the internet in your vpc which also blocks direct communication between the internet to the private subnet and add to the private subnet route table the ::/0 - eigw-id** , egress only is stateful so it remmbers who it sent the content to and allows automatically to get back a response from the destination if inbound premission isn't allowed to the private subnet. To allows access to the internet from / to the private subnet you MUST also configure a route table inside the private subnet to allow specific types of traffic and ips to & from the subnet. 

Q: explain vpc peering
A: vpc peering connects different vpcs to each other either on the same aws account or accross different aws accounts. peering provides sharing data transfer between different vpc's. 

Q: how to create vpc peering?: 
A: 1. you have to add to the route table of the requester and receiver vpc their corresponding cidr block.
2. go to insatnces menu column -> security tab -> click on security groups option. inside inbound rules tab click edit inbound rules -> add in the type custom icmp-ipv4 and in the source the CIDR of the peered vpc subnet. if you need to add different traffic types you need to change the security group accordingly.
* peered VPCs do not necessairly accept all data between them by default. Security features, such as network access control lists and security groups, still apply. Be sure to update them accordingly as well.
* remmeber security groups are stateful which means the response for the request will be allowed to flow from the outbound reciever and into the inbound sender REGARDLESS if there are security groups rules that allows it!
* only a direct connection between peers exists (if both VPC A & C connects to VPC B via peering, A and C CANNOT communicate with each other - this is also called tranitive or edge to edge routing) 

Q: explain the difference betweem root user & IAM user
A: the root user is the initial user account that is created when you first create an AWS account. The root user has full access to all AWS services and resources in the account, and can perform any action on those resources. As such, it is recommended that you do not use the root user for day-to-day activities, but instead create and use IAM (Identity and Access Management) users. IAM users are separate user accounts that you can create and manage within your AWS ROOT account. IAM users have specific permissions that you can control and manage, allowing you to grant or restrict access to AWS services and resources as needed. IAM users can be assigned to groups, which can simplify the process of managing permissions for multiple users. this provides improved security (limit scope to your resources), accountability (track and audit actions taken by individual users), management (can control access of all users to every resource from one account)

Q: are all subnets in a vpc must share the same route table , security groups and acl?
A: In Amazon Web Services (AWS), all subnets within a Virtual Private Cloud (VPC) share the same route table, but they can have different security groups and network access control lists (ACLs).
The route table is used to determine how traffic is routed between subnets within the VPC and to the internet. By default, all subnets within a VPC are associated with the same route table. However, you can create additional route tables and associate them with specific subnets if you need to route traffic differently. On the other hand, security groups and network ACLs are used to control inbound and outbound traffic to and from resources within the VPC. Each subnet can have its own set of security groups and network ACLs, which allows you to apply different security policies to different subnets and resources.
It is important to note that when you create a security group or network ACL, you can specify the VPC ID and the subnet ID that it should be associated with. This means that you can apply the same security group or network ACL to multiple subnets within the same VPC if you want to enforce consistent security policies.
In summary, all subnets within a VPC share the same route table, but they can have different security groups and network ACLs. This allows you to create a more flexible and secure network architecture for your resources in AWS.


Q: If i create an igw and added the route table to it from the public instance do i need to open security premsision or it's already acccessible to the internet?
A: If you have created an internet gateway (IGW) and added the route table to it from a public instance in your AWS VPC (Virtual Private Cloud), you may still need to configure security group rules to allow inbound traffic from the internet to your instance. 
Security groups: Security groups act as a virtual firewall that controls inbound and outbound traffic to your instances. By default, security groups deny all inbound traffic and allow all outbound traffic. 
Inbound rules: To allow inbound traffic from the internet to your instance, you must create inbound rules in your security group that allow traffic on specific ports and protocols. 
Outbound rules: To allow outbound traffic from your instance to the internet, you must create outbound rules in your security group that allow traffic on specific ports and protocols. 
Overall, while an internet gateway provides internet connectivity to instances in your VPC, you still need to configure security group rules to control access to your instances and other resources. By carefully designing your security groups and using inbound and outbound rules to control traffic, you can ensure that your resources are secure and accessible only to authorized users and applications.

Q: if an instance doesn't have public ipv4 does it mean it is created inside a private subnet?
A: Not necssairly, if an EC2 instance in AWS does not have a public IPv4 address, it's possible that it was launched in a private subnet within a VPC (Virtual Private Cloud) OR the public ip hasn't been assigned yet, to assign a public ip you need to Allocate an Elastic IP address: In the AWS Management Console, navigate to the Elastic IPs page and click "Allocate new address". This will allocate a new Elastic IP address that you can use to assign to your instance. Associate the Elastic IP address with the instance: In the Elastic IPs page, select the Elastic IP address that you want to associate with your instance and click "Actions" > "Associate IP address". In the Associate Elastic IP address dialog box, select the instance that you want to associate the Elastic IP address with and click "Associate". Update the instance's security group rules: To allow inbound traffic to the instance, you must update the security group rules for the instance to allow traffic on specific ports and protocols. Note that you will also need to configure the routing tables for your VPC and subnets to allow traffic to and from the internet.

Q: how do i know if the subnet is private or public?
A: You can determine whether a subnet is public or private by checking its route table configuration.
Navigate to the VPC console: In the AWS Management Console, navigate to the VPC console. 
Select the subnet: Select the subnet that you want to check. 
Check the route table: In the "Details" tab for the subnet, check the "Route table" field. This will show you the route table that is associated with the subnet. 
Check the route table configuration: Navigate to the "Route tables" section of the VPC console and select the route table that is associated with the subnet. Check the route table configuration to see if it has a route to the internet. If the route table has a route to the internet, the subnet is a public subnet. If the route table does not have a route to the internet, the subnet is a private subnet. 
* In AWS VPC (Virtual Private Cloud), there is NO BUTTON OPTION to make a subnet either public or private. Whether a subnet is public or private is determined by its route table configuration, which is a logical configuration that you must set up manually.

Q: Does an ec2 resides within a subnet?
A: Yes, an ec2 resides within a subnet, subnet is a range of ip addresses in your vpc.

Q: are security groups on the vpc level and on ec2 / instance level are the same ?
A: Yes, in aws, Security Groups are only applied at the instance level and are the same security groups showing at the vpc menu column.

Q: what's the difference between network acl and security groups? 
A: Network ACLs and Security Groups are both used to control inbound and outbound traffic to and from resources within a VPC in AWS. However, Network ACLs are stateless and applied at the subnet level, while Security Groups are stateful and applied at the instance level. Network ACLs are evaluated BEFORE Security Groups which means if there's a traffic that is blocked by NACL it won't reach the security group and you must explicitly allow both inbound and outbound traffic for a specific protocol and port with Network ACLs.

Q: explain compute cpu, memory, storage in aws
A: CPU: This refers to the processing power of the instance. Each instance type has a different number of virtual CPUs (vCPUs) that are allocated to the instance. The number of vCPUs ranges from 1 to 128, depending on the instance type.
Memory: This refers to the amount of RAM that is allocated to the instance. Each instance type has a different amount of memory that is allocated to the instance. The amount of memory ranges from 0.5 GB to 24 TB, depending on the instance type.
Storage: This refers to the amount of disk space that is allocated to the instance. Each instance type has a different amount of storage that is allocated to the instance. The amount of storage ranges from 8 GB to 24 TB, depending on the instance type. In addition, AWS offers several types of storage, including Amazon Elastic Block Store (EBS), Amazon Elastic File System (EFS), and Amazon Simple Storage Service (S3).

## RDS & DynamoDB (NOSql)
* failover means when rds fail (hardware issue) and there's multi az enagbled for that rds If the primary instance fails, the standby replica is automatically promoted to become the new primary instance. This process is automatic and typically takes less than a minute to complete. Once the new primary instance is promoted, the DNS record for the RDS endpoint is updated to point to the new instance. 
* host replacement used to replace the host of an RDS instance in AWS, you can create a new instance, create a read replica, promote the read replica to become the new primary instance, test the new instance, and delete the original instance. You should consider using host replacement for an RDS instance in AWS when there is a hardware failure, performance issues, or when you need to upgrade the database engine or operating system. Host replacement can take several hours, so you should plan accordingly and communicate any downtime or service disruptions to your users or customers.

DynamoDB is one of the nosql servers avilable in aws. when creating a db in dynamo db you must specify the partiton key and optional a second required key called a sort key. the partition key ensures that each item-attribute has a unique value (e.g. userId). if you use both of the primary keys (partition and sort key) you can have same value for multiple partition keys as long as the value for each sort key is different, this is called composite key. to query in a dynamodb table you have to use the instance id value and optional the sort key value to further refine your query results.

Q: sql vs nosql
A: SQL databases, also known as relational databases, are based on the Structured Query Language (SQL) and use a table-based data model. SQL databases are ideal for applications that require complex queries and transactions, such as financial applications or e-commerce websites. SQL databases are also highly scalable and can handle large amounts of data.
NoSQL databases, on the other hand, are non-relational databases that use a variety of data models, such as key-value, document, or graph. NoSQL databases are ideal for applications that require high scalability and performance, such as real-time analytics or social media platforms. NoSQL databases are also highly flexible and can handle unstructured or semi-structured data.
It is also possible to use a combination of SQL and NoSQL databases in the same application to takeadvantage of the strengths of each.

Q: Explain schema & schemaless in sql and nosql
A: a schema is a logical container for database objects, such as tables, views, indexes, and procedures. A schema defines the structure of the database and the relationships between the objects.
On the other hand schemaless like in nosql dynamodb you can create any table with as many attributes as you like for each item in the table. you can also add new fields anytime even after the table or item has been created. this is called a flexible schema / schemaless as you can always change your app items db' WITHOUT redfine the table schema as would be required in relational databases.

Q: what operation gets a specific item from the DynamoDB table and what are the required fiels? 
A: GetItem operation get a specific item field from the DynamoDB table and you must specify the primary keys-values for the client/item that you want to retrieve. you can retrieve all the fields or apple a condition to retrivte just a subset of its atributes.

Q: what MANAGED mean in aws managed nosql db?
A: a managed NoSQL database refers to a database service that is fully managed by AWS. This means that AWS takes care of the underlying infrastructure, such as servers, storage, and networking.

Q: map vs list in dynamodb attributes
A: Maps are useful for storing structured data that can be accessed by a UNIQUE key in the map (key: value, key2: value), while lists are useful for storing unstructured data that can be accessed by position (list[0],list[1] etc).

## EFS (elastic file system)
Q: what's the purpose of efs?
A: efs used to provides a serverless (no infrastrcutre setup / maintainance) elastic (scale up/down automatically according to your files size) file system that you can use to share files data without provisioning or managing storage.

Q: How to configure efs and connect it to ec2 instances?
A: 
1. first you need to create a security group rule that allows NFS INBOUND TRAFFIC to the current security group that is attached to your instances that you want to allow efs there, this is required so instances can connect to the efs. to do so, go to the the securtiy group tab inside ec2 or vpc console then go to inbound rules tab and choose choose: "nfs" as the type, in the source choose the security group that your ec2 instaces are ALREADY attached to, this will give the instance an acccess to the shared file system you'll create and mount in the next steps.
2. go to efs console and create an efs and choose the customize option, choose the correct vpc your instances are in, the subnet id and the security group (that you have just created with the inbound rule) for each az you have create a sepereate mount target. (each mount target installs an elastic network interface (eni) into the chosen subnet). an eni is a glogical networking component in a vac that repenests a virtual network card. the eni atuaiotmcailly receives an ip address from the vpc.
3. go inside the efs you've just created and click the attach button. in the mount via dns tab copy the mount helper code. (you need to install later in session manager the package amazon-efs-utils to use this code) which shortcut the mount configuration and installation on each instance.
4. go to ec2 console choose the instance , click connect icon on top and choose the session manager tab. apply admin privilages by typing: sudo -i , install the amazon helper package (if you don't install it the bash terminal won't know what is the efs mount file type that you'll run after installing the package) by typing: sudo yum install -y amazon-efs-utils , then create folder: mkdir data, mount the fs there by typing: sudo mount -t efs -o tls fs-XXXXXXX:/ DIR-NAME, go inside the directory you've mounted the fs into by typing: cd DIR-NAME, to create a continuos appending to a file (using -c flag) type: bash -c "cat >> efs-1-setup.log", then to actually append the data type the data you want e.g.: efs-1 mounted in site **, to view the content of the file type: cat efs-1-setup.log
5. go to another ec2 instance you want to add efs to, and repeat step 4 (and 3 if you've not mounted a file target in the efs) so you can access the fs that you've mounted in another az.

Q: explain amazon-efs-utils
A: the Amazon EFS utils package is a set of command-line tools and scripts that are designed to simplify the management of EFS file systems. The package includes several tools, including efs-utils, nfs-utils, amazon-efs-mount-watchdog, and amazon-efs-mount-helper. The package is available for several Linux distributions and can be installed using the package manager for the respective Linux distribution. 1. efs-utils: This tool provides a set of commands for managing EFS file systems, including creating and deleting file systems, mounting and unmounting file systems, and configuring file system properties. 2. nfs-utils: This tool provides a set of commands for managing NFS (Network File System) shares, which are used to mount EFS file systems to EC2 instances. 3. amazon-efs-mount-watchdog: This tool monitors the health of the EFS mount points and automatically remounts the file system if it becomes unresponsive. 4. amazon-efs-mount-helper: This tool is a mount helper that simplifies the process of mounting EFS file systems to EC2 instances. The mount helper is designed to work with the mount command and automatically configures the mount options for the EFS file system.

Q: what is a file systems?
A: a file system is a method used to organize and store data on a storage device. A file system provides a way to organize data into files and directories, and allows the operating system to access and manage the data stored on the storage device. A file system typically includes several components, including:
File names: A file system uses file names to identify and organize files. File names can include letters, numbers, and special characters, and can be organized into directories.
Directories: A directory is a container for files and other directories. Directories can be nested within other directories to create a hierarchical structure.
File attributes: A file system can store additional information about files, such as the file size, creation date, and permissions.
Allocation methods: A file system uses allocation methods to determine how data is stored on the storage device. Common allocation methods include block allocation and extent-based allocation.

Q: what is mount and what mount targets do in efs?
A: Mounting file systems is an important part of managing data in an operating system, For example, when you insert a USB drive into your computer, the operating system will mount the file system on the USB drive and make it available for access through a directory in the file system hierarchy, such as /media/usb. Mounting allows you to access and manage data stored on different types of file systems. By mounting file systems to directories in the file system hierarchy, you can access and manage data stored on network file systems, local file systems, and removable media.
mount targets in Amazon EFS provide access to the file system from EC2 instances by creating a network interface that can be used to mount the file system. Mount targets are associated with a specific subnet in a VPC and can be accessed by EC2 instances that are in the same subnet. When an EC2 instance mounts an EFS file system, it creates a connection to the mount target using the mount target's IP address. This connection allows the EC2 instance to access the file system as if it were a local file system, Mount targets are important for providing access to EFS file systems from EC2 instances, as they allow the file system to be mounted and accessed over the network. Without mount targets, it would not be possible to access an EFS file system from an EC2 instance. EFS supports multiple mount targets for each file system, which allows for high availability and scalability. By creating multiple mount targets in different subnets, you can ensure that the file system is accessible even if one of the subnets or mount targets becomes unavailable.
* you can create mount target for a file system by using either the aws management console (aws website) , aws cli, or by programmatically using the aws sdks

Q: explain mount targets
A: EFS uses mount targets to provide access to the file system from EC2 instances. A mount target is a network interface that is used to mount an EFS file system to an EC2 instance. Each mount target is associated with a specific subnet in a VPC, and can be accessed by EC2 instances that are in the same subnet. When an EC2 instance mounts an EFS file system, it creates a connection to the mount target using the mount target's IP address. This connection allows the EC2 instance to access the file system as if it were a local file system. Mount targets are important for providing access to EFS file systems from EC2 instances, as they allow the file system to be mounted and accessed over the network. Without mount targets, it would not be possible to access an EFS file system from an EC2 instance. It is important to note that EFS supports multiple mount targets for each file system, which allows for high availability and scalability. By creating multiple mount targets in different subnets, you can ensure that the file system is accessible even if one of the subnets or mount targets becomes unavailable.

Q: what efs used for?
A: EFS is used for a variety of use cases, such as: 
Content management: EFS can be used to store and manage content, such as images, videos, and documents, for use in web applications or other types of content management systems.
Big data analytics: EFS can be used to store and process large amounts of data for use in big data analytics applications, such as Hadoop or Spark.
Application development: EFS can be used to store and share code and other development assets across multiple EC2 instances, making it easier to develop and deploy applications.
Media processing: EFS can be used to store and process media files, such as audio and video, for use in media processing applications, such as transcoding or streaming.
Backup and disaster recovery: EFS can be used as a backup and disaster recovery solution, providing a scalable and highly available storage solution for critical data.

Q: explain ENI & how to create one
A: eni is a logical netowrking component in a vpc that represents a virtual network card. the eni atuomatically receives an ip address from the vpc. after creating an efi, you can mount the efs on instances in that subnet.
To create an elastic network interface you write efs in search bar then choose the network tab of your desired efs. choose the subnet and a security group (usually all eni will use to the same secuity group) that the eni will be attached to. eni will be installed automatically in that subnet specified above.

Q: how to mount efs to an ec2 instance?
A: connect to the instance via ssh or session manager write:
sudo -i 
sudo yum install -y amazon-efs-utils
now you create a data directory, mount your Amazon EFS file system to the data directory, add entries to the existing log file, and view them by:
cd ~/
mkdir data
ls 
paste the sudo mount command that you copied from the Amazon EFS console in an earlier step. At the end of the command, replace the "efs" folder name with "data" (without quotes) and press Enter
cd data
sudo bash -c "cat >> efs-1-setup.log"
this is an ec2 in az B
cat efs-1-setup.log
You have successfully mounted an Amazon EFS file system to two Amazon EC2 instance
* can use amazon ec2 user data (optional meta data setting) to attach files systems to new instances everytime they lunch by pasting this code inside the user data 


Q: explain ecs and lambada
A: Amazon ECS is a fully managed container orchestration service that allows you to run and manage Docker containers on a cluster of EC2 instances. ECS provides a scalable and highly available platform for deploying and managing containerized applications. With ECS, you can easily deploy and manage containerized applications, and scale them up or down as needed to meet changing demands.
AWS Lambda, on the other hand, is a serverless computing service that allows you to run code without provisioning or managing servers. With Lambda, you can write code in a variety of programming languages, and the service will automatically run and scale the code in response to events, such as changes to data in an S3 bucket or a new message in an Amazon Simple Notification Service (SNS) topic.

Q: when and for what docker containers are useful for
A: Docker containers are useful for a variety of use cases, including application deployment, microservices architecture, DevOps, hybrid cloud, and big data. Docker containers provide several benefits, including portability, scalability, consistency, and efficiency. Portability: Docker containers can be easily moved between environments, making it easy to deploy applications across different infrastructure and cloud providers.
Scalability: Docker containers can be easily scaled up or down to meet changing demands, making it easy to handle spikes in traffic or demand.
Consistency: Docker containers provide a consistent and reproducible environment for building, testing, and deploying applications, which can help to reduce errors and improve reliability.
Efficiency: Docker containers are lightweight and use fewer resources than traditional virtual machines, which can help to reduce costs and improve performance.

Q: what is the purpose of mounting efs to ec2 / lambada / ecs
A: Shared storage: Mounting EFS to EC2, Lambda, or ECS allows multiple instances or functions to access the same file system, providing a shared storage solution for applications.
Scalability: EFS is designed to be highly scalable, allowing you to easily scale up or down as needed to meet changing demands. By mounting EFS to EC2, Lambda, or ECS, you can ensure that your application has access to scalable and highly available storage.

Q: do i need the same underlying os when running a docker image across multiple env ?
A: No, you do not need the same underlying operating system to run a Docker image across multiple environments. Docker containers are designed to be portable and can run on any system that supports Docker. Docker containers are isolated from the underlying operating system and include all of the dependencies and libraries required to run the application. This means that you can create a Docker image on one system and run it on another system with a different operating system, as long as both systems support Docker.
* However there may be differences in the way that the application interacts with the file system or network on different operating systems. Therefore always ensure that your Docker image runs correctly across multiple environments by testing the image on each environment to ensure that it behaves as expected. You may also need to make adjustments to the Docker image or application to account for any differences in the underlying operating system.

## Load Balancing & Auto Scaling Groups
Q: what are the purpose and capabilities of auto scaling and load balancing
A: Auto Scaling:
Purpose:
Auto Scaling is designed to automatically adjust the number of EC2 instances in your application in response to traffic patterns. This means that you can ensure that you have the right number of EC2 instances available to handle the load for your application.
Capabilities:
Dynamic Scaling: Auto Scaling can increase the number of EC2 instances during demand spikes to maintain performance, and decrease capacity during lulls to reduce costs.
Predictive Scaling: Auto Scaling uses machine learning algorithms to predict future traffic patterns and proactively scale your applications in anticipation of changes in traffic.
Health Checks: Auto Scaling continuously monitors the health of your instances. If an instance becomes unhealthy, Auto Scaling can replace it with a new one.
Balanced Across Availability Zones: Auto Scaling can ensure that your instances are evenly distributed across multiple Availability Zones in a region for high availability.
Load Balancing:
Purpose:
Load Balancing is used to distribute incoming application or network traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in multiple Availability Zones.
Capabilities:
Distribute Traffic: Load Balancing efficiently distributes incoming application traffic across multiple targets.
Fault Tolerance: If a target becomes unavailable, Load Balancing automatically reroutes traffic to other healthy targets.
Health Checks: Load Balancing continuously checks the health of your targets and only sends traffic to the healthy ones.
SSL/TLS Termination: Load Balancers can handle SSL/TLS termination, offloading the work from your servers and freeing up resources on your backend.
Sticky Sessions: Load Balancers can bind a user's session to a specific target, enabling the user to connect to the same target for the duration of their session.
Together, Auto Scaling and Load Balancing can help you build highly available, fault-tolerant applications that can scale up or down based on demand, and distribute traffic efficiently across multiple targets.

Q: What's auto scaling group
A: 

Q: how come that i send a load balancer traffic in ec2 to a public subnet but in the auto scaling group i configure to create only private subnet instances and it still connects just fine to the instances via the web?
A: In AWS, when you configure a load balancer to send traffic to instances in a public subnet, it is still possible to have the instances themselves located in private subnets. This is achieved through the use of Network Address Translation (NAT) gateways or NAT instances.
Here's how it works:
Load Balancer in a Public Subnet: The load balancer is placed in a public subnet, which has a route table associated with it that has an internet gateway attached. This allows the load balancer to have a public IP address and be accessible from the internet.
Instances in Private Subnets: The instances that the load balancer routes traffic to can be located in private subnets. Private subnets do not have a direct internet gateway attached, so they are not directly accessible from the internet.
Network Address Translation (NAT): To allow the instances in the private subnets to communicate with the internet, you can use a NAT gateway or a NAT instance. The NAT gateway/instance acts as an intermediary between the private instances and the internet. It translates the private IP addresses of the instances to a public IP address, allowing them to communicate with the internet.
Routing: The route tables associated with the private subnets are configured to route outbound traffic to the NAT gateway/instance. This ensures that the instances can send traffic to the internet through the NAT gateway/instance.
When the load balancer receives traffic from the internet, it routes the traffic to the instances in the private subnets. The instances respond to the traffic, and the response is sent back to the load balancer through the NAT gateway/instance. The load balancer then forwards the response back to the client.
This setup allows you to have a secure architecture where your instances are located in private subnets, while still being able to receive traffic from the internet through the load balancer.
It's important to note that the instances in the private subnets do not have direct public IP addresses. They communicate with the internet through the NAT gateway/instance, which handles the translation of IP addresses.

* if you termiante an instance within an auto scaling group, which resutls in loweering the number of running instances below the auto scaling minimum requierment, a new isntance is launched autoamtically.
* to take advtange of the safety and reliability of geographic redundancy, span your auto scaling group accross multiple AZ and attach a load balacner to distribute incoming traffic across those az.
* by creating security group that allow inbound traffic from the internet to the load balancer and outbound to the security group of the webservers (and configure inbound traffic in the webservers to only allow load balancer traffic) you can run the instances in a private subnets inside the auto scaling group and they will still be accessible via the load balancer to the internet.


## IAM (Identity and access management)
Q: What's object reference
A: an object reference refers to a way of identifying and granting permissions to AWS resources or actions. IAM uses Amazon Resource Names (ARNs) as object references to uniquely identify resources within AWS.
An ARN is a string that follows a specific format and includes information about the AWS account, the resource type, and the resource name. It provides a standardized way to reference and manage resources across AWS services.
For example, an ARN for an IAM user might look like this:
arn:aws:iam::123456789012:user/my-iam-user
In this ARN, "123456789012" represents the AWS account ID, and "my-iam-user" is the name of the IAM user.
Object references are used in IAM policies to specify the resources or actions to which the policy applies. IAM policies define permissions and access control rules for users, groups, or roles within an AWS account. By referencing specific ARNs in IAM policies, you can grant or deny permissions to specific resources or actions.
For example, a policy statement might include an object reference to allow a specific IAM user to access an S3 bucket:
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-bucket/*",
  "Principal": {
    "AWS": "arn:aws:iam::123456789012:user/my-iam-user"
  }
}
In this policy statement, the "Resource" field specifies the ARN of the S3 bucket, and the "Principal" field specifies the ARN of the IAM user.
By using object references in IAM policies, you can control access to AWS resources and actions based on specific identities or resource ARNs, providing granular control over permissions within your AWS environment.

Q: explain serverless
A: serverless refers to a model where the cloud provider manages the infrastructure and automatically scales resources based on demand. In a serverless model, the cloud provider takes care of the underlying infrastructure, such as servers, operating systems, updates and network resources, and provides a platform for developers to build and deploy applications without worrying about the underlying infrastructure, where you can scale up or down your app resouces, pay per what you use only and focus on the code without managing the infrastrcture as well.

Q: What's cache and how is it useful in databases, servers and websites to improve performance?
A: cache refers to a high-speed data storage layer that is used to temporarily store frequently accessed data. Caching is a technique used to improve the performance of databases, servers, and websites by reducing the amount of time it takes to access data. caching can be used to store frequently accessed data in memory, which rdeuce the need to read from disk / memory. 

Q: what are resource tags used for
A: resource tags in AWS are a powerful tool for organizing, managing, and automating your AWS resources, and can help you optimize your AWS spending, improve your operational efficiency, and enforce your resource policies. Resource tags can be used for a variety of purposes, such as:
Cost allocation: You can use resource tags to track the cost of your AWS resources by department, project, or team. This can help you allocate costs more accurately and optimize your AWS spending.
Resource management: You can use resource tags to organize your AWS resources based on their attributes, such as their environment, application, or owner. This can help you manage your resources more efficiently and improve your operational visibility.
Automation: You can use resource tags to automate tasks, such as backups, snapshots, or resource termination. For example, you can use AWS Lambda functions to automatically tag resources based on their attributes, or to trigger actions based on specific tags.

Q: explain amazon route 53 , when is it being and where
A: Route 53 can be used to perform the following functions:
Domain registration: You can use Route 53 to register domain names, such as example.com, and manage the DNS settings for your domain.
DNS management: You can use Route 53 to manage the DNS settings for your domain, such as creating DNS records, configuring DNS routing policies, and setting up health checks.
Traffic management: You can use Route 53 to route traffic to different endpoints based on various criteria, such as geographic location, latency, or health status.
DNS query logging: You can use Route 53 to log DNS queries for your domain, which can help you troubleshoot DNS issues and analyze traffic patterns.
Route 53 is available in all AWS regions and can be accessed through the AWS Management Console, AWS CLI, or AWS SDKs. It is designed to be highly available and scalable, with a global network of DNS servers that can handle millions of queries per second.
In summary, Amazon Route 53 is a cloud-based DNS web service provided by AWS that can be used to manage domain registration, DNS management, traffic management, and DNS query logging. It is available in all AWS regions and can be accessed through the AWS Management Console, AWS CLI, or AWS SDKs.

Q: what are the Storage options avialble to use with ec2
A: efs (elastic file storage that i've trained with above), 
s3 (i've practice with above as well), 
ebs (elastic block store - not sure if i practice but possible during ec2 class), Instance store: Instance store is a temporary, high-performance storage option that is directly attached to the EC2 instance. 
Instance store volumes are ideal for temporary data that does not need to be persisted, such as cache or scratch data
Amazon Glacier: Amazon Glacier is a low-cost, highly durable, and secure cloud-based storage service provided by AWS. Glacier can be used to store and archive data that is infrequently accessed, such as backups or archives
AWS Storage Gateway: AWS Storage Gateway is a hybrid cloud storage service provided by AWS that enables on-premises applications to use cloud storage. Storage Gateway can be used to connect on-premises storage systems to AWS storage services, such as S3 or EBS.
Each storage option has its own unique features and use cases, and can be used to meet different storage requirements for EC2 instances.

Q: aws cli vs aws sdk
A: AWS CLI:
The AWS CLI is a unified tool that provides a consistent interface for interacting with all parts of AWS.
It's a command-line tool for managing AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.
It's primarily used for administrative tasks, such as managing resources in AWS, deploying applications, and automating manual tasks.
It's ideal for scripting, automation, and for those who prefer a command-line interface.
It's written in Python and can be used on Windows, macOS, and Linux.
To connect to AWS via the AWS CLI (Command Line Interface), you need to install the CLI and configure it with your AWS credentials. Here are the steps:
Step 1: Install AWS CLI
The AWS CLI is supported on Windows, macOS, and Linux. The installation depends on your operating system. Here's how to install it on each:
Windows: Download the installer from the AWS CLI website and run it.
macOS and Linux: You can install the AWS CLI using pip, which is a package manager for Python. Run the following command:
pip install awscli --upgrade --user
Step 2: Configure AWS CLI
After installing the AWS CLI, you need to configure it with your AWS credentials. You can do this by running the aws configure command:
aws configure
You'll be prompted to enter your Access Key ID, Secret Access Key, Default region name, and Default output format. Here's what each of these means:
AWS Access Key ID and AWS Secret Access Key: These are your AWS credentials, which you can get from the AWS Management Console. If you don't have these, you'll need to create a new IAM user with programmatic access, and AWS will generate a new set of keys for you.
Default region name: This is the name of the AWS region that you want to send your requests to by default. You can find a list of available regions in the AWS documentation.
Default output format: This specifies how the results are formatted. The options are json, yaml, text, and table. If you're not sure which one to choose, json is a good default.
After you've entered these details, your AWS CLI is set up and ready to use. You can start running commands to interact with AWS services. For example, to list all your S3 buckets, you can run:
aws s3 ls
AWS SDK:
AWS SDKs are language-specific APIs for AWS services. They are available in several programming languages such as Java, .NET, Node.js, Python (boto3), Go, Ruby, PHP, etc.
They are used to build applications with increased flexibility, reliability, and scalability.
They provide native features and take the complexity out of coding by providing AWS service-specific APIs.
They are ideal for developers building applications that use AWS services.
They handle low-level details such as authentication, retry logic, and error handling.
In summary, if you're a developer building an application that interacts with AWS services, you'd typically use the AWS SDK. If you're an administrator or DevOps engineer who needs to manage AWS resources, automate tasks, or quickly prototype something, you'd typically use the AWS CLI.
AWS SDKs are language-specific APIs for AWS services. They simplify the process of integrating your application, library, or script with AWS services like Amazon S3, Amazon EC2, Amazon DynamoDB, etc. AWS SDKs handle low-level details such as authentication, retry logic, and error handling.
To use an AWS SDK:
Choose the SDK that corresponds to the language you're using. AWS provides SDKs for several programming languages including Python (Boto3), JavaScript, Java, .NET, PHP, Go, Ruby, etc. aws.amazon.com, aws.amazon.com, aws.amazon.com.
Install the SDK. For example, to install Boto3 for Python, you can use pip:
pip install boto3
Configure your credentials. You can do this by setting your AWS access key ID and secret access key as environment variables:
export AWS_ACCESS_KEY_ID='your_access_key'
export AWS_SECRET_ACCESS_KEY='your_secret_key'
In your code, import the AWS SDK and use it to interact with AWS services. Here's a simple example using Boto3 to list all your S3 buckets:
import boto3
s3 = boto3.resource('s3')
for bucket in s3.buckets.all():
    print(bucket.name)