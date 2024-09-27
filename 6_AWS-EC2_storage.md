# AWS EC2 Instance Storage

## AWS EBS - Elastic Block Store

- ## Amazon EBS Volumes: (Availability zone locked)
  - Locked to the availability Zone, **to move** to another AZ you **need to create a EBS Snapshot**.
  - Storage volumes that you attach to Amazon EC2 instances while they run.
  - After you attach a volume to an instance, you can use it in the same way you would use a local hard drive attached to a computer, for example to store files or to install applications.
  - By default if you terminate your EC2 instance it will terminate also the EBS created with it.
  - **Network Drive**: it uses the network to communicate the instance, there might be a bit of latency.
    - Can be datached from an EC2 instance and attached to other quickly.
- ## Amazon EBS Snapshots
  - Point-in-time backups of Amazon EBS Volumes. Independent from the volume itself.
  - Used to copy EBS to another Availability Zone or Region.
  - You can use a **Snapshot** to restore a new EBS Volume in other AZ or Region (basically using a backup).
  - **EBS Snapshot Archive**:
    - Can move a snapshot to "archive tier" that is 75% cheaper.
    - Archived Snapshots take 24-72 hours to be restored.
  - **EBS Snapshot Recycle Bin**:
    - Setup rules to **retain for X period of time** the deleted snapshots before really hard deleting them.
    - It prevents you of any accidental deletion.
    - Specify retention (from | day to | year)

## AWS AMI - Amazon Machine Images

- A customization of an EC2 instance. (like a **template** of a machine pre-configured with software installed)
- You add your own software, configuration, operating system, monitoring...
- **Faster boot/configuration** time because all your software and configurations are pre-packaged.
- Is created for a specific region and can be copied across regions.
- You can launch an EC2 instance from:

  - **Public AMI**: Aws provided
  - **Your Own AMI**: You make and maintain them yourself
  - **AWS Marketplace AMI**: Someone else made (and potentially sells).

- ## How to create an AMI - Amazon Machine Image
  - Start an EC2 instance and customize it
  - Stop the instance (for data integrity)
  - Build an AMI - this will also create EBS snapshots.
    - click on: `your instance -> actions -> image and templates -> create image`
  - Launch instances from the AMIs. (**can be used across AZ and Regions**)

## AWS EC2 Image Builder -> Good to update your EC2 AMIs, updating the software on that.

- Can be run on a schedule (weekly, whenever packages are updated, etc..), and also manually.
- Used to automate the creation of Virtual Machines or container images.
- Automate the creation, maintain, validate and test EC2 AMIs.
  - Example "if NodeJS changes from LTS 20 to 21, update my AMI". This way you will have your AMIs updated.
- Free service, only pay for the underlying resources. If you create an EC2 instance during this process.

## AWS EC2 Instance Store

- EBS volumes are **network drives** (not physically attached) with good but "limited" performance. Because of the latency of network.
- If you need a high-performance hardware disk, use EC2 Instance Store. Better I/O performance.
- EC2 Instance Store lose their storage if they're stopped. Risk of data loss if hardware fails.
- Good for buffer / cache / temporary content. Not for long-term, for **long-term prefer EBS Volume**.
- Backups and Replications are your responsibility.

## AWS EFS - Elastic File System

- Managed NFS (Network file system), that can be mounted on 100s of EC2 instances.
- EFS works with Linux EC2 Instances in multi-AZ. Same EFS can be used in two EC2 instances across more than one AZ.
- Highly available, scalable, expensive (3x gp2), pay per use, no capacity planning.
- You can have on EFS in a security group and this EFS can be used for more than one instance in multiple Availability Zones.

- ## EFS-IA - Infrequent Access
  - Storage class that is cost optimized for files not accessed every time (92% lower cost) compared to EFS standard.
  - **Lifecycle policy**: You can **configure a period** to EFS **automatically move** your files to **EFS-IA** based on the last time they were accessed.
    - Example "move files that are not accessed for 60 days to EFS-IA".

## EBS vs EFS

- **EBS - Elastic Block Store**
  - One EBS can be used just for **one instance** in the same Availability Zone (AZ).
  - You can copy but it will not be "synchronized". Data is accessible from a single EC2 instance at a time.
  - **Block storage**: applications that require direct access to storage, such as databases.
- **EFS - Elastic File System**
  - One EFS can be used for **multiple instances** in multiple Availability Zones (AZ). Sharing the same data, same file system.
  - **File system**: Applications that require a shared storage storage solution used by multiple users or applications. If you need to work file folders and files.

## AWS FSx - File system

- Launch 3rd party high-performance file systems on AWS.
- Fully managed service.
- Examples:
  - `FSX for Windows File Server`:
    - Windows native shared file system, supports ntfs, integrated with Microsoft Active Directory.
    - Can be accessed by AWS or your on-premise infrastructure.
  - `FSx for Lustre`: Lustre = Linux + Cluster
    - File storage for **High Performance Computing (HPC)**.
    - Machine learning, analytics, video processing...

## Shared responsibility Model for EC2 (IaaS)

- AWS -> security OF the cloud:
  - Infrastructure, Replacing faulty hardware
  - Replication for data for EBS Volumes and EFS Drives
  - Ensure their employees cannot access your data.
- USER -> security IN the cloud:
  - Setting up backup/snapshot procedures.
  - Setting up data encryption
  - Responsibility of any data on the drives.
  - Understanding the risk of using EC2 Instance Store and losing the storage if EC2 Stops or any hardware fails.

## !Important

- **Elastic File System (EFS)**: Multiple users using concurrently **AT SAME TIME**, files/folders, directories.
- **AMI**: Must be the same region of EC2 instance. Performance doesn't change because of the region.

## Reference

- https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html
- https://docs.aws.amazon.com/imagebuilder/latest/userguide/what-is-image-builder.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html
- https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html
- https://aws.amazon.com/fsx/
