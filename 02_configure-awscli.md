Step 1:  go to the aws document page 
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

Step 2: in my case based on OS (in my case Linux) I have executed below command
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
Step 3: validate 
```
execute  /usr/local/bin/aws --version
```
Sample Output:
```
[ec2-user@ip-10-0-14-30 terraform]$ /usr/local/bin/aws --version
aws-cli/2.11.18 Python/3.11.3 Linux/6.1.25-37.47.amzn2023.x86_64 exe/x86_64.amzn.2023 prompt/off
```
