# Creating the Lex bot using aws lambda function and twilio 

Project Details:
1. In this project you will see the creation of the lex bot 
2. Creation of the Lambda function 
3. Connecton between lambda and lexbot
4. Get request in Lambda function 
5. Show data of lambda function in Lex bot
6. Integrate the lex bot in Twilio


# AWS Lex chatbot creation :

1. First go to https://aws.amazon.com/ses/
2. Login to the account and go to aws lex service 
3. Now you are in aws lex dashboard
4. Now click on the bots 
5. SO here we will build a lex bot for post request 
6. Initially we will focus only on creating lex bot 
7. Some terminology before creating the lex bot :
## a. Intent:
In AWS Lex, intent represents the goal or purpose of a user's input in a conversation with a chatbot. It refers to the user's intention or what they want to accomplish with their message. Intents in AWS Lex are created and defined by the bot developer, who specifies the set of user inputs that trigger each intent. The developer can also define the response that the bot should provide when a particular intent is recognized, as well as any necessary actions or backend services that should be invoked to fulfill the user's request.


## b. Slots:
In AWS Lex, a slot is a specific piece of information that the chatbot needs to collect from the user to fulfill their request or intent. Slots represent variables that hold specific values or pieces of data that the bot needs to perform an action or provide a response to the user.
For example, if a user wants to order a pizza through a chatbot, the bot might need to collect information such as the type of pizza, the size of the pizza, and the delivery address. Each of these pieces of information can be represented as a slot.

## c. Utterances: 
In AWS Lex, an utterance is a text or voice message input by a user in a conversation with a chatbot. It represents what the user is saying or asking the bot to do.
For example, if a user wants to order a pizza through a chatbot, they might input an utterance such as "I would like to order a large pepperoni pizza for delivery." The Lex bot would then analyze this utterance and try to match it to an intent and any necessary slots.


![Screenshot (119)](https://user-images.githubusercontent.com/112924115/230888673-0d554488-7392-4b23-ad7a-0c642769c287.png)


8. Now click on create button in bot section 
9. You will see three option like building from scratch,custom,template
10. Choose building from scratch
19. Give any name to  your bot ( we have given "Post_request" in our case)
10. In the permisson chosse the basic IAM role permisson. 
11. Now your bot is created 
12. Now click on the bot you have created . After that multiple option will be open.
13. click on Intent
14. Now name your intent as you want.
15. Under the uttrances train your model
16. Utrances mean what type of input the chatbot wants from user.
17. You can train your model by many type of uttrances 
18. SO after that under response , Enter the response message chatbot will promt to user after the user enter the uttrance
19. Then the main thing comes, that is slots.
20. AS slots are already discussed above so lets create a slot 
21. We will be creating the inbuilt type slots that are provided by default in aws lex.
22. We can also create the custom slots.
23. Now click on the add button in slots and name the first  slot as fcm_token. Choose the type as
 AMAZON.alphanumeric(Store the data like ABC123) . Under promt enter the message you wanna promt to user while asking for data.
24. Now create the next slots same as above and name them as :
```
a. token_type
b. user_type
c. Activity
d. user

```
![Screenshot (120)](https://user-images.githubusercontent.com/112924115/230890854-b5008ddc-3a4e-44f4-a3ff-21192366b3a2.png)


25. Now you are donw with slots
26. Then go to next step that is confirmation promt . It is used for asking the user for confirming the given details.
27. Activate the confirmation promt
28. Fullfilment : This is main step in creating the bot.  When user enter yes after confirmation then fullfiment state is used for fullfilling the user requirements. It is used for terminating the conversation .
29. This state requires the lambda function.
30. SO to fullfillment we will be required the lambda function . As of now we are just testing and creating only lex bot Souncheck the fullfilment
31. You can give any message while ending the conversation by checking the end response section after fullfilment.
32. Now your bot is ready for testing. 
33. Click on build 
34. It may take some in building the chatbot 
35. After that you  can test you chatbot by clicking on test button 
36. Your chatbot  is ready for conversation but it not send any post or get request untill a lambda function is associated with lex bot.
37. SO now lets move to the next step that is creating the lambda function.




# AWS Lambda fuction :

1. Login into aws console and start the aws lambda service 
2. Before start lambda function we need to focus in few things like:--
3. In lambda we can write lambda function in multiple languages.
4. Lambda functon comes with default libraries in each and every language
5. For example if we are working on lambda function that is in python so all the default packages which comes with python 3.9 version will be supported.
6. So to install external library in aws lambda we will be using two mwthods:

```
1. using Layers
2. Using importing the package with python file

```

## Method 1: Using Layers:-

![Screenshot (121)](https://user-images.githubusercontent.com/112924115/230890990-e4ae6364-4b04-4fb3-87d4-77ee096244e9.png)

1. Create a folder in your local disk and run the following command
2. As we need only requests package for implementing our project so run the following commands:-----
```
 
>>D:\>mkdir aws
>>D:\>cd aws
>>D:\aws\>pip install requests -t .

```
3. The last command will install requests package inside the aws package.
4. Now zip the app packages you have got and name it as requests
5. Now go to aws lambda dashboard and under layers click on add layer
6. name the layer as requests 
7. Now you can add the layer into multiple projects or in muliple lambda function

### Note:
```
 Lambda uses amazon linux environment as its OS. Therefore, all the python packages that you install on your Windows laptop/PC may not work on it. Packages installed on Linux based distributions such as Ubuntu work. Mac should also work but not sure. Using Docker on my windows machine, I will be uploading packages installed on Ubuntu to my lambda layer. So, I would also recommend you to install Docker if not already

```

## Method 2 : Using importing direct zip file in lambda fuction:--

1. In this process we will see that how to create the lambda function
2. So now click on functons
3. click on create
4. Name you lambda function as you want (Post_request in our project)
5. Now choose the language you want (Choose python)
6. Chosse the OS type (Choose the first one)
7. Now click on create
8. Now the dashboard will be open for lamda function 
9. Now go to code section .
10. Paste the code given in lambda_function.py file
11. If you will run the code then it will return error (like can't import requests)
12. So for that inside your aws folder in which you have installed the requests  library, create a python file and name it as lambda_function.
13. And paste the code of lambda_function in it.
14. Now make a zip file of all the file and folder inside the aws folder.
15. Now come back to lambda function dashboard you will see a tab like upload from 
16. click on it and select the upload zip and upload your zip.
17. Now your code will automatically reflected in code editor.
18. Now lambda functon is done.
19. The next step is to link the lambda function and the aws lex bot which we have created earlier.
20. Now move to the next step.



# Connection of AWS LEX chatbot and AWS Lambda function:--

1. Go to aws lex dashboard
2. Go to Bots
3. Choose the bot you have created earlier
4. Go to version 
5. Now create a version 
6. Now go to aliases
7. Create a new alias and associate it with the version 1
8. Again go aliases and chosse the alias you have created earlier
9. Click on it and under language section click English (US)
10. Now Choose the name of lambda function you have just created 
11. Also choose the version (Choose LATEST)
12. Save the alias and now rebuild you lex bot by clicking on Build
13. Now click on test and now you can test you bot It will ask you for data and you can basically answer the bot.
14. Some few things that are compulsory to know in lambda  function :
15.  Dialogcodehook: In certain situations, you may want to perform additional validation or manipulation of the input before it is processed by the fulfillment code hook. This is where the dialog code hook comes in.
16.  FulfillmentCodeHook:In the context of AWS Lambda and AWS Lex, a fulfillment code hook is a Lambda function that is responsible for processing the user's input and generating a response.When a user interacts with an AWS Lex bot, their input is passed to a fulfillment code hook for processing. The fulfillment code hook is responsible for interpreting the user's intent, performing any necessary validation or data processing, and generating an appropriate response


# Integration Lex bot with Twilio.:--


1. Sign up for a Twilio account and record the following account information:

 ACCOUNT SID

 AUTH TOKEN

2. To associate the Amazon Lex bot with your Twilio programmable SMS endpoint, activate bot channel association in the Amazon Lex console. When the bot channel association has been activated, Amazon Lex returns a callback URL. Record this callback URL because you need it later.

3. Sign in to the AWS Management Console and open the Amazon Lex console at https://console.aws.amazon.com/lex/.

4. Choose the Amazon Lex bot that you created in Step 1.

5. Choose the Channels tab.

6. In the Chatbots section, choose Twilio SMS.

7. On the Twilio SMS page, provide the following information:

    Type a name. For example, BotTwilioAssociation.

   Choose "aws/lex" from KMS key.

    For Alias, choose the bot alias.

    For Authentication Token, type the AUTH TOKEN for your Twilio account.

   For Account SID, type the ACCOUNT SID for your Twilio account.
![Screenshot (115)](https://user-images.githubusercontent.com/112924115/230887765-3c733cfd-bca2-455c-838b-7d3400da7837.png)

![Screenshot (117)](https://user-images.githubusercontent.com/112924115/230887782-c1077266-87e8-4b58-8c2e-4673089762af.png)
8. Now you will get an endpoint url after this so copy it and paste it in twilio endpoint url.

![Screenshot (118)](https://user-images.githubusercontent.com/112924115/230888426-b80a1371-9da2-41cc-883a-15bb9412b550.png)


Now your bot is ready for working. You can test your bot now.

For extra doucmentation:  https://docs.aws.amazon.com/lex/latest/dg/twilio-bot-association.html
