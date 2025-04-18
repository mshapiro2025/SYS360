# AWS Network Security

## Lecture Notes: AWS Network Security

### Amazon VPC

* Amazon Virtual Private Cloud enables you to launch AWS resources into a virtual network that you've defined
* Amazon VPC is the networking layer for Amazon EC2
* the VPC closely resembles a traditional network, with the benefits of using the scalable infrastructure of AWS

### Key Components of VPC

* VPC- a virtual network dedicated to your AWS account
* subnet- a range of IP addresses in your VPC
* route table- a set of rules, called routes, that are used to determine where network traffic is directed
* internet gateway- a gateway that you attach to your VPC to enable communication between resources in your VPC and the internet (similar to NAT)

### Security Groups

* EC2 feature that are configured and connected to instances
  * operates as a layer 3/4 firewall for an instance
    * IP addresses and ports
  * associated with a VPC, but assigned to instances
* similar to a host-based firewall, but not configured in the OS
* security groups are stateful
  * if you send a request from your instance, the response traffic for that request is allowed regardless of inbound security group rules

### Network ACLs

* a network access control list is an optional layer of security for your VPC
  * acts as a firewall for controlling traffic in and out of one or more subnets
  * you might set up network ACLs with rules similar to your security groups in order to add an additional layer of security to your VPC
  * assigned to subnets, not instances
* VPC automatically comes with a modifiable default network ACL
  * by default, it allows all inbound and outbound IPv4 traffic
* can create a custom network ACL and associate it with a subnet
  * by default, each custom network ACL denies all inbound and outbound traffic until you add rules
* each subnet in a VPC must be associated with a network ACL
  * if the subnet is not explicitly associated with a network ACL, it is automatically associated with the default network ACL
* can associate a network ACL with multiple subnets
  * however, a subnet can only be associated with one network ACL at a time
  * when a subnet is associated with a network ACL, the previous association is removed
* a NACL contains a numbered list of rules
  * the rules are applied in order from lowest to highest
* a NACL has separate inbound and outbound rules, and each rule can either allow or deny traffic
* NACLs are stateless
  * this means that responses to allowed inbound traffic are subject to the rules for outbound traffic and vice versa
  * difficult when working with ephemeral ports

### Configuring NACL Rules

* rule number- rules are evaluated starting with the lowest numbered rule
  * as soon as a rule matches traffic, it's applied regardless of any higher-numbered rule that might contradict it
* type- the type of traffic (ex. SSH)
  * can also specify all traffic or a custom range
* protocol- you can specify any protocol that has a standard protocol number
  * can also specify ICMP with any or all of the ICMP types and codes
* port range- the listening port or port range for the traffic (ex. 80 for HTTP)
* source (inbound rules only)- the source of the traffic (CIDR range)
* destination (outbound rules only)- the destination for the traffic (CIDR range)
* allow/deny- whether to allow or deny the specified traffic

### AWS Network Firewall

* a stateful, managed, network firewall and intrusion detection and prevention service
* features:
  * stateful firewall
    * can incorporate context from traffic flows, like tracking connections and protocol identification
    * enforce policies such as preventing your VPCs from accessing domains using an unauthorized protocol
  * intrusion prevention system
    * provides active traffic flow inspection to identify and block vulnerability exploits using signature-based detection
  * web filtering
    * that can stop traffic to known bad URLs and monitor fully qualified domain names

### AWS DNS Firewall

* new service as of March 2021
* filter and regulate outbound DNS traffic for your VPC
  * integrated with AWS route 53 DNS service
* a primary use of DNS firewall protections is to help prevent DNS exfiltration
  * DNS exfiltration can happen when a threat actor compromises an application instance and then uses DNS lookup to send data out of the VPC to a domain that they control
  * DNS firewall can deny access to the domains known to be malicious
  * you can also deny access to all domains except for the ones you explicitly trust
