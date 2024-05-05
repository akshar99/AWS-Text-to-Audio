import boto3
import os
from contextlib import closing

# Initialize AWS clients
s3 = boto3.client('s3')
polly = boto3.client('polly')

def lambda_handler(event, context):
    # Get the bucket name and file key from the event
    bucket_name = event['Records'][0]['s3']['bucket']['name']
    file_key = event['Records'][0]['s3']['object']['key']
    output_bucket="text-to-talk-polly"
    
    # Download the text file from S3
    with closing(s3.get_object(Bucket=bucket_name, Key=file_key)['Body']) as file:
        text = file.read().decode('utf-8')
    
    # Convert text to speech using Amazon Polly
    response = polly.synthesize_speech(
        Text=text,
        OutputFormat='mp3',
        VoiceId='Joanna'
    )
    
    # Get the audio stream
    audio_stream = response['AudioStream']
    
    # Upload the audio file to S3
    output_key = os.path.splitext(file_key)[0]  + '.mp3'
    s3.upload_fileobj(
        Fileobj=audio_stream,
        Bucket=output_bucket,
        Key=output_key
    )
    
    return {
        'statusCode': 200,
        'body': f'Successfully converted {file_key} to {output_key}'
    }
