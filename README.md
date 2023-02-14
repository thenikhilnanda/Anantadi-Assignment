Uploading a video file to S3 and print the contents of a JSON file using NodeJS.

    const AWS = require('aws-sdk');
    const fs = require('fs');

    // Set up AWS credentials
    AWS.config.update({
    accessKeyId: 'YOUR_ACCESS_KEY_ID',
    secretAccessKey: 'YOUR_SECRET_ACCESS_KEY'
    });

    // Set up S3 client
    const s3 = new AWS.S3();

    // Define file path and type
    const filePath = '/path/to/file';
    const fileType = 'video/mp4';

    // Check if file is a video
    if (fileType === 'video/mp4') {

    // Read the file and upload it to S3
    const fileContent = fs.readFileSync(filePath);
    const params = {
    Bucket: 'YOUR_BUCKET_NAME',
    Key: 'YOUR_OBJECT_KEY',
    Body: fileContent
    };

    s3.upload(params, (err, data) => {
    if (err) {
    console.error(err);
    } else {
    console.log(`File uploaded successfully. Location: ${data.Location}`);
    }
    });

    } else if (fileType === 'application/json') {

    // Read the file and print its contents
    const fileContent = fs.readFileSync(filePath, 'utf8');
    console.log(fileContent);
    } else {
    console.log('File type not supported');
    }
    
