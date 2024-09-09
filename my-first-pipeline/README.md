# A simple jenkins pipeline to verify if the docker slave configuration is working as expected.

To configure a GitHub webhook for a Jenkins instance running on an EC2 instance, follow these steps:

1. Prepare Jenkins for Webhooks
Install Required Plugins:

Ensure you have the GitHub Plugin and GitHub Integration Plugin installed in Jenkins. You can install these from Manage Jenkins > Manage Plugins > Available tab.
Set Up Jenkins Job:

Create a Jenkins job or pipeline that will be triggered by GitHub commits. Configure it to use the GitHub repository you want to track.
2. Configure Jenkins to Accept Webhooks
Get Jenkins URL:

Make sure Jenkins is accessible from the internet. If you're running Jenkins on an EC2 instance, you need its public IP or domain name. For example, if Jenkins is running on http://ec2-xx-xxx-xxx-xxx.compute-1.amazonaws.com:8080, use this URL.
Create a Jenkins GitHub Webhook URL:

The URL for the GitHub webhook should look like this:

http://<your-jenkins-url>/github-webhook/
Replace <your-jenkins-url> with your actual Jenkins URL.
Configure Jenkins Job to Listen to GitHub Webhooks:

Go to the configuration page of your Jenkins job.
Scroll down to the Build Triggers section.
Check GitHub hook trigger for GITScm polling.


3. Configure GitHub Webhook
Navigate to GitHub Repository Settings:

Go to your GitHub repository.
Click on Settings > Webhooks > Add webhook.
Fill in Webhook Details:

Payload URL: Enter the Jenkins webhook URL from step 2. For example:
bash
Copy code
http://ec2-xx-xxx-xxx-xxx.compute-1.amazonaws.com:8080/github-webhook/
Content type: Select application/json.
Secret: (Optional) Set a secret token for added security. Make sure to configure this in Jenkins under Manage Jenkins > Configure System > GitHub section, if used.
Which events would you like to trigger this webhook?: Choose Just the push event or other events depending on your needs.
Click Add webhook.
Test the Webhook:

You can test the webhook by pushing a change to the repository or manually triggering it from GitHub’s webhook settings page.
4. Check Jenkins for Incoming Webhook Requests
Go back to Jenkins and ensure that the job is triggered by GitHub commits. You should see builds being triggered automatically according to the webhook configuration.
Troubleshooting Tips
Firewall and Security Groups: Ensure that your EC2 instance's security group allows incoming traffic on the port Jenkins is running on (e.g., port 8080).
Jenkins Logs: Check Jenkins logs for any errors related to webhook processing. You can find these in Manage Jenkins > System Log.
