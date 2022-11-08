# Hosting a Full-Stack Application

[View Client-side](http://udagrambuck.s3.amazonaws.com/index.html)
Cancel changes


[![Noirl01](https://circleci.com/gh/Noirl01/udacity-cicd.svg?style=svg&circle-token=2461e7f0ac25c24a19267d3996984e5a2d04d986)](http://udagrambuck.s3.amazonaws.com/index.html)


### Dependencies

- NodeJS LTS

- npm LTS

- AWS CLI v2

- Postgres Database.

- File storage for pictures.

### Infrastructure

- Github - CircleCI - AWS RDS - AWS S3 - AWS Elastic Beanstalk

### Pipeline process

- Build
- Hold
- Deploy on approval

### AWS Dependencies

- AWS Elastic Beanstalk(includes EC2) for backend and run enviroment.
- AWS S3 for picture file storaging and Front-end pages.
- AWS RDS for the postgresql database.
- CircleCI for CI/CD.

### Installation

#### Typical Updates

- _CI/CD Needs a manual confirmation to deploy the app on the AWS_

#### Preinstallation Testing

- Making sure backend and front-end works

* Creating a database

```
sudo service postgresql start
sudo -u postgres psql
CREATE DATABASE udagram
CREATE USER fullstackdev WITH PASSWORD fullstackdev;
\c udagram
GRANT ALL PRIVILEGES ON DATABASE udagram TO fullstackdev;
```

- `touch .env ` at (/udagram/udagram-api)
- Filling enviroment variables as follow

```
POSTGRES_HOST="127.0.0.1"
POSTGRES_PORT=5432
POSTGRES_DB="udagram"
POSTGRES_USERNAME="fullstackdev"
POSTGRES_PASSWORD="fullstackdev"
PORT=8080
URL="http://127.0.0.1"
JWT_SECRET=mysecretkeyword
AWS_BUCKET=
AWS_REGION=us-east-1
AWS_PROFILE=default
```

- `npm run build && prod `at (/udagram/udagram-api) & `npm run start`
  at (/udagram/udagram-frontend)
- Viewing localhost:8081(Frontend Enviroment)
- Delete .env and any enviroment variables after finishing the tests.
- Can run the automated tests using `npm run test` view package.json for more commands

#### First Time Installation

- Create IAM User and download the csv.

- Create a RDS Database at AWS with public access using the recommended username and password and don't forget to specifiy a database name.

- Go to the created database Connectivity & security check the VPC group then (Security Groups > Inboud rules > Edit inboud rules) need to accept the traffic either create the elastic beanstalk first and add the IP/PORT or accept all traffic using 0.0.0.0/0 may lead to security issues(Never do it at real projects).

- Create a S3 Bucket instance with public access and mention it at (/udagram/udagram-frontend/bin/deploy.sh) to push the frontend files into the bucket

- You can edit the bucket policy and make it completely public(AWS warns but thats our front-end) move over to the bucket and enable website static hosting.

- Create a Elastic Beanstalk enviroment using the AWS interface / CLI for CLI
  make sure that package.json start script has the same path for the server.js file as Archive.zip when unpacked because AWS servers executes app.js by default if avaliable if not it will run the npm run start.

- Elastic Beanstalk using command. First make sure you authinticated your AWS in command-line and installed eb/aws. `eb init` then head over to the yaml and add the following

```
add deploy:
  artifact: `path to the zip file`
```

then create a eb enviroment

```
eb create --sample `name of your enviroment`
eb list
```

head over to the package.json in deploy script edit the deploy enviroment type the same name you got from eb list enviroment.

- Finally you can run npm run deploy to deploy the backend.
- Head over to your elastic beanstalk and copy the url of it and use it as the api host at the frontend files.

- Grab the url for the backend from EB instance and add it into front-end enviroment apiHost

#### CircleCI Requirements

```
AWS_ACCESS_KEY_ID

AWS_DEFAULT_REGION

AWS_SECRET_ACCESS_KEY

```

- Upon github push it will build and await the approval.
