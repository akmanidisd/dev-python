
# Python and AWS SSM Parameter Store

[link](https://towardsdatascience.com/python-and-aws-ssm-parameter-store-7f0e211bb91e)

## Introduction

In any application, it is very common to have some secrets, which our application needs to be able to provide its intended functionalities. It is forbidden to put those secrets in our project folder and commit them to the Github repo. It is a big NO, NO. 🙅‍♂

## Pre-requisites

This tutorial assumes that you already have an AWS account and have access to it. This is required to do the ***KMS*** and ***SSM*** related exercises, in particular, creating the KMS key and putting a parameter into SSM. We are going to use ***aws-cli*** to do this. You can follow the AWS official documentation on how to install and set up the credentials.

Alternatively, you can just do it directly on the AWS console.

## Prepare Python Environment and Dependency

In this section, we will set up all the components required to do SSM parameter decryption.

### Create virtual environment

Let’s create a virtual environment to contain our project dependencies using ***virtualenv***. From your terminal, run the following commands to create the virtual environment and activate it.

```bash
$ > mkdir -p ./demo/kms-ssm-decrypt
$ > cd ./demo/kms-ssm-decrypt
$ ~/demo/kms-ssm-decrypt ❯ virtualenv ./venv
Using base prefix '/Library/Frameworks/Python.framework/Versions/3.8'
New python executable in /Users/billyde/demo/kms-ssm-decrypt/venv/bin/python3.8
Also creating executable in /Users/billyde/demo/kms-ssm-decrypt/venv/bin/python
Installing setuptools, pip, wheel...
done.
$ ~/demo/kms-ssm-decrypt ❯ source ./venv/bin/activate
$ ~/demo/kms-ssm-decrypt (venv) ❯
```

### Install Boto3 library

The only library that is needed is Boto3. Let’s create a text file to keep project dependency and name it requirements.txt.

```text
boto3==1.11.0
```

The reason why we have this text file instead of installing the library straight away is so that we can commit it to a Github repo, instead of the whole ***venv*** to keep the repo size compact. Anyone can then clone the repo and install all the requirements on their machine via ***pip***.

Let’s go ahead and install this package from our terminal.

```bash
$ ~/demo/kms-ssm-decrypt (venv) ❯ pip install -r requirements.txt
Collecting boto3==1.11.0
  Using cached boto3-1.11.0-py2.py3-none-any.whl (128 kB)
Collecting s3transfer<0.4.0,>=0.3.0
  Downloading s3transfer-0.3.2-py2.py3-none-any.whl (69 kB)
     |████████████████████████████████| 69 kB 1.5 MB/s
Collecting botocore<1.15.0,>=1.14.0
  Downloading botocore-1.14.9-py2.py3-none-any.whl (5.9 MB)
     |████████████████████████████████| 5.9 MB 4.6 MB/s
Collecting jmespath<1.0.0,>=0.7.1
  Using cached jmespath-0.9.4-py2.py3-none-any.whl (24 kB)
Collecting urllib3<1.26,>=1.20
  Using cached urllib3-1.25.8-py2.py3-none-any.whl (125 kB)
Collecting python-dateutil<3.0.0,>=2.1
  Using cached python_dateutil-2.8.1-py2.py3-none-any.whl (227 kB)
Collecting docutils<0.16,>=0.10
  Using cached docutils-0.15.2-py3-none-any.whl (547 kB)
Collecting six>=1.5
  Using cached six-1.14.0-py2.py3-none-any.whl (10 kB)
Installing collected packages: urllib3, six, python-dateutil, docutils, jmespath, botocore, s3transfer, boto3
Successfully installed boto3-1.11.0 botocore-1.14.9 docutils-0.15.2 jmespath-0.9.4 python-dateutil-2.8.1 s3transfer-0.3.2 six-1.14.0 urllib3-1.25.8
```

## Create a KMS Key

Since we want to store secret/s, it is better to encrypt it at rest to provide extra layer of security. We are going to create a KMS key that will be used to encrypt and decrypt our secret parameter/s.

From your terminal, run the following command, which will create a KMS key.

```bash
$ ~/demo/kms-ssm-decrypt (venv) ❯ aws kms create-key --description "A key to encrypt-decrypt secrets"
{
    "KeyMetadata": {
        "AWSAccountId": "xxxxxxxxxxxx",
        "KeyId": "ca83c234-7e63-4d8d-1234-28603cb10123",
        "Arn": "arn:aws:kms:ap-southeast-2:xxxxxxxxxxxx:key/ca83c234-7e63-4d8d-1234-28603cb10123",
        "CreationDate": 1580217378.859,
        "Enabled": true,
        "Description": "A key to encrypt-decrypt secrets",
        "KeyUsage": "ENCRYPT_DECRYPT",
        "KeyState": "Enabled",
        "Origin": "AWS_KMS",
        "KeyManager": "CUSTOMER"
    }
}
```

Nice, the command outputs the key metadata onto the console if run successfully. We’re good to continue to the next step.

## Put a Secret into SSM Parameter Store

We are going to store a secret parameter into the SSM parameter store as ***SecureString*** parameter type - simply indicates that the value of the parameter we are storing will be encrypted.

To put a secret parameter, let’s execute the following command from the terminal.

```bash
$ ~/demo/kms-ssm-decrypt (venv) ❯ aws ssm put-parameter --name "/demo/secret/parameter" --value "thisIsASecret" --type SecureString --key-id ca83c234-7e63-4d8d-1234-28603cb10123 --description "This is a secret parameter"
{
    "Version": 1,
    "Tier": "Standard"
}
```

The parameters for the command are self-explanatory, however, I just want to highlight a few of them:

+ name : is the name or path to the parameter you are storing, e.g. it could’ve just been a name like “somesecretpathname” instead of a path like above.

+ value : is the value of the parameter you are storing.

+ type : is the type of the parameter, which in this example is a SecureString to tell SSM to encrypt the value before storing it in the parameter store. If you are just storing a non-secret parameter, then the SSM parameter type would just be String.

+ key-id : is the id of the KMS key you want to use to encrypt the value of the parameter. This is the value of KeyId from the previous section where we generated the KMS key.

+ description : is the description of the parameter you are storing so you know what it’s for.

Awesome. Now, we have our secret parameter stored in the SSM parameter store. Let’s see how we can programmatically retrieve and decrypt it.

## Write a Python Script to Retrieve and Decrypt Secret

Now, it’s time to write the script that will retrieve the secret parameter we just stored in SSM parameter store and decrypt it so we can use it in our application.

Let’s create a new Python file in the project directory and name it ***retrieve_and_decrypt_ssm_secret.py***.

Notice the ***get_parameter()*** function’s argument named ***WithDecryption***. In this exercise, we specify it to be ***True*** because we want to get the secret value and use it in our application. You might ask, why don’t we specify the ***KeyId*** that was used to encrypt it? The answer is, the ***KeyId*** information is actually contained in the encrypted parameter and so, SSM knows which key to use to decrypt the secret with.

The script is runnable from terminal and it accepts an argument, which is the parameter’s name or path. Go ahead and execute it from terminal like this. (Note that Boto3 will look for AWS Credentials in your environment)

```bash
$ ~/demo/kms-ssm-decrypt (venv) ❯ python3 retrieve_and_decrypt_ssm_secret.py "/demo/secret/parameter"Secret is
thisIsASecret
=====
Parameter details
{'Parameter': {'Name': '/demo/secret/parameter', 'Type': 'SecureString', 'Value': 'thisIsASecret', 'Version': 1, 'LastModifiedDate': datetime.datetime(2020, 1, 30, 23, 26, 35, 169000, tzinfo=tzlocal()), 'ARN': 'arn:aws:ssm:ap-southeast-2:xxxxxxxxxxxx:parameter/demo/secret/parameter'}, 'ResponseMetadata': {'RequestId': '5ad11d35-axz6-42a0-90g5-0b7682a79321', 'HTTPStatusCode': 200, 'HTTPHeaders': {'x-amzn-requestid': '5ad07d20-ama6-43c0-90a4-0b7682a11267', 'content-type': 'application/x-amz-json-1.1', 'content-length': '239', 'date': 'Thu, 30 Jan 2020 12:48:53 GMT'}, 'RetryAttempts': 0}}
```

We got the secret parameter back — ***thisIsASecret***. 🙂

Just a reminder that the Github repo is available [here](https://github.com/billydh/kms-ssm-decrypt).
