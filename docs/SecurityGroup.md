The SecurityGroup template can be used as a standalone template or as a child-template. When used as a stand-alone template, it will be necessary to provide sufficient information to the template for it to create a AWS Security-group for use by the Gluster EC2 nodes.

The template takes only one argument, `TargetVPC`. With this parameter, it will create a security group that allows all EC2 instances (or other AWS object types that can use SecurityGroups) with the security-group attached to have unfettered network access to each other. If this is an unacceptably-broad communication capability, use host-based (or service-based) restrictions to cut down on the available communication ports.

It should be noted that use of parameter-files (via the AWS CLI) may make it easier to consistently reproduce security-groups. If using a template from the CLI, the associated parameters file is very simple:
~~~json
[
    {
        "ParameterKey": "TargetVPC",
        "ParameterValue": "__VPC-ID__"
    }
]
~~~
_**Note:** The EC2 instances deployed with this project's templates use `firewalld` to limit inter-node communications._
