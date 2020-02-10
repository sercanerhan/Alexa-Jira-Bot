# Custom Alexa Skill for Assining Jira Issues

This is a fun project for assisning issue via Alexa conversation. Project uses, 
[Amazon Alexa Developer Console](https://developer.amazon.com/alexa/console/ask), Amazon Lambda (Alexa Hosted Python Application) and Jira python library.
Using Jira is the fun point here, the main purpose is the using some handler via  speech of Alxea and triggering some python actions. You may consider that project is a Hello World to developing a Custom Alexa Skill.

## Introduction
Our aim is creating a custom application (Alexa Skill) to assign a Jira issue to a pre-defined user (selecting user is a todo for the project). So , we need to design a flow for interactions. Our flow will be described below image.

<<<<<<< HEAD
- Triggering our application by saying `Alexa, run jira bot application`
- Alexa will welcome use and will ask for the project name. In our case, We use Customer Support Jira Project with the porject key `CS`. 
- So, we will say `Cutomer Support` or `CS` to Alexa.
=======
- Triggering our application by saying 'Alexa, run jira bot application'
- Alexa will welcome use and will ask for the project name. In our case, Ww use Customer Support Jira Project with the porject key 'CS'. 
- So, we will say 'Cutomer Support' or 'CS' to Alexa.
>>>>>>> 20ac3599e8a218977cad37ac6b2ff8a82e171097
- Above action will be handled in our customerSupportHandler and that handler will ask for the issue number. Let's assume that it is 1234.
- Alexa will be waiting for a number value and will catch the 1234 as issue number.
- Finally, Alexa will assign CS-1234 to our pre-defnied user.


![flow](/images/flow.png)

## Using

First ou need a amazon developer account. To get that you have to sign up for [Amazon Alexa Developer Console](https://developer.amazon.com/alexa). After geting a dveloper account go to [Alexa Developer COnsole](https://developer.amazon.com/alexa/console/ask)
then click to **Create Skill**. 

![CreateSkill_1](/images/create_skill_1.png)

You need to select **Custom** from the first menu (Choose a model to add to your skill) and **Alexa-Hosted (Python)** from the second menu (Choose a method to host your skill's backend resources)

![create_skill_2](/images/create_skill_2.png)

### Invocation
Invocation is the triggering word for Alxe to run your custom application. In this case Incovation is the **Jira bot** and we need to say 'Alexa, run jira bot application' to run our application.

<<<<<<< HEAD
Name the Invocation as `Jira bot`
=======
Name the Invocation as 'Jira bot'
>>>>>>> 20ac3599e8a218977cad37ac6b2ff8a82e171097

![invocation](/images/invocation.png)

### Intents
<<<<<<< HEAD
Intents are the basic class which will be handled in handlers. We need to define some words for it then Alexa will understand these words to trigger relevant handler functions. Our example covers the Customer Support project do we will have a `customerSupportIntent` for it.

Create an intent named `customerSupportIntent`
=======
Intents are the basic class which will be handled in handlers. We need to define some words for it then Alexa will understand these words to trigger relevant handler functions. Our example covers the Customer Support project do we will have a 'customerSupportIntent' for it.

Create an intent named 'customerSupportIntent'
>>>>>>> 20ac3599e8a218977cad37ac6b2ff8a82e171097

![intent](/images/Intents.png)

### Slots
<<<<<<< HEAD
Slots are the magic part of the Alexa skills'. We will use them for storing user's answer with the data type definition. Alexa will recieve the issue number as an integer format and store the value in our `issueKey` slot. So, we need to define the slot.
You may get more information with the link below:
[Alexa Slot Type Reference](https://developer.amazon.com/en-US/docs/alexa/custom-skills/slot-type-reference.html)

Crete an `AMAZON.NUMBER` slot named `issueKey`.
=======
Slots are the magic part of the Alexa skills'. We will use them for storing user's answer with the data type definition. Alexa will recieve the issue number as an integer format and store the value in our 'issueKey' slot. So, we need to define the slot.
You may get more information with the link below:
[Alexa Slot Type Reference](https://developer.amazon.com/en-US/docs/alexa/custom-skills/slot-type-reference.html)

Crete an 'AMAZON.NUMBER' slot named 'issueKey'.
>>>>>>> 20ac3599e8a218977cad37ac6b2ff8a82e171097

After completing this step, use must **Save the Model** and **Build the Model** with relevant butons.

### Codes

<<<<<<< HEAD
We will modify two files. The first one is the `requirements.txt` to add our python library which our code needs.

The second file is the `lambda_function.py` which includes main code. This code defines the handler functions and main actions for our applications.
=======
We will modify two files. The first one is the 'requirements.txt' to add our python library which our code needs.

The second file is the 'lambda_function.py' which includes main code. This code defines the handler functions and main actions for our applications.
>>>>>>> 20ac3599e8a218977cad37ac6b2ff8a82e171097

Just like:
```python
class customerSupportIntentHandler(AbstractRequestHandler):
    """Handler for Customer Support Project"""
    def can_handle(self, handler_input):
        return ask_utils.is_intent_name("customerSupportIntent")(handler_input)

    def handle(self, handler_input):
        # Take answered issue key number as string
        issueKey = str(handler_input.request_envelope.request.intent.slots["issueKey"].value)
        # In that example, CS is the Project Key for Customer Support. full_key will be CS-1234 while answered slot value is 1234.
        full_key = 'CS-%s' % issueKey
        
        # Jira Login
        email = 'your_email@address.com'
        key = 'your_AtlassianKey'
        server = 'Your_Jira_Address'
        jira = JIRA(basic_auth=(email, key), options={'server': server})
        jira.issue(full_key).update(assignee = {'name': 'jira_username_to_be_assigned'})
        
        speak_output = ("Ok, It's done. The issue {} has been assigned.".format(issueKey))

        return (
            handler_input.response_builder
                .speak(speak_output)
                .response
        )
<<<<<<< HEAD
```
=======
```
>>>>>>> 20ac3599e8a218977cad37ac6b2ff8a82e171097
