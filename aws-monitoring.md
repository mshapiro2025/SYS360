# AWS Monitoring

## Lecture Notes: Monitoring for AWS

### Monitoring EC2

* monitoring is an important part of maintaining the reliability, availability, and performance of your Amazon EC2 instances and AWS solutions
* you should collect monitoring data from all of the parts in your AWS solutions so that you can more easily debug a multi-point failure if one occurs
* also critical in detecting security events

### Monitoring Goals

* before you start monitoring EC2, you should create a monitoring plan that should include:&#x20;
  * what are your goals for monitoring?
  * what resources will you monitor?
  * how often will you monitor these resources?
  * what monitoring tools will you use?
  * who will perform the monitoring tasks?
  * who should be notified when something goes wrong?

### Establishing a Baseline

* measure EC2 performance at various times and under different load conditions
* store a history of monitoring data that you've collected
* compare current EC2 performance to historical data to help identify:
  * normal performance patterns
  * performance anomalies
  * optimization methods

#### Minimum Baseline

* EC2 logs the following metrics by default which can help set a minimum baseline:
  * CPU utilization
    * CPUUtilization
  * network utilization
    * NetworkIn
    * NetworkOut
  * disk performance
    * DiskReadOps
    * DiskWriteOps
  * disk reads/writes
    * DiskReadBytes
    * DiskWriteBytes
* additional metrics like memory utilization, disk space utilization, and page file/swaps require an agent on the instance

### Automated Monitoring

* systems status checks:
  * monitors the AWS systems required to support an instance
* instance status checks:
  * monitor the software and network configurations of individual instances
* CloudWatch events and alarms:
  * use the Amazon CloudWatch service to identify issues that can arise over time

### AWS System Status Checks

* monitor the AWS systems required to use your instance to ensure that they are working properly
* these checks detect problems with your instance that require AWS involvement to repair
* when a system status check fails, you can choose to wait for AWS to fix the issue or you can resolve it yourself (ex. by stopping and restarting or terminating and replacing an instance)
* examples of problems that cause system status checks to fail include:
  * loss of network connectivity
  * loss of system power
  * software issues on the physical host
  * hardware issues on the physical host that impact network reachability

### AWS Instance Status Checks

* monitor the software and network configuration of your individual instance
* these checks detect problems that require your involvement to repair
* examples of problems that may cause instance status checks to fail include:
  * misconfigured networking or startup config
  * exhausted memory
  * corrupted file system
  * incompatible kernel

### AWS CloudWatch

* collects and processes raw data from EC2 into readable, near real-time metrics
* separate AWS service with its own console
* basic monitoring: by default, EC2 sends metric data to CloudWatch in 5-minute periods (free)
* detailed monitoring; sends data/metrics for your instance to CloudWatch in 1-minute periods
  * can be enabled per instance
  * can cost $ if free-tier usage is exceeded
* alarms: can create alarms if certain conditions are observed
  * can notify through console or email
  * can also take an action such as reboot, shutdown, or terminate on instance
