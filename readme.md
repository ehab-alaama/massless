# Massless

Massless is an Open Source cloud file storage server (Similar To Google Drive and Dropbox). Massless uses mongoDB to store file/folder metadata, and supports multiple databases to store the file chunks, such as Amazon S3, the Filesystem, or just MongoDB. Massless is built using Node.js, and Typescript. The service now even supports Docker images! 

The we website is hosted on: https://massless.herokuapp.com/


## Features

* Upload Files
* Download Files
* Google Drive Support
* Personal S3 storage support
* Share Files
* Multiple DB Support (MongoDB, S3, Filesystem)
* Photo Viewer
* Video Viewer
* Thumbnails
* One-time download links
* Move Folder/Files
* Mobile Support
* Docker Support
* Search/Filter Options
* AES256 Encryption
* Access/Refresh tokens

## Installation

Required:
- Node.js (15 Recommended)
- MongoDB (Unless using a service like Atlas)

Windows users will usually need both the microsoft visual build tools, and python 2. These are required to build the sharp module:
- Visual Tools: http://go.microsoft.com/fwlink/?LinkId=691126
- Python 2: https://www.python.org/downloads/release/python-2717/

Linux users will need to make sure they have 'build-essential' installed:
```bash
sudo apt-get install build-essential
```

Setup:
>Install Node Modules
``` javascript
npm install
```

>Run the build command
``` javascript
npm run build
```

>Create Environment Variables: Easily create enviroment variables with the built in command. This command will start a server where you can type in the enviroment variables through a webUI on your browser.
``` javascript
npm run setup
```

>Rebuild the project after entering enviroment variables
``` javascript
npm run build
```

>(Optional) Create the MongoDB indexes, this increases performance. MongoDB must be running for this command to work.
```javascript
npm run create-indexes-database
```

>Start the server
``` javascript
npm run start
```

## Docker

MyDrive has built in Docker support, there are two options when using Docker, users can either use the Docker image that has MongoDB built in, or use the Docker image that just has the MyDrive image (If you're using a service like Atlas).

Create the Docker environment variables by running the 'npm run setup' command as seen in the installation section. Or by manually creating the file (e.g. docker-variables.env on the root of the project, see the environment section for more infomation).

Docker with mongoDB image:
```bash
docker-compose build
```

Docker without mongoDB image:
```bash
docker-compose -f docker-compose-no-mongo.yml build
```
Start the Docker Image:
```bash
docker-compose up
```

## Environment Variables

You can easily create environment variables using the built in setup tool 'npm run setup', or manually create the files.

Create a config folder on the root of the project, and create a file with the name prod.env for the server. For the client variables create a .env.production file in the root of the project. 

Docker: If you're using Docker, instead create a file named 'docker-variables.env' on the root of the project. You must also include DOCKER=true in the servers environment variables. 

Server Environment Variables:

- MONGODB_URL (Required): Sets the MongoDB URL, this should also work with DocumentDB. 
- HTTP_PORT (Required): Sets the HTTP port number.
- HTTPS_PORT (Required): Sets the HTTPS port number.
- REMOTE_URL (Required): This is the URL that the client navigates to in their browser in order to access myDrive. This is needed for things like the Google Drive redirect URL, and including the URL when sending email verification/password reset emails.
- PASSWORD_ACCESS (Required): Sets the JWT secret for access tokens.
- PASSWORD_REFRESH (Required): Sets the JWT secret for refresh tokens.
- PASSWORD_COOKIE (Required): Sets the secret for cookies.
- DB_TYPE (Required): Sets the Database Type, options include s3/mongo/fs.
- NODE_ENV (Required): Must be set to 'production'.
- SSL (Optional): Enables SSL, place certificate.crt, certificate.ca-bundle, and certificate.key at the root of the project. Set this to 'true'
- SECURE_COOKIES (Optional): Makes cookies secure, which means they can only be sent with HTTPS/SSL. Choose this option only if you are using HTTPS.
- KEY (Optional): Encryption key for data, this is not recommended, please use the built in webUI for setting the key.
- DOCKER (Optional/Required): Sets the server to use docker, set this to 'true'.
- FS_DIRECTORY (Optional/Required): Sets the directory for file data on the file system. 
- S3_ID (Optional/Required): Sets the Amazon S3 ID.
- S3_KEY (Optional/Required): Sets the Amazon S3 Key.
- S3_BUCKET (Optional/Required): Sets the Amazon Bucket.
- ROOT (Optional): Uses a filesystem path, is used for storage space.
- URL (Optional): Allows to specify URL to host on, this is usually not needed. 
- USE_DOCUMENT_DB (Optional): Enables documentDB, this is experimental, set this to 'true'.
- DISABLE_EMAIL_VERIFICATION (optional): Disabled email verification when creating an account. Also will not allow users to reset their password with an email.
- SENDGRID_EMAIL (optional): If you are using email verification it is done through sendgrid, enter the sendgrid email address you would like to use. This is the email address users will see when they need to verify their account, or reset their password.
- SENDGRID_KEY (optional): This is the sendgrid API key.
- DOCUMENT_DB_BUNDLE (Optional): Enables SSL with documentDB, set this to 'true'.
- BLOCK_CREATE_ACCOUNT (Optional): Blocks the ability to create accounts, set this to 'true'.

Client Environment Variables

- REMOTE_URL (Required): Sets the Remote URL for the client.
- DISABLE_STORAGE (Optional): Disables storage, use this if you're not using ROOT on the server.
