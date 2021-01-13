# Add a GitLab WebHook to trigger Jenkins job by push event

![gitlab-jenkins-webhook.svg](images/gitlab-jenkins-webhook.svg)

## Install the GitLab plugin

[Official URL](https://plugins.jenkins.io/gitlab-plugin/)

## Generate a GitLab Access Token [optional]

A Jenkins server will establish a connection to communicate with GitLab therefore an API access token is required.

Navigate to **User Settings > Access Tokens** to create a personal access token for Jenkins.

This token will be displayed just once make sure you copy and save it in a secured place.

## Jenkins Configure System [optional]

In GitLab section add a GitLab connection property:

- Connection name
- GitLab host URL
- Credentials (The GitLab personal API access token which is generated from above step)

Test the connection and make sure it works.

## Configuring per-project authentication

If you want to create separate authentication credentials for each Jenkins job:

1. In the configuration of your Jenkins job, in the GitLab configuration section, click 'Advanced'
2. Click the 'Generate' button under the 'Secret Token' field
3. Copy the resulting token, and save the job configuration
4. In GitLab, create a webhook for your project, enter the trigger URL (e.g. `https://JENKINS_URL/project/YOUR_JOB`) and paste the token in the Secret Token field
5. After you add the webhook, click the 'Test' button, and it should succeed

## Configuring global authentication

1. Create a user in Jenkins which has, at a minimum, Job/Build permissions
2. Log in as that user (this is required even if you are a Jenkins admin user), then click on the user's name in the top right corner of the page
3. Click 'Configure,' then 'Show API Token...', and note/copy the User ID and API Token
4. In GitLab, when you create webhooks to trigger Jenkins jobs, use this format for the URL and do not enter anything for 'Secret Token': `https://USERID:APITOKEN@JENKINS_URL/project/YOUR_JOB`
5. After you add the webhook, click the 'Test' button, and it should succeed

## Test The webhook

Now the webhook should trigger the Jenkins job when you push a specific local branch to remote repository.
