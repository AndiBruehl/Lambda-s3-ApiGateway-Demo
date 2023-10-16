ha115-post

import json
import boto3
import uuid

def lambda_handler(event, context):
    # TODO implement
    
    message = event["body"]
    
    # codecs.encode('message', 'rot_13')
    
    s3 = boto3.client('s3')
    
    bucket_name = 'ha115'
    file_name = str(uuid.uuid4()) + '.txt'  # Fix: Added a dot before 'txt'
    file_content = message    

    print('ok')
    response = s3.put_object(
        Body=file_content,
        Bucket=bucket_name,
        Key=file_name
    )
    
    return {
        'statusCode': 200,
        'body': json.dumps('https://s1oq8jrj5c.execute-api.eu-central-1.amazonaws.com/' +  file_name)
    }



