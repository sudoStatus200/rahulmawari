---
title: Setup AWS DynamoDB in local with docker
date: "2020-05-12T15:17:02.810Z"
template: "post"
draft: false
slug: "aws-dynamodb-local-docker"
category: "aws"
tags:
  - "AWS"
  - "DynamoDB"
description: "AWS dynamodb can be accessed directly from your system but for that developer needs access to AWS account and It might be possible that you can't or don't want to give access to every developer. DynamoDB charges for reading, writing and storing the data , so testing with AWS DynamoDB directly also could be very expensive. To resolve all these issue amazon provides amazon/dynamodb-local."
---

AWS dynamodb can be accessed directly from your system but for that developer needs access to AWS account and It might be possible that you can't or don't want to give access to every developer. DynamoDB charges for reading, writing and storing the data , so testing with AWS DynamoDB directly also could be very expensive. To resolve all these issue amazon provides
[amazon/dynamodb-local](https://hub.docker.com/r/amazon/dynamodb-local/).

![dynamodb](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fd/DynamoDB.png/220px-DynamoDB.png)

## Step 1 : Pull image and run docker image

- Pull the docker image from this link [amazon/dynamodb-local](https://hub.docker.com/r/amazon/dynamodb-local/)
- Run docker image: `docker run -p 8000:8000 amazon/dynamodb-local`

But this is not enough, We should be running docker image inside the container

## Step 2 : Setup and Run container

By default port is 8000 but It can be changes while running image inside the container.

Command to run inside container with port 9000:
`docker run -d -p 9000:8000 --name dynamo-db-local amazon/dynamodb-local`

Above command will start container dynamo-db-local and DynamoDB port 9000. Now you can access AWS DynamoDB local with endpoint http://localhost:9000/.

## Step 3 : Access DynamoDB local from AWS Cli

I hope you have already setup AWS configuration in your system to run AWS Cli.
If you not setup yet checkout [this](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)

To run an AWS Cli command, you need to specify endpoint to dynamodb and region as well.
For example to list tables:
`aws dynamodb list-tables --endpoint-url http://localhost:9000/ --region example`

Above command will give you list of tables in your local dynamodb(There will be nothing initially, you need to create tables :) ).

Hope it helps you!!!! :)
