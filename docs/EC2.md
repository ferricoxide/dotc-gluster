The EC2 template can be used as a standalone template or as a child-template. When used as a stand-alone template, it will be necessary to provide sufficient information to the template for it to launch an instance. Unless detailed otherwise, all parameter-values should be filled out.
* If launching the first node of a cluster, the `GlusterPartnerIp` should be left blank.
* If launching the second node of a cluster, the `GlusterPartnerIp` value should be set to the private IP address of the first node. This IP address can be found in the first node's `Outputs` tab (in the CloudFormation console).
* Each cluster's EC2 instances should have uniq `GlusNodeNumber`. Convention is `00` for the first node and `01` for the second node.
* It is recommended that each cluster's EC2 instances have unique `GlusterSubnets` values: this will help assure data availability in the event of an AZ failure.
* All other values should be the same across the cluster's nodes
Templates may be launched either by way of the CloudFormation console or the AWS CLI. If launching via the CLI, it will be necessary to have a parameters file similar to the following:
~~~json
[
    {
        "ParameterKey": "AmiId",
        "ParameterValue": "__AMI-ID__"
    },
    {
        "ParameterKey": "CfnEndpointUrl",
        "ParameterValue": "https://cloudformation.us-east-1.amazonaws.com"
    },
    {
        "ParameterKey": "ClusterInstanceType",
        "ParameterValue": "t2.micro"
    },
    {
        "ParameterKey": "ClusterSecurityGroup",
        "ParameterValue": "__SG-ID__"
    },
    {
        "ParameterKey": "ConsumerApplication",
        "ParameterValue": "__APP-NAME__"
    },
    {
        "ParameterKey": "EpelRepo",
        "ParameterValue": "epel"
    },
    {
        "ParameterKey": "GlusDomName",
        "ParameterValue": "__TLD__"
    },
    {
        "ParameterKey": "GlusNodeName",
        "ParameterValue": "__NODENAME__"
    },
    {
        "ParameterKey": "GlusNodeNumber",
        "ParameterValue": "__NN__"
    },
    {
        "ParameterKey": "GlusterGfsScript",
        "ParameterValue": "https://s3.amazonaws.com/__SCRIPT-BUCKET-PATH__/gluster_fgsconfig.sh"
    },
    {
        "ParameterKey": "GlusterOsprepScript",
        "ParameterValue": "https://s3.amazonaws.com/__SCRIPT-BUCKET-PATH__/gluster_osprep.sh"
    },
    {
        "ParameterKey": "GlusterPartnerIp",
        "ParameterValue": ""
    },
    {
        "ParameterKey": "GlusterSubnets",
        "ParameterValue": "__SUBNET-ID__"
    },
    {
        "ParameterKey": "InstanceProfile",
        "ParameterValue": "__INSTANCEROLE__"
    },
    {
        "ParameterKey": "KeyPairName",
        "ParameterValue": "__KEYNAME__"
    },
    {
        "ParameterKey": "PipRpm",
        "ParameterValue": "python2-pip"
    },
    {
        "ParameterKey": "PyStache",
        "ParameterValue": "pystache"
    },
    {
        "ParameterKey": "ShareVolDev",
        "ParameterValue": "/dev/xvdf"
    },
    {
        "ParameterKey": "ShareVolSize",
        "ParameterValue": "20"
    },
    {
        "ParameterKey": "ShareVolType",
        "ParameterValue": "gp2"
    }
]
~~~
It should be noted that use of parameter-files (via the AWS CLI) may make it easier to ensure that each node has appropriately-overlapping parameter-defines.

_**Note:** It is critical that both nodes be bound to at least one security-group that allows unfettered communications between the gluster nodes. Failure to do so will result in the launch of the second node faulting (due to attempting to communicate with a partner node is lacks sufficient connectivity to)._
