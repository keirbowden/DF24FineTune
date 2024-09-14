# Fine-Tuned LLM for Copilot Actions

Repository for my Dreamforce '24 talk on integrating a Fine Tuned Large Language Model with Einstein Copilot.

## Sample App

The metadata for the sample application to track session proposals for conferences in the talk lives in the force-app directory. 
This is a very simple application with the following custom objects :

- Session__c - an idea for a session to present at a conference. This contains the generic information about the session and is not targeting a particular event.
- Trailblazer_Event__c - an event (e.g. Salesforce World Tour, Dreamforce, Community Conference) that accepts session proposals via a call for papers process.
- Trailblazer_Event_Session__c - a junction object that ties a session to an event - this is the session proposal for the event and contains details of the maximum length of the title and abstract.

Generative AI prompt templates are also included - note that at present (September 2024) it is not possible to deploy prompt templates via the metadata API, so you would need to recreate the templates in a target org manually.

The following field generation templates can be used to generate the title and abstract on a Trailblazer_Event_Session__c record

- Generic_Session_Proposal_Abstract - create the abstract for a generic (non-Salesforce) session proposal. This uses GPT 3.5 Turbo
- Generic_Session_Proposal_Title - as above, but for the title field
- Salesforce_Session_Proposal_Abstract - create the abstract for a Salesforce session proposal. This uses the fine-tuned model created from the training data (see below)
- Salesforce_Session_Proposal_Title - as above, but for the title field

The following flex templates can be wrapped in Copilot actions to suggest a title and abstract:

- Session_Proposal - suggest a title and abstract for a generic (non-Salesforce) session proposal. This uses GPT 3.5 Turbo.
- Salesforce_Session_Proposal - suggest a title and abstract for a Salesforce session proposal. This uses the fine-tuned model created from the training data (see below). Note that this includes multiple versions of the prompt to show the refining process I went through to get a good response.

## Training Data

This contains the JSONL file used to fine-tune the model for the sample app. You can use this as-is with the OpenAI platform to create an identical model to the one I used to help me create my session proposal on fine-tuning, which was ultimately successful!
