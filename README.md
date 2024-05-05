# AWS-Text-to-Audio

I've created a small project that seamlessly transforms text files into audio files on AWS. Here's how it works:

Simply upload a text file to an Amazon S3 bucket. An event trigger is set for .txt files, automatically invoking a Lambda function. The lambda function has an IAM role assigned to it which allows it to access S3 bucket. The Lambda function, powered by AWS Polly, transforms the text file into an audio file. Finally, the audio file is saved in another designated bucket. 
