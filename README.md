# DynamoDB table cloning

Requires :

- python 3
- aws cli & dynamo-local (for the local)

### HOW TO

> Copy a dynamo-local with

```bash
USE_LOCAL=yes python3 dynamo_copy_table.py source-table dest-table
```

> Copy a online dynamo db:

 - copy with table creation
```bash
ACCESS_KEY_ID=aws_access_key_id SECRET_ACCESS_KEY=aws_secret_access_key REGION=ap-east-1 python3 dynamo_copy_table.py source-table dest-table
```
 - skip table creation
```bash
SKIP_CREATION=yes ACCESS_KEY_ID=aws_access_key_id SECRET_ACCESS_KEY=aws_secret_access_key REGION=ap-east-1 python3 dynamo_copy_table.py source-table dest-table
```


### Run your own local DynamoDB-Local:

- aws-cli

```bash
curl -O https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py --user
pip3 install awscli --upgrade --user
```

- dynamo-local

```bash
docker run -p 8000:8000 --name dynamodb-local --restart unless-stopped -d dwmkerr/dynamodb -sharedDb
```

- table

```bash
aws dynamodb list-tables --endpoint-url http://localhost:8000

aws dynamodb create-table --table-name Music --attribute-definitions AttributeName=Artist,AttributeType=S AttributeName=SongTitle,AttributeType=S --key-schema AttributeName=Artist,KeyType=HASH AttributeName=SongTitle,KeyType=RANGE --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1
```
