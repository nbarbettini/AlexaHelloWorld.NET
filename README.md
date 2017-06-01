# Alexa skill using C# and AWS Lambda

This project contains a simple Hello World skill for Alexa. It's written in C# using the [Alexa.NET](https://github.com/timheuer/alexa-skills-dotnet) library and intended to be deployed as a Lambda function.

Follow these steps to try it out yourself:

### Create an Alexa skill

Sign in to [developer.amazon.com](https://developer.amazon.com/) and click on **Alexa**. Create a new skill using the Alexa Skills Kit.

The skill name and invocation phrase can be anything you want. Use the [intent schema](intentSchema.json) and [sample utterances](sampleUtterances.txt) from this repo for the interaction model.

### Create the Lambda function

First, clone and build the project:

```sh
git clone git@github.com:nbarbettini/AlexaHelloWorld.git
cd AlexaHelloWorld
dotnet restore
dotnet build
```

Then, use `dotnet lambda` to deploy the function:

```sh
cd src
dotnet lambda deploy-function -pcfg true
```

The script will prompt you to select an IAM role (pick New Role) and a policy (pick the BasicExecutionRole policy). When it's done propagating, you should see `New Lambda function created`.

### Connect Alexa to Lambda

Log into the [Lambda console](https://developer.amazon.com/) and open the new function you deployed. Add a trigger from Alexa Skills kit, and copy the function **ARN** from the top right of the page.

Switch back to the Alexa Developer console and select the option to use Lambda as the service endpoint for the skill. Paste the ARN of your Lambda function.

### Test it out

Send the `say hello world` utterance with the Service Simulator. You should see a response from your Lambda function:

![Service Simulator screenshot](http://g.recordit.co/IyNub3ni2X.gif)

If you used the same email address for the developer console as you did when you logged into Alexa on your device, you can test the skill live on your device, too!
