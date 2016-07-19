---
layout: post
title:  AWS S3 Curl Authentication Version 4
date:   2016-07-07
---

The other day I learned how to access a private Amazon S3 file without using the AWS CLI.

#! /bin/bash

AWS_SECRET=My-S3-Secret
AWS_REGION=My-S3-Bucket-Region
REQ_DATE=$(date -u +%Y%m%d)
REQ_TIME=$(date -u +%H%M%S)
TIMESTAMP=$REQ_DATE'T'$REQ_TIME'Z'
BUCKET_NAME=My-S3-Bucket
FOLDER_NAME=My-S3-Directory
FILE_NAME=My-S3-File

### Assembling Canonical Request

CANONICAL_REQ="GET
/$FOLDER_NAME/$FILE_NAME.conf

host:$BUCKET_NAME.s3-$AWS_REGION.amazonaws.com
x-amz-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
x-amz-date:$TIMESTAMP

host;x-amz-content-sha256;x-amz-date
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855"

echo -n "$CANONICAL_REQ" >> canonical-request.creq

### Calculate String To Sign

CANONICAL_REQ_HASH=$(openssl dgst -sha256 ./canonical-request.creq | sed 's/^.* //')

STRING_TO_SIGN="AWS4-HMAC-SHA256
$TIMESTAMP
$REQ_DATE/$AWS_REGION/s3/aws4_request
$CANONICAL_REQ_HASH"

echo -n "$STRING_TO_SIGN" >> string-to-sign.sts

### Calculate Signature

function encode {
    echo -n "$2" | openssl dgst -sha256 -mac HMAC -macopt "$1" | sed 's/^.* //'
}

DATE_KEY=$(encode key:AWS4$AWS_SECRET $REQ_DATE)
DATE_REGION_KEY=$(encode hexkey:$DATE_KEY $AWS_REGION)
DATE_REGION_SERVICE_KEY=$(encode hexkey:$DATE_REGION_KEY s3)
SIGNING_KEY=$(encode hexkey:$DATE_REGION_SERVICE_KEY aws4_request)

### Calculate Signature

echo "$(openssl dgst -sha256 -mac HMAC -macopt hexkey:$SIGNING_KEY ./string-to-sign.sts | sed 's/^.* //')"

### Remove Temporary Files
rm canonical-request.creq
rm string-to-sign.sts
