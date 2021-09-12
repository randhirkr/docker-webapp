# docker-webapp
Docker build using amazonlinux for hosting static website.
- pulls latest amazon linux 2 image
- Install all required packages(git, httpd etc.)
- Clones codebase from Github(static website using html, css and javascript)
- Deploys codebase to httpd server and starts the httpd process

Finally, webapp container image is pushed to AWS ECR public repository.

### Steps
Clone the repo and run below commands
```
cd docker-webapp
docker build -t myportfolio .
```

Verify image and test it locally by running it as shown below:
```
docker images -a
docker run -t -i -d  -p 80:80 myportfolio
docker ps 
```

Cleanup local container
```
docker ps
docker container rm <container-id> --force
```

Push image to AWS public ECR by running below commands:
```
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws
docker tag myportfolio:latest public.ecr.aws/c6m5z5o5/myportfolio:v1.0
docker push public.ecr.aws/c6m5z5o5/myportfolio:v1.0
```

Verify image at AWS public ecr gallery:
https://gallery.ecr.aws/c6m5z5o5/myportfolio

### Reference:
https://docs.aws.amazon.com/AmazonECR/latest/public/getting-started-cli.html
