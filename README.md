# aws-allowlister

![Continuous Integration Tests](https://github.com/salesforce/aws-allowlister/workflows/continuous-integration/badge.svg)

Automatically compile an AWS Service Control Policy that ONLY allows AWS services that are compliant with your preferred compliance frameworks.

![](./examples/media/aws-allowlister.gif)

## Overview

AWS Service Control Policies (SCPs) allow you to control which AWS Service APIs are allowed *at the AWS Account level* - so local administrators (not even the account's root user) can perform prohibited actions in a child account.

 However, before `aws-allowlister`, it was very difficult and error-prone to create AWS AllowList SCPs - only giving accounts access to the compliant services that they need, and nothing else. Before `aws-allowlister`, the approach for creating an AllowList was:
1. Create a spreadsheet 🙄  based on the [AWS Services in Scope](https://aws.amazon.com/compliance/services-in-scope/) documentation, which have inconsistent naming and do not list the "IAM names"
2. Create an AllowList.json by hand, based on that spreadsheet
3. Roll it out to Dev/Stage/Production
4. Whoever manages that spreadsheet now magically owns the AllowList policy due to ✨tribal knowledge✨ and any updates occur by pinging this person over Slack.

`aws-allowlister` takes care of this process for you. Instead of following the painful process above, just run the following command to generate an AWS SCP policy that meets PCI compliance:

```bash
aws-allowlister generate --pci
```

The policies generated by `aws-allowlister` are based off of official AWS [documentation](https://aws.amazon.com/compliance/services-in-scope/) and are automatically kept up to date when new services achieve compliance or accreditation.


### Support statuses

`aws-allowlister` currently supports:

| Compliance Framework | Support Status |
|----------------------|----------------|
| PCI                  | ✅             |
| SOC 1, 2, and 3      | ✅             |
| ISO/IEC              | ✅             |
| HIPAA BAA            | ✅             |
| FedRAMP Moderate     | ✅             |
| FedRAMP High         | ✅             |
| HITRUST              | ⏱ Coming soon |
| DOD CC SRG (USA 🇺🇸)  | ⏱ Coming soon |
| IRAP (Australia 🇦🇺)  | ⏱ Coming soon |
| C5 (Germany 🇩🇪)      | ⏱ Coming soon |
| K-ISMS (Japan 🇯🇵)    | ⏱ Coming soon |
| ENS High (Spain 🇪🇸)  | ⏱ Coming soon |

### Forcibly include/exclude services

In addition to creating compliance-focused SCPs, `aws-allowlister` supports the ability to include or exclude services (IAM permissions) of your choice using the `--include` or `--exclude` flags. For more details related to policy customization, view the [Arguments](#arguments) section.

## Installation

* Python Pip:

```bash
pip3 install aws-allowlister
```

* Homebrew:

```bash
brew tap salesforce/aws-allowlister https://github.com/salesforce/aws-allowlister
brew install aws-allowlister
```

## Usage

* Generate an AllowList Policy using this command:

```bash
aws-allowlister generate
```

By default, it allows policies at the intersection of PCI, HIPAA, SOC, ISO, FedRAMP High, and FedRAMP Moderate.

The resulting policy will look like this:

<details>
<summary>Example AllowList Policy</summary>

```json
{
    "Version": "2012-10-17",
    "Statement": {
        "Sid": "AllowList",
        "Effect": "Deny",
        "NotAction": [
            "account:*",
            "acm:*",
            "amplify:*",
            "amplifybackend:*",
            "apigateway:*",
            "application-autoscaling:*",
            "appstream:*",
            "appsync:*",
            "athena:*",
            "autoscaling:*",
            "aws-portal:*",
            "backup:*",
            "batch:*",
            "clouddirectory:*",
            "cloudformation:*",
            "cloudfront:*",
            "cloudhsm:*",
            "cloudtrail:*",
            "cloudwatch:*",
            "codebuild:*",
            "codecommit:*",
            "codedeploy:*",
            "codepipeline:*",
            "cognito-identity:*",
            "cognito-idp:*",
            "comprehend:*",
            "comprehendmedical:*",
            "config:*",
            "connect:*",
            "dataexchange:*",
            "datasync:*",
            "directconnect:*",
            "dms:*",
            "ds:*",
            "dynamodb:*",
            "ebs:*",
            "ec2:*",
            "ecr:*",
            "ecs:*",
            "eks:*",
            "elasticache:*",
            "elasticbeanstalk:*",
            "elasticfilesystem:*",
            "elasticmapreduce:*",
            "es:*",
            "events:*",
            "execute-api:*",
            "firehose:*",
            "fms:*",
            "forecast:*",
            "freertos:*",
            "fsx:*",
            "glacier:*",
            "globalaccelerator:*",
            "glue:*",
            "greengrass:*",
            "guardduty:*",
            "health:*",
            "iam:*",
            "inspector:*",
            "iot:*",
            "iot-device-tester:*",
            "iotdeviceadvisor:*",
            "iotevents:*",
            "iotwireless:*",
            "kafka:*",
            "kinesis:*",
            "kinesisanalytics:*",
            "kinesisvideo:*",
            "kms:*",
            "lambda:*",
            "lex:*",
            "logs:*",
            "macie2:*",
            "mediaconnect:*",
            "mediaconvert:*",
            "medialive:*",
            "mq:*",
            "neptune-db:*",
            "opsworks-cm:*",
            "organizations:*",
            "outposts:*",
            "personalize:*",
            "polly:*",
            "qldb:*",
            "quicksight:*",
            "rds:*",
            "rds-data:*",
            "rds-db:*",
            "redshift:*",
            "rekognition:*",
            "robomaker:*",
            "route53:*",
            "route53domains:*",
            "s3:*",
            "sagemaker:*",
            "secretsmanager:*",
            "securityhub:*",
            "serverlessrepo:*",
            "servicecatalog:*",
            "shield:*",
            "sms:*",
            "sms-voice:*",
            "snowball:*",
            "sns:*",
            "sqs:*",
            "ssm:*",
            "sso:*",
            "sso-directory:*",
            "states:*",
            "storagegateway:*",
            "sts:*",
            "support:*",
            "swf:*",
            "textract:*",
            "transcribe:*",
            "transfer:*",
            "translate:*",
            "waf:*",
            "waf-regional:*",
            "wafv2:*",
            "workdocs:*",
            "worklink:*",
            "workspaces:*",
            "xray:*"
        ],
        "Resource": "*"
    }
}
```

</details>

## Arguments

`aws-allowlister` supports different arguments to generate fine-grained compliance focused Service Control Policy (SCP) AllowLists. You can specify individual flags for the compliance frameworks you care about.

```
Usage: aws-allowlister generate [OPTIONS]

Options:
  -a, --all                SOC, PCI, ISO, HIPAA, FedRAMP_High, and
                           FedRAMP_Moderate.

  -s, --soc                Include SOC-compliant services
  -p, --pci                Include PCI-compliant services
  -h, --hipaa              Include HIPAA-compliant services
  -i, --iso                Include ISO-compliant services
  -fh, --fedramp-high      Include FedRAMP High
  -fm, --fedramp-moderate  Include FedRAMP Moderate
  --include TEXT           Include specific AWS IAM services, specified in a
                           comma separated string.

  --exclude TEXT           Exclude specific AWS IAM services, specified in a
                           comma separated string.

  -q, --quiet
  --help                   Show this message and exit.
```


* For example, to generate a PCI only Service Control Policy and save it to JSON:

```bash
aws-allowlister generate --pci --quiet > pci.json
```

* You can also chain command flags together. For example, to generate a Policy for all the major compliance frameworks but FedRAMP:

```bash
aws-allowlister generate -sphi --quiet
```

* Let's say your organization is not subject to FedRAMP or HIPAA, but you want to create a Policy for SOC, ISO, and PCI:

```bash
aws-allowlister generate -sip --quiet
```

# Contributing

## Setup

* Set up the virtual environment

```bash
# Set up the virtual environment
python3 -m venv ./venv && source venv/bin/activate
pip3 install -r requirements.txt
```

* Build the package

```bash
# To build only
make build

# To build and install
make install

# To run tests
make test

# To clean local dev environment
make clean
```

# Authors and Contributors

* [Kinnaird McQuade (@kmcquade3)](https://twitter.com/kmcquade3), Salesforce - Author
* [Jason Dyke (@jasonadyke)](https://twitter.com/jasonadyke), ScaleSec - Contributor

# 🚨 Disclaimer 🚨

The policies generated by `aws-allowlister` do not guarantee that your AWS accounts will be compliant or that you will become accredited with the supported compliance frameworks. These policies are intended to be a useful tool to assist with restricting which service can or cannot be leveraged.
