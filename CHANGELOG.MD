
# Change Log
All notable changes to this project will be documented in this file.

## [2.2.0] - 2021-01-07

### Fixes
- #38: fixing deployment into Regions with < 3 AZs 

### Added
- #34: Optional deployment onto Aurora Serverless (Postgresql) for cost optimization especially with smaller deployments of a scalable solution
- #15: Optional deployment into a predefined/existing VPC containing at least Subnets in 2 AZs
- Parameter "BBBNumberOfAZs" to define how many AZs the deployment should utilize (=> also defines how many Subnets are used/created)

### Changed
- #44: Added section to prerequisites to ensure users are heads-up for common issues incl. missing service linked roles
- Big Blue Button Version String via parameter to make the version to be adjusted easily for upcoming Big Blue Button releases
- Application and Turn Server Ubuntu Versions are now parameterized. This ensures OS Versions can allign with the Big Blue Button Version used (e.g. for 2.3-dev deployments of BBB)
- Parameter BBBVPCcidr renamed into BBBVPCs
- BBBVPCs and BBB*Subnets parameters now take cidr blocks to create VPCs (and subnets) or IDs to reuse existing VPCs (and its subnets )
- Turn server Instance OS defaults to Ubuntu 20.04 LTS
- Removal of dedicated Contributing.md
- Restructure/Simplification of Conditions 
- Cleanup of unused conditions and parameters. 

## [2.1.0] - 2020-11-04

### Upgrade Notes: 
- Be sure to backup persistent storages if you use the single instance deplyoment mode before running the upgrade via setup.sh. The setup is backward compatible and will only adjust log group namings and streams. If you need or want to keep the already collected logs, export the data to S3 before running the upgrade process. 

### Changed
- #35: Log groups names are now more dynamic, allowing multble stacks in the same account as well as make it easier to locate related logs in Cloudwatch. Also the LogGroup strucure is simlified for better usability. 
- bump cfn-certificate-provider version to 0.2.5

### Fixes
- minor adjustments at the readme.md
- #42: Bump cfn-ses-provider version to 0.6.5

## [2.0.0] - 2020-11-03

### Upgrade Notes: 
- Be sure to backup especially your persistent storages like your recording storage before attempting the upgrade. the Changes in this Version will cause the EFS folder structure to be changed and simplyfied. 
If you decide to change the deployment type from EC2 based to AWS Fargate based architecure for Scalelite and Greenlight please make sure your ApplicationPrivateSubnet does have a reasonable size due each task will use it's very own IP address. 

To Upgrade, simply run the setup.sh with your parameters. Be sure to test and evaluate beforehand! 

### Added
- Optional AWS Fargate deployment instead of EC2 based deployment for Greenlight and scalelite #19
- containerized initialization for the EFS storage structure setup via Cloudformation, elimination of EC2 instance mount/mkdir hack #16
   
### Changed
- Default parameter settings for Desired ECS Instances have been lowered to 1. Max ECS Instance default settings have been lowered to 3. 
- Default Volume Size for Recordings EBS Storage have been lowered to 50G
- as the Instance Deployment for Turn and Application instances is pretty much settled, we shifted the cfn-signal command to the end of the bootstrap. this should ensure BBB is accessable pretty closely after the cloudformation deployment is done. 
- instance sizes for ECS Worker Instances and Application servers have been lowerd to the minimum needed to start a small test deployment to optize cost
- vCPU and memory limits of the ECS tasks have been simplified and are now set only on task level.

### Fixed
 
- Unreliable Turn and Application EC2 bootstraping due dkpg file locks
- Container Health Checks adjusted for more reliable service startups.
- #32
- #28

## [1.0.1] - 2020-11-04

### Changed
- bump cfn-certificate-provider version to 0.2.5

### Fixes
- #42: Bump cfn-ses-provider version to 0.6.5

## [1.0.0] - inital release

### inital version