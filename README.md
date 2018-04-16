# Interactive Adventure Game Tool

This tool provides an easy to use front-end that allows developers to instantly
 deploy code for your story, or use the generated code as a starting point for
 more complex projects. It was written in Node.js by Thomas Yuill, a designer
 and engineer in the Amazon Advertising team.
 
The tool was edited to become the Alexa Gaming Framework by a group from UCF.
The tool was developed by David Allen, James Jeffrey, Scott Mosher, Peter Tran,
and sponsored by Peter Smith. Improved features include node return and custom audio.

![alt text](https://cloud.githubusercontent.com/assets/7671574/17309622/a574be7a-57f4-11e6-9ea8-a52f20424bc5.png "Interactive Adventure Game Tool Screenshot")

##  How to Get Started

Setup AWS and the Amazon Developer Console

To get started with the included sample project, you'll need to setup a few pre-requisites:

* The tool generates Node.js code that will be deployed to AWS Lambda to handle requests from users passed to you from the Alexa platform. 
* The skill uses a table in AWS DynamoDB to save the user's progress between sessions.  
* You can then register your skill with Alexa using the Amazon Developer website, linking it to your AWS resources.

Set these up with these step-by-step instructions:

1. Create or login to an AWS account. In the AWS Console:
  1. Switch to the "N. Virginia" region, since Alexa Skills are currently only supported in that region.
  
     ![switch_region](https://user-images.githubusercontent.com/18518788/38746496-a11690f6-3f15-11e8-8326-a6487e0064e2.png "AWS Switch Region Screenshot") 
  
  1. Create an AWS Role in IAM with access to Lambda, CloudWatch Logs and DynamoDB.
  
     ![create_role_1](https://user-images.githubusercontent.com/18518788/38746616-134d85c6-3f16-11e8-841a-a09f15b84e3e.png "AWS Create Role Screenshot 1")
     ![create_role_2](https://user-images.githubusercontent.com/18518788/38746753-79f0dcd8-3f16-11e8-986f-ef6588ded620.png "AWS Create Role Screenshot 2")
     ![create_role_3](https://user-images.githubusercontent.com/18518788/38747037-86dcd612-3f17-11e8-975e-73ef8698297b.png "AWS Create Role Screenshot 3")

  1. Create an AWS Lambda function named MyAlexaSkillLambdaFunction being sure to select "Alexa Skills Kit" as the trigger and using the role created above.  Take note of the ARN on the upper right, which you'll configure in the Developer Console later.
  
     ![alt text](https://user-images.githubusercontent.com/18518788/38747198-12d92936-3f18-11e8-8845-098d6f332cfb.png "AWS Lambda Create Trigger Screenshot")

  1. Create an AWS DynamoDB table named MyAlexaSkillTable with the case sensitive primary key "userId".

     ![alt text](https://cloud.githubusercontent.com/assets/7671574/17307587/b80787f2-57ea-11e6-9be2-3df26e8e5947.png "AWS DynamoDB Screenshot")

1. Create or login to an [Amazon Developer account](https://developer.amazon.com).  In the Developer Console: 
  1. [Create an Alexa Skill](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-function) named MySkill and using the invocation name "my skill" and using the ARN you noted above making sure it is a custom skill.

     ![alt text](https://user-images.githubusercontent.com/18518788/38747438-df0d5e64-3f18-11e8-9f37-b3282dc79bf6.png "Developer Portal Skill Information Screenshot")

     ![alt text](https://user-images.githubusercontent.com/18518788/38747659-916bc8de-3f19-11e8-8744-edfe55168f37.png "Developer Portal Configuration Screenshot")

## Set up Your Machine

Next, you'll setup your local environment to run the tool.  It's run using Node.js and you access it with a standard web browser. You need to use node 6.10.0 in order for the tool to work properly.  On OS X:

1. Configure AWS credentials the tool will use to upload code to your Skill.  You do this by creating a file under a ".aws" directory in your home directory.

    ```
    mkdir ~/.aws/
    touch ~/.aws/credentials
    ```

2. The file should have the format, and include keys you retrieve from the AWS console:

    ```
    [default]
    aws_access_key_id = [KEY FROM AWS]
    aws_secret_access_key = [SECRET KEY FROM AWS]
    ```

3.	Setup NodeJS and NPM:

    ```
    brew install node
    ```

4.	Get the code and install dependencies:

    ```
    git clone  https://github.com/alexa/interactive-adventure-game-tool.git
    npm install
    ```

5.	Launch:

    ```
    npm start
    ```

	On Microsoft Windows:
	
1. Configure AWS credentials the tool will use to upload code to your Skill.  You do this by creating a file under a ".aws" directory in your home directory.

    ```
    mkdir ~/.aws/
    touch ~/.aws/credentials
    ```

2. The file should have the format, and include keys you retrieve from the AWS console:

    ```
    [default]
    aws_access_key_id = [KEY FROM AWS]
    aws_secret_access_key = [SECRET KEY FROM AWS]
    ```

3.	Setup NodeJS and NPM by acquiring node 6.10.0 from the website and NPM.

4.	Get the code:

    ```
    git clone  https://github.com/alexa/interactive-adventure-game-tool.git
    ```

5.  Move to the file folder and install dependencies:

	```
	cd "Path of the folder"
	npm install
    ```
	
6.	Launch:

    ```
    npm start
    ```
	
Also unzip the initial configuration zip.

## Using the Tool

Once the tool opens in a browser window, you'll see that a sample project is pre-loaded that shows off the main features of the tool.

On the left, you'll see a tree of nodes, which represents how users will navigate your skill.  Users start at the big blue "Start" node.

The smaller bubbles above each node represents the utterance, a phrase the user will say to reach that node, and Alexa will read these to the user when they reach the parent node unless you override this using "Override Default Prompt" or if the node is hidden (see below).

In the sample skill, an example interaction with Alexa might be:

```
User:  Alexa, launch My Alexa Skill.
Alexa:  Welcome to my Alexa Skill.  To learn how to use this skill, say "Help".  When you are ready, say "Begin".
User:  Begin
Alexa:  You enter a room with three doors, each with a distinct number on it. Which door would you like to open?
```

If you select a node, you can see the Voice and Card elements on the right that Alexa will send/say to the user upon reaching the node.

Under the "Advanced" options, you can change the color of the node to help you organize (colors don't change the behavior of your skill) and you can "hide" nodes, causing Alexa to skip reading their utterance as part of the default prompt of the parent.

If you click on an utterance, you can enter multiple variations of the phrase that will also be accepted by Alexa.  Only the first one will be read to the user in the default prompt.

Lastly, the icons on the upper right allow you to:

* ![alt text](https://cloud.githubusercontent.com/assets/7671574/17307920/48d152f8-57ec-11e6-9bdd-f24c9695ce49.png "Save Icon") Save the Skill code, which will be output to "./src/skill". 
* ![alt text](https://cloud.githubusercontent.com/assets/7671574/17307929/515c27ae-57ec-11e6-8347-3736778f1b41.png "Upload Icon")
 Upload the Skill code to the Lambda function you configured earlier.  You can configure the function name by clicking the home icon and changing the values under "AWS Settings".
* ![alt text](https://cloud.githubusercontent.com/assets/7671574/17307932/53fc7e50-57ec-11e6-8019-00fa8054e53e.png "Help Icon") See help content for the tool.

The new features include customizable audio, node transitions, and variables that allow for sections to be inaccessible until items are acquired.
![alt text](https://user-images.githubusercontent.com/18518788/38817497-81a4b1fa-4166-11e8-9709-e299bac5266b.png "New Tools")

## Finishing Deployment of Your Skill

You'll need to complete the configuration manually by logging into the [Developer Console](https://developer.amazon.com) and accessing the "My Alexa Skill" you created above.  On the "Interaction Model" tab, copy and paste the Intent Schema from "./src/skill/models/intentSchema.json" and Sample Utterances from "./src/skill/models/utterances.txt".

Congrats!  Enjoy and let your imagination run wild, we can't wait to see what you come up with!
