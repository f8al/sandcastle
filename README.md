<p align="center">
   
<img src="https://cloud.githubusercontent.com/assets/4115778/24827505/eab7322a-1c42-11e7-96f3-dbc772da5f10.png" width="70%" alt="Sandcastle logo - AWS S3 bucket enumeration">

Originally inspired by a conversation with Instacart's [@nickelser](https://github.com/nickelser) on HackerOne, 0xsearches optimized and published Sandcastle – a Python script for AWS S3 bucket enumeration, formerly known as bucketCrawler.

In December 2022, Securityshrimp updated this code to work with Python 3 while adding Mac support, and support for any other flavor of *nix by adding the ability to provide a custom path the the AWS command line binary

The script takes a target's name as the stem argument (e.g. `shopify`) and iterates through a file of bucket name permutations, such as the ones below:

```
-training
-bucket
-dev
-attachments
-photos
-elasticsearch
[...]
```

## Getting started
Here's how to get started:

1. Clone this repo.
2. pip install requests if you dont have it installed
2. Run `sandcastle.py` with a target name (`-t name`) and input file (`-f foo.txt`)
3. Matching bucket permutations will be identified, and read permissions tested.

```
usage: sandcastle.py [-h] -t targetStem [-f inputFile]

arguments:
  -h, --help            show this help message and exit
  -t targetStem, --target targetStem
                        Select a target stem name (e.g. 'shopify')
  -f inputFile, --file inputFile
                        Select a bucket permutation file (default: bucket-
                        names.txt)
  -a aws binary, --awscli-path  /path/to/aws binary
```

```
   ____             __             __  __
  / __/__ ____  ___/ /______ ____ / /_/ /__
 _\ \/ _ `/ _ \/ _  / __/ _ `(_-</ __/ / -_)
/___/\_,_/_//_/\_,_/\__/\_,_/___/\__/_/\__/

S3 bucket enumeration // release v1.3.0 // SecurityShrimp


[*] Commencing enumeration of 'shopify', reading 138 lines from 'bucket-names.txt'.

[+] Checking potential match: shopify-content --> 403

An error occurred (AccessDenied) when calling the ListObjects operation: Access Denied

```

### Status codes and testing

| Status code        | Definition           | Notes  |
| ------------- | ------------- | -----|
| 404      | Bucket Not Found | Not a target for analysis (hidden by default)|
| 403      | Access Denied      |   Potential target for analysis via the CLI |
| 200 | Publicly Accessible      |    Potential target for analysis via the CLI  |

### AWS CLI commands
Here's a quick reference of some useful AWS CLI commands:
* List Files: `aws s3 ls s3://bucket-name`
* Download Files: `aws s3 cp s3://bucket-name/<file> <destination>`
* Upload Files: `aws s3 cp/mv test-file.txt s3://bucket-name`
* Remove Files: `aws s3 rm s3://bucket-name/test-file.txt`

## What is S3?
From the Amazon [documentation](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingBucket.html), *Working with Amazon S3 Buckets*:
> Amazon S3 [Simple Storage Service] is cloud storage for the Internet. To upload your data (photos, videos, documents etc.), you first create a bucket in one of the AWS Regions. You can then upload any number of objects to the bucket.

> In terms of implementation, buckets and objects are resources, and Amazon S3 provides APIs for you to manage them.

## Closing remarks
* I have taken over this project from 0xSearches.  Their gitub has been inactive since 2017
* This is my first public security project. Sandcastle is published under the MIT License.
* Usage acknowlegements:
  * Castle (icon) by Andrew Doane from the Noun Project
  * Nixie One (logo typeface) free by Jovanny Lemonad
