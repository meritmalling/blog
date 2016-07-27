---
layout: post
title:  AWS S3 Curl Authentication Version 4
date:   2016-07-07
---

The other day I learned how to access a private Amazon S3 file without using the AWS CLI.

#! /bin/bash

S3_AWS_SECRET=${S3_AWS_SECRET}
S3_AWS_REGION=${S3_AWS_REGION}

REQ_DATE=$2
REQ_TIME=$3
TIMESTAMP=$4
BUCKET_NAME=$5
FOLDER_NAME=$6
FILE_NAME=$7

### Assembling Canonical Request

CANONICAL_REQ="$1
/$FOLDER_NAME/$FILE_NAME.conf
host:$BUCKET_NAME.s3-$S3_AWS_REGION.amazonaws.com
x-amz-content-sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
x-amz-date:$TIMESTAMP
host;x-amz-content-sha256;x-amz-date
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855"

echo -n "$CANONICAL_REQ" >> canonical-request.creq

### Calculate String To Sign

CANONICAL_REQ_HASH=$(openssl dgst -sha256 ./canonical-request.creq | sed 's/^.* //')

STRING_TO_SIGN="AWS4-HMAC-SHA256
$TIMESTAMP
$REQ_DATE/$S3_AWS_REGION/s3/aws4_request
$CANONICAL_REQ_HASH"

echo -n "$STRING_TO_SIGN" >> string-to-sign.sts

### Calculate Singature

function encode {
    echo -n "$2" | openssl dgst -sha256 -mac HMAC -macopt "$1" | sed 's/^.* //'
}

DATE_KEY=$(encode key:AWS4$S3_AWS_SECRET $REQ_DATE)
DATE_REGION_KEY=$(encode hexkey:$DATE_KEY $S3_AWS_REGION)
DATE_REGION_SERVICE_KEY=$(encode hexkey:$DATE_REGION_KEY s3)
SIGNING_KEY=$(encode hexkey:$DATE_REGION_SERVICE_KEY aws4_request)

### Calculate Signature

echo "$(openssl dgst -sha256 -mac HMAC -macopt hexkey:$SIGNING_KEY ./string-to-sign.sts | sed 's/^.* //')"

### Remove Temporary Files
rm canonical-request.creq
rm string-to-sign.sts

By sourcing the above file from another file, passing it the correct inputs (e.g. SINGATURE=$(/etc/signature.sh GET $REQ_DATE $REQ_TIME $TIMESTAMP $BUCKET_NAME $FOLDER_NAME $FILE_NAME)), you will receive the signature of an empty get request. This can then be used in a curl or wget, etc.
