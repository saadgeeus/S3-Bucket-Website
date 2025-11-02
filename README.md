# Static Website Hosting on AWS S3

This project demonstrates how to host a static website (HTML, CSS, JS) using **Amazon S3**.

## 🚀 Overview

Amazon S3 allows you to host a static website directly from an S3 bucket.  
This repo contains sample files (like `index.html`) and setup instructions.

---

## 🧱 Prerequisites

Before you start, make sure you have:

- An **AWS account**
- **AWS CLI** installed and configured (`aws configure`)
- Basic knowledge of S3 and IAM

---

## 🪣 Step 1: Create an S3 Bucket

```bash
aws s3 mb s3://your-unique-bucket-name
Replace your-unique-bucket-name with a globally unique name (e.g. saad-static-site-demo).
```
⚙️ Step 2: Enable Static Website Hosting
Go to the AWS Management Console

Open your S3 bucket

Go to Properties → Static website hosting

Choose "Enable"

Set:

Index document: ```index.html```

(Optional) Error document: ```error.html```

Save changes

🔒 Step 3: Make the Bucket Public
Update the bucket policy to allow public read access:

json
Copy code
```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-unique-bucket-name/*"
    }
  ]
}
```
Upload this policy in the Permissions → Bucket Policy section.

📤 Step 4: Upload Website Files
You can upload files via Console or CLI:

Copy code
```bash
aws s3 cp index.html s3://your-unique-bucket-name/ --acl public-read
```
(Repeat for other files if needed.)

🌐 Step 5: Access Your Website
Once hosting is enabled, your website URL will look like:
```bash
http://your-unique-bucket-name.s3-website-<region>.amazonaws.com
```
## Example:
```bash
http://saad-static-site-demo.s3-website-us-east-1.amazonaws.com
```

Open the URL in your browser to view your static site.

🧩 Optional: 
Add a Custom Domain (Route 53 + CloudFront)
If you want to serve your website from your own domain:

Create a Route 53 hosted zone

Configure CloudFront for HTTPS

Link the distribution to your S3 bucket

🧹 Cleanup
When done, delete the bucket to avoid extra charges:

```bash
aws s3 rb s3://your-unique-bucket-name --force
```

🧰 Tools Used
AWS S3 – Static site hosting

AWS CLI – Command-line operations

HTML/CSS/JS – Frontend content

✍️ Author
Saad Khan
DevOps Engineer | AWS | Automation | Cloud Infrastructure
