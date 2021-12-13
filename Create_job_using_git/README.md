## Creating a CICD(e) Pipeline Localhost -> Git -> Jenkins -> AWS

## Job 1: Cloning and Testing Code on Jenkins Server

![image](https://user-images.githubusercontent.com/14828358/145607674-68c1f96f-d6e0-412d-8e66-c885b333eceb.png)


## Task 
- Create a localhost
- Assign it to a git repo
- Create a secure channel between localhost and git repo
- Create webhook
- Create Jenkins job to test application


## Step 1: Generate SSH key pair

- Generate an ssh key pair in .ssh folder with: (for windows) `ssh-keygen -t -C "<your_email>"`
- This will generate a public (id_rsa.pub) and private (id_rsa) key 

## Step 2: Secure SSH Connection by Adding Public Key to Your GitHub Repo

- Copy the content of the id_rsa.pub 

![image](https://user-images.githubusercontent.com/14828358/145586456-566c3c63-b8dd-496a-a55d-be720b06d056.png)


- On the git repo you want to connect with: `Setting` -> `Deploy keys` -> `Add deploy`

![image](https://user-images.githubusercontent.com/14828358/145585263-470520cc-d714-4420-9351-505078528c8a.png)

- Paste the content into the Key text box
- Click `Allow write access`
- Click `Add key`

![image](https://user-images.githubusercontent.com/14828358/145586821-bdd9ad4a-94fe-4fa8-8990-8c1f5aa621fe.png)

# Step 3: Add Webhook

- Webhooks allow intereaction between web-based applications through the use of custom callback. 
- In this case, we weant to allow git to automaticaly communicate with Jenkins whenever work has been pushed onto the git repo (dev branch)
- `Settings` -> `Webhooks` -> `Add webhook`

![image](https://user-images.githubusercontent.com/14828358/145588542-fa4aff4b-781a-45a3-88e3-b580177bbc6b.png)

- Add the custom webhook url into the Payload URL box

![image](https://user-images.githubusercontent.com/14828358/145589068-2001a47e-fe64-4026-bc1b-ed3c5261fea9.png)


# Step 4: Configure Jenkins Job

- Create a new job on jenkins
- `New Item` -> Name it -> `Freestyle Project`

## General

![image](https://user-images.githubusercontent.com/14828358/145590556-320d7a4d-881e-4c0e-b525-9da794d55d1d.png)

## Office 365 Connector

![image](https://user-images.githubusercontent.com/14828358/145590718-8efa9eca-5013-42ad-be90-a9cb467f86a4.png)

## Source Code Management

- Enter ssh link of repo in Repository URL
- On credential click Add -> Jenkins

![image](https://user-images.githubusercontent.com/14828358/145591812-908e0078-5670-4ae0-b235-ca6f38b235ad.png)



Kind: SSH Username with private key 
ID: Name the key
Private Key: add content of private key (id_rsa)

![image](https://user-images.githubusercontent.com/14828358/145592151-6e31503c-0e42-4db3-978d-82e3c6790652.png)

![image](https://user-images.githubusercontent.com/14828358/145592240-320e4003-a4e6-4d39-ae31-7d166dabeea9.png)


- click Add
- Select the key you made
- Specify branch you want to build from

![image](https://user-images.githubusercontent.com/14828358/145592870-ebe97c15-b0ea-48f2-be08-a47a051fab5d.png)

## Build Trigger

- Click Github hook trigger for GITScm polling

![image](https://user-images.githubusercontent.com/14828358/145593203-b6be569b-b754-4f21-a8ba-82cc03e15611.png)


## Build Environment

- Click Provide Node & npm bin/folder to PATH
- Do nothing else and move on

![image](https://user-images.githubusercontent.com/14828358/145593740-8d488861-8cc9-4d36-af26-263dd1174f45.png)

## Build

- Build -> Execute Shell
- Enter the commands to start the app

![image](https://user-images.githubusercontent.com/14828358/145593885-59dd6e4a-676f-49f8-bd0f-7ba526ddd9d5.png)


Click Apply -> Click Save


# Step 5: Test the job

- Make a change to the git dev branch on localhost and push it to the git repo

![image](https://user-images.githubusercontent.com/14828358/145601533-bb5123b5-8aaf-41c4-82f8-161efb68df91.png)


- Back on jenkins, the server gets sent to a queue


![image](https://user-images.githubusercontent.com/14828358/145602161-5ff60281-891f-4619-94b2-2142dff105b2.png)

- colour of the Sphere represent build success
- Blue -> Success
- Red -> Failure

![image](https://user-images.githubusercontent.com/14828358/145602506-483624ce-a1ba-474f-8ee1-b70a1202e27c.png)

- Click on project -> click on Workspace
- Jenkins clones the repo that you have set up on git hub which it uses to build and test the job

![image](https://user-images.githubusercontent.com/14828358/145602777-e6deea35-6da3-4802-b51b-648552d459e5.png)

- click the number on build history

![image](https://user-images.githubusercontent.com/14828358/145602905-5e9f2f52-0df2-43d6-8c6e-2f586f7e4d2b.png)

- Click on Console Output
- Here you can check errors if build failures

![image](https://user-images.githubusercontent.com/14828358/145603051-7b08fa8e-106e-4dbb-889f-574d6df53d0a.png)


