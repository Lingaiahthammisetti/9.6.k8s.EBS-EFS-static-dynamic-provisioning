\* EBS Static Provisioning Steps:



We need to create the EBS volume in AWS.  create a volume in AWS Elastic Block Store, attach to region us-ease-1c. name the instance ebs-static. volume and ec2 should be same availabley zone.

We need to install the EBS CSI drivers in EKS Cluster.

kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.32"

The worker nodes should have access to connect with EBS volumes. First Add IAM role to worker nodes and then Attach EBSCSI policy to the EC2 instance role.



\* EBS Dynamic Provisioning  Steps:



We need to install the EBS CSI drivers in EKS cluster.

kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.32"

Your nodes should have access to connect with EBS volumes. Attach EBS CSI policy to the EC2 instance role.

someone on behalf of you should create EBC Volume in AWS and equivalent PV in K8s automatically --> dynamic provisioning that one is Storage class.

$kubectl get sc

$kubectl api-resources



\* EFS Static Provisioning Steps:



create EFS volume  efs volume in EKS cluster VPC, not default vpc

Allow EC2 instances on NFS protocol in EFS SG,

Install EFS drivers,

https://github.com/kubernetes-sigs/aws-efs-csi-driver

To install the driver using images stored in the public Amazon ECR registry

Downloading the drivers:

kubectl kustomize  

"github.com/kubernetes-sigs/aws-efs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-2.0" > public-ecr-driver.yaml

Installing the drivers:

$kubectl apply -f public-ecr-driver.yaml

Check IAM access to the instances

Please attach IAM policy to security group.

AmazonEFSCSIDriverPolicy

Note: EFS has one security group(sg-5fe…..dec2) and need to allow nodes security group(sg-0613dl…..7ec2). and open efs security group and edit inbound rules and add node security group.



\* EFS Dynamic Provisioning  Steps:



Installing drivers

https://github.com/kubernetes-sigs/aws-efs-csi-driver

To install the driver using images stored in the public Amazon ECR registry

kubectl kustomize  

"github.com/kubernetes-sigs/aws-efs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-2.0" > public-ecr-driver.yaml

$kubectl apply -f public-ecr-driver.yaml

Check ec2-instance role have access or not

Create a file system in AWS Elastic File System.

Create EFS Volume

(Check EFS SG allowing EC2 SG)

go to Elastic File System --> Network

5.Create SC



\* What is the purpose of PV, PVC, Pod, and Service in Kubernetes?

PV (PersistentVolume): Provides storage in the cluster.

PVC (PersistentVolumeClaim): Requests storage from PV.

Pod: Runs your containerized app.

Service: Exposes Pod(s) for networking.

SC (StorageClass): Defines how storage is dynamically provisioned.

PVC (PersistentVolumeClaim): Requests storage.

Pod: Runs the application.

Service: Exposes the Pod for network access.

