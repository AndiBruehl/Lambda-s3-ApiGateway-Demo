ha115-get

import json
import boto3

def lambda_handler(event, context):
    # TODO implement
    
    s3 = boto3.client('s3')
    bucket_name = 'ha115'
    file_name = event["pathParameters"]["messageid"]
    
    # Get the object
    response_get = s3.get_object(  
        Bucket=bucket_name,
        Key=file_name
    )
    
    # Delete the object
    response_delete = s3.delete_object(
        Bucket=bucket_name,
        Key=file_name 
    )
    
    # Read data from the get_object response (if needed)
    data = response_get['Body'].read().decode('utf-8') 
    
    return {
        'statusCode': 200,
        'body': json.dumps(data)
    }


