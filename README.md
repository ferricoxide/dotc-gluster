This project contains a set of templates for creating a simple, two-node, Gluster replicated-data cluster. The project includes three templates:
* A template to create an [AWS SecurityGroup](docs/SecurityGroup.md)
* A template to create an [AWS EC2 instance](docs/EC2.md) to act as a Gluster node
* A ["parent" template](docs/Parent.md) to drive the EC2 and SecurityGroup templates
This project is provided to ease deployment of highly-available, persistent storage to AWS Regions that do not (yet) support EFS.
