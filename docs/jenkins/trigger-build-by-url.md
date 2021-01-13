# Triggering Jenkins builds by URL

- [Triggering Jenkins builds by URL](https://humanwhocodes.com/blog/2015/10/triggering-jenkins-builds-by-url/)
- [Jenkins Remote Build Trigger – Build Jobs with URL and Token](https://www.middlewareinventory.com/blog/jenkins-remote-build-trigger-url/)

## Step 1: Setting up a new user

Trigger a build via URL means that the Jenkins endpoint is open to anyone who can hit the server. Naturally, that means you want to ensure you’ve secured this endpoint as much as possible and the first step is to create a user with limited access to Jenkins.

## Step 2: Enable the URL job trigger

Under Build Triggers, check the box next to “Trigger Builds Remotely”. You’ll be asked to provide a secure token for validation. This should not in any way be related to the “auto” user, so don’t reuse the password. You might want to generate a new key using a tool like the [Random Key Generator](https://randomkeygen.com/).

![jenkins-triggers.png](images/jenkins-triggers.png)

## Step 3: Enable permission for “auto”

In order to allow “auto” to trigger the build, the user needs to have the following permissions set:

- Overall - Read
- Job - Build
- Job - Read
- Job - Workspace

To configure these permissions:

1. Click on Manage Jenkins
2. Click on Configure Global Security
3. Assuming you’re using matrix-based security: add “auto” to the list and check off the boxes for the necessary permissions
4. Click Save

If you are not using matrix-based security, then this step is likely not necessary. Just make sure the “auto” user has the correct permissions.

## Step 4: Create the URL

In order to make an external call using the “auto” user, you’ll need to use an API token. From the user list, click on the “configure” icon (the wrench and screw driver) next to the “auto” user. Underneath the user’s full name and description is a section labeled “API Token”. Click on the “Show API Token” button. This will reveal the API token you need to provide when triggering a job by URL:

![jenkins-user-token.png](images/jenkins-user-token.png)

Note that “JobName” should be replaced with the job name you’re triggering. The correctly escaped version of this URL is shown when you set the authentication token (step 2).

This URL has three key pieces of information:

1. The username “auto”
2. The API token (after the colon)
3. The authentication token

All three must be correct, and the permissions for the user must be correct in Jenkins, in order for this URL to trigger the job. In order to trigger the job, you must send a POST request. You can test it out using cURL:

```bash
curl -X POST http://auto:8702d1cb53a83f8748d9433ebca494fb@your-jenkins.com/job/JobName/build?token=iFBDOBhNhaxL4T9ass93HRXun2JF161Z
```

Once you send the request, log in to Jenkins and verify that the job is running. You can then use this URL for most webhooks.
