# IaC - Infrastructure as Code

A dumping ground for learning AWS CloudFormation,
mostly.

## Requirements

*   [An AWS Account](https://aws.amazon.com/account/)
*   [AWS CLi](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)

These instructions assume that you have created an AWS account and
[configured aws-cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)
with that account.

## Cost

Note that NAT Gateways (and other potential future services to be added here) are not free.
Please run this with that understanding,
and create AWS budgets and alerting appropriate to your needs.

## How to Deploy

To deploy a template defined in this repo,
do the following:

1.  Create the stack

    ```sh
    aws cloudformation create-stack \
        --stack-name <MyStackName> \
        --template-body file://stacks/my-vpc.yml \
        --parameters file://params/my-vpc.json
    ```

    Note that aws cli requires the `--template-body` argument to be a
    [file URI](https://en.wikipedia.org/wiki/File_URI_scheme),
    hence `file://`.

1.  Confirm stack creation either in the AWS UI or on the command line

    ```sh
    aws cloudformation describe-stacks
    ```

    The output should be something like the following:

    ```sh
    {
        "Stacks": [
            {
                "StackId": "arn:aws:cloudformation:us-east-1:1234567890:stack/MyStackName/541ffe51-1947-22fc-9bb0-17b37ea42b11",
                "StackName": "MyStackName",
                "CreationTime": "2019-10-07T00:52:21.266000+00:00",
                "RollbackConfiguration": {},
                "StackStatus": "CREATE_COMPLETE",
                "DisableRollback": false,
                "NotificationARNs": [],
                "Tags": [],
                "DriftInformation": {
                    "StackDriftStatus": "NOT_CHECKED"
                }
            }
        ]
    }
    ```

1.  To delete the stack run the following

    ```sh
    aws cloudformation delete-stack --stack-name <MyStackName>
    ```

## Resources

*   [AWS CloudFormation User Guide - Learn template basics](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/gettingstarted.templatebasics.html)
*   [Building a VPC with CloudFormation - Part 1](https://www.infoq.com/articles/aws-vpc-cloudformation/)
