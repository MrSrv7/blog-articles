# AWS SES with NodeJS - Send E-Mails with Amazon AWS's SES utility and Lambda functions

&emsp; If you are a beginner, it might not be easy to set up an E-Mail delivery service like **SendGrid** from scratch and access it programmatically in your **NodeJS** Server application or even a **ReactJS** frontend application. Let's discuss how to set up the same with **AWS's SES** and **Lambda** functions to deliver a welcome email to new users signing up for our application.

## SES

&emsp; If you are unaware of **SES**, Amazon's **Simple Email Service (SES)** is a cloud-based email service provided by **Amazon Web Services (AWS)** that enables businesses to send and receive emails. SES allows developers to send bulk emails to their users with high deliverability. It provides a reliable, cost-effective solution for managing transactional emails such as welcome emails, password reset emails, order confirmations, and other automated emails.

## AWS Setup

&emsp; If you are new to AWS, you should create an **Access Key** (like an **API** key) to use **AWS SDK's** functions from your NodeJS functions after creating an account. Go to the [Security Credentials tab]([IAM Management Console (amazon.com)](https://us-east-1.console.aws.amazon.com/iamv2/home#/security_credentials)) in AWS and create an Access Key for the **IAM** user or root user.

> ***Note: AWS doesn't recommend creating root user access keys. Because you can't specify the root user in a permissions policy, you can't limit its permissions, which is a best practice. Instead, use alternatives such as an IAM role or a user in IAM Identity Center, which provide temporary rather than long-term credentials. If your use case requires an access key, create an IAM user with an access key and apply the least privilege permissions for that user.***

&emsp; As this is for educational purposes, I will create an Access Key for the root user and proceed with that. 

## AWS SES Setup

&emsp; After creating the Access Key, search for SES in the AWS search bar and select Amazon Simple Email Service from the results (I cannot provide the direct link as it will vary according to the region of your account).

<img src="https://i.ibb.co/ZHVV5ZH/image.png" />

&emsp; In SES, select create identity. Enter the from address (from which the emails will be sent to the users). You can verify the domain if you plan to use SES for production. For the sake of this article, I will create an identity with my email address and verify it.

![img](https://i.ibb.co/ZMzZVGD/image.png)

&emsp; After creating the identity, we will receive a verification email from AWS to authenticate the sender's identity. Click on the link in the email and authenticate the same.

<img src="https://i.ibb.co/gMqy0mG/partial-blur.jpg" />

## Serverless Lambda function

&emsp; Now that we have authenticated the from identity, we can set up our serverless lambda function that will trigger and act as an **API** through which we can programmatically send emails to recipients. 

> *We must create a custom role for our lambda function to access **AWS's SES** to send emails. Please follow [AWS SES Setup](https://www.youtube.com/watch?v=o7l9JY2JeoE) for the same.*

<img src="https://i.ibb.co/vzdG7B5/image.png" />

&emsp; Click on **Create Function**. Select the **Author from Scratch** option, give the function a name, and select the architecture and run time (in our case, NodeJS). Scroll down to the code section and enter the following code by selecting `index.js` 

```javascript
const AWS = require('aws-sdk');
const ses = new AWS.SES({ region: 'ap-south-1' });

exports.handler = async (event) => {
  const params = {
    Source: '', // replace with your verified email address
    Destination: {
      ToAddresses: [] // replace with the recipient's email address
    },
    Message: {
      Subject: {
        Data: 'Test email from Lambda' // replace with your email subject
      },
      Body: {
        Text: {
          Data: 'This is a test email sent from a Lambda function.' // replace with your email body
        }
      }
    }
  };
  
  try {
    const result = await ses.sendEmail(params).promise();
    console.log(result);
    return result;
  } catch (err) {
    console.log(err);
    throw err;
  }
};
```

&emsp; After entering the code, click on **Deploy**. Once the changes are deployed successfully, click on **Test** to verify the functionality.

![img](https://i.ibb.co/Wg0xSXB/AWS-Lambda-Function.gif)

&emsp; Now we can programmatically access this AWS Lambda function even from your ReactJS application or our own NodeJS server application like

```javascript
const AWS = require("aws-sdk");

AWS.config.update({
  accessKeyId: "accessKey",
  secretAccessKey: "secretAccessKey",
  region: 'region'
});

const lambda = new AWS.Lambda();

const functionName = "welcomeEmail";

const payload = {};

const params = {
  FunctionName: functionName,
  Payload: JSON.stringify(payload),
};

lambda.invoke(params, function (err, data) {
  if (err) {
    console.error(err);
  } else {
    console.log(data);
  }
});
```

&emsp; Once we run this code with `node filename.js`, we see no errors, and the email has been delivered to our inbox.

**Output**

![img](https://i.ibb.co/bgdpC5v/Whats-App-Image-2023-03-03-at-02-49-46.jpg)

**Mail Inbox**

![img](https://i.ibb.co/6yN3hzQ/Whats-App-Image-2023-03-03-at-02-49-46.jpg)

> *View the GitHub repository here: [MrSrv7/aws-ses-lambda](https://github.com/MrSrv7/aws-ses-lambda)*

## Conclusion

&emsp; This way, we can make a Serverless AWS Lambda function to send emails via AWS's SES programmatically. This is just one of the many advantages of Serverless functions. With the help of serverless functions, we can have our custom functions for custom functionalities without creating a server application from scratch and configuring and maintaining the same. To know more about Serverless functions, checkout. 