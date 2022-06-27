---
tags: [aws, mfa, commandline, security]
date: 2022-06-25
title: How to do MFA for the aws command line
---

# [[2022-06-25 How to do MFA for the aws command line]]

```
#!/bin/bash -e

AWS_USER=grayson
MFA_TOKEN_SERIAL=111222333444
PROFILE_NAME=CompanyName

echo -n "MFA Token: "
read token

response="$(aws sts get-session-token --serial-number arn:aws:iam::${MFA_TOKEN_SERIAL}:mfa/${AWS_USER} --token-code ${token} --profile $PROFILE_NAME-long-term)"

access_key_id=$(echo ${response} | jq -r '.Credentials.AccessKeyId')
secret_access_key=$(echo ${response} | jq -r '.Credentials.SecretAccessKey')
session_token=$(echo ${response} | jq -r '.Credentials.SessionToken')
expiration=$(echo ${response} | jq -r '.Credentials.Expiration')

# You probably want to inline the PROFILE_NAME here
start_line_number=$(grep -n '\[${PROFILE_NAME}]' ~/.aws/credentials | cut -d: -f1)
end_line_number=$(expr ${start_line_number} + 3)

sed -i '' "${start_line_number},${end_line_number}d" ~/.aws/credentials

cat << EOF >> ~/.aws/credentials
[codesee]
aws_access_key_id     = ${access_key_id}
aws_secret_access_key = ${secret_access_key}
aws_session_token     = ${session_token}
EOF

echo "Credentials written to the ${PROFILE_NAME} profile. They will expire at ${expiration}."
```