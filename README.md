
# Docker image version manager
___
## install
### Download xml from S3
___ 

### build image
``` shell
docker build -t 560491377201.dkr.ecr.us-east-1.amazonaws.com/download-xml-from-s3:<version> .
docker build -t 560491377201.dkr.ecr.us-east-1.amazonaws.com/download-xml-from-s3:latest .
```

### local test
``` shell
# run container
docker run --rm -p 9000:8080 560491377201.dkr.ecr.us-east-1.amazonaws.com/download-xml-from-s3
 
# execute lambada
curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{"bucket":"<bucket_name>", "keys": [["filename", "key"],["filename", "key"]] }'
```

### Access AWS ECR [[get login](https://docs.aws.amazon.com/cli/latest/reference/ecr/get-login-password.html)]
````shel
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 560491377201.dkr.ecr.us-east-1.amazonaws.com
````

### push image
``` shell
docker push 560491377201.dkr.ecr.us-east-1.amazonaws.com/download-xml-from-s3:latest
```
___

### Call lambda in another Ruby project
```ruby
client = Aws::Lambda::Client.new(region: 'us-east-1')
req_payload = { bucket: '<bucket_name>', keys: ['key', 'key1', '...'] }
payload = JSON.generate(req_payload)
response = client.invoke(function_name: 'download-xml-from-s3', payload: payload)
```
