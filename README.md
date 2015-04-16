# Deployment Milestone
---------------------------------------------------------------------------------------------

### Project Group Members 

Vineeta Khurana (vkhuran2)

Satvik Andi (sandi)

### Links to Github repository

Code housing Canary and Deployment source files : *https://github.com/satvikandi/Hello.git*

Code having the javascript file for Monitoring :  *https://github.com/satvikandi/Hello.git*


## Steps to Deploy :

### 1. The ability to configure a deployment environment automatically using a configuration management tool

We have used AWS "CloudFormation" service along with Jenkins configurations to create an automatic deployment environment. 

We use a template file to configure the EC2 instance that CloudFormation creates. 

![Alt text] [img1] 

On Jenkins, we use the **"Publish over SSH"** plugin to SSH into our EC2 instance to carry out our pre and post build actions.

![Alt text] [img22] 

In the pre-build step, we SSH into the EC2 instance and set the commands to install nodejs as follows :

![Alt text] [img3]

'nodejs' and 'npm' get installed after this step

![Alt text] [img5]


### 2. The ability to deploy the application on the remote instances after the build step

In the Jenkins post-build actions, we set the commands to install the dependencies required to run our javascript application **app.js** on our Production server.

![Alt text] [img4]

The dependencies are resolved using the npm install command :

![Alt text] [img6]

The application is run using the *'forever start'* command

![Alt text] [img7]

Now, app.js has been deployed on the production server.


### 3. Remote Deployment

We have a remote EC2 instance running that we can SSH into :

![Alt text] [img9]

We can see app.js running on http://52.5.198.199:5000/

![Alt text] [img10]

### 4. Canary Release

For our Canary release, as a Jenkins pre-build step, we have configured another EC2 instance for our canary release similar to our production server.

![Alt text] [img12]

The build ensures the app_canary.js is deployed on the canary server.

![Alt text] [img8]

We can see the app_canary.js running on Canary server i.e http://52.5.160.173:5000/.

![Alt text] [img11]

### 5. Canary Analysis

We run the monitoring app main.js to monitor CPU and memory utilization on the canary server periodically. Thie main.js is run to view the app deployed on production and is accessible via http://52.5.160.173:3000/.

![Alt text] [img13]

![Alt text] [img14]

The threshold to kill the canary, that runs on canary_server's port 5000, has been set to 90 to match against the current CPU utilization. The '*forever stop*' command is used to kill the canary based on threshold. The canary is killed once this threshold is crossed.

![Alt text] [img15]

![Alt text] [img16]

[img1]: ./Images/cloud_form_create.PNG 
[img22]: ./Images/publish_ssh1.PNG
[img3]: ./Images/pre_build.PNG
[img4]: ./Images/post_build.PNG
[img5]: ./Images/nodejs_conop.PNG
[img6]: ./Images/npm_conop.PNG
[img7]: ./Images/forever_conop.PNG
[img8]: ./Images/Canary_build.PNG
[img9]: ./Images/ec2_instances.PNG
[img10]: ./Images/prod_server.PNG
[img11]: ./Images/canary_server.PNG
[img12]: ./Images/canary_prebuild.PNG
[img13]: ./Images/node_main.PNG
[img14]: ./Images/canary_port.PNG
[img16]: ./Images/canary_killed.PNG
[img15]: ./Images/canary_limit.PNG
