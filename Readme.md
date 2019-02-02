## Create the stack

1. Create and log into your [AWS account](https://aws.amazon.com).
2. Select **CloudFormation** under the **Management & Governance** section.
3. Select **Create Stack** and select the cloudformation.yaml file.
4. Click **Next** to continue.
5. Give the stack a name. I recommend the name be the site's domain with the **.** replaced with **-**.
6. *Important:* Leave **DNSIsLive** to No.
7. Enter the DNS name for the site. *Do not include www*.
8. Select if you would like to setup a API Backend or Cognito.
9. Click **Next** to continue.
10. Leave this page alone.
11. Click **Next** to continue.
12. Check the **I acknowledge that AWS CloudFormation might create IAM resources** box
13. Click **Nex** to continue.
14. Wait until complete, this will take several minutes.


## Upload placeholder site

1. Return to the console by clicking the AWS logo in the top left.
2. Select **S3** under the **Storage** section.
3. Click the bucket name for you site's domain,not the www bucket, *Be sure to click the bucket name, not just the row*.
4. Select the **Upload** button.
5. Select the **Add files** button.
6. Find and choose the index.html file from this repo.
7. Click the **Upload** button, not the Next button.


## Get the DNS server NS Record

1. Return to the console by clicking the AWS logo in the top left.
2. Select **Route 53** under the **Networking & Content Deliver** section.
3. Select the **Hostes zones** link in the left menu.
4. Select the Domain Name from the list for your new site.
5. Look for the **NS** record Type in the list.
6. Write down the four items in the Value column.


## Configure DNS Server (Namecheap)

1. In a new browser window, log into your [Namecheap](http://namecheap.com) account.
2. Click the Manage button next to your sites domain.
3. Change the Nameservers option from **Namecheap BasicDNS** to **Custom DNS**.
4. Add each item you wrote down to the list, do not include the final period.
5. Click the checkmark to the right of the list to save changes.
6. Log out and close the Namecheap browser window.


## Verify Static Site

1. Wait for 5 minuets. Really, go get a cup of coffee or something.
2. Open a new browser window and go to your domain, without the www subdomain, for example **http://domain.com**.
3. Verify you see the placeholder site.
4. Go to your domain with the www subdomain, for example **http://www.domain.com**.
5. Verify you see the placeholder site.

##### At this point you can upload any site you like to the same place as the placeholder. This is the location for all your static files. If you are not including a backend to your site then you're complete.

---
---
Stop here if you did not select **Yes** to **IncludeAPIBackend**.

---
---



## Wait for Certificate

1. In the AWS browser window return to the console by clicking the AWS logo in the top left.
2. Select **Certificate Manage**r from the **Security, Identity, & Compiance** section.
3. If the **Status** for your sites domain is **Pending validation** wait 5 min and click the refresh button at the top and right of the list of certificates.
4. Waiting for the certificate **status** to be ** Issued** can take up to 24 hours, though it normally about 30 minuets.

## Continue Setup

1. Return to the console by clicking the AWS logo in the top left.
2. Select **CloudFormation** under the **Management & Governance** section.
3. Highlight the stack for your site, it will have the name you gave it earlier.
4. Select the **Actions** button above the list of stacks.
5. Select **Update Stack** from the menu.
6. Select **Next** on to continue with the current tempalte.
7. Change **DNSIsLive** to **Yes**
9. Click **Next** to continue.
10. Leave this page alone.
11. Click **Next** to continue.
12. Check the **I acknowledge that AWS CloudFormation might create IAM resources** box
13. Click **Nex** to continue.
14. Wait until complete, this will take several minutes.


## Verify API

1. Open a new browser window and go to your domain with the api subdomain, for example **http://api.domain.com/test**.
2. You should see a large javascript object as the initial lambda function returns the data that the API Gateway gives it.
3. Return to the console by clicking the AWS logo in the top left.
4. Select **Lambda** under the **Compute** section.
5. You should see a Lambda function with your domain name, the description will be API Backend.

##### At this point your Backend is connected. The Lambda function that was created is very simple and not very useful. You'll want to upload your own code to replace it.


## Update Lambda

1. Select the Lmabda function name that contains your domain name.
2. You can edit the code inline if you want to test anything.
3. Change the **Code entry type** from **Edit code inline** to **Upload a .zip file**.
4. Select the **Upload** button and choose your backend code zip file.
