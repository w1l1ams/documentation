# What is a workflow ?

A workflow is the link between an event from one service to an action on another service.

Workflows will let you connect anything from any technologies to everything you want.

## When should I use workflows ?

If you want to connect different services together even comming from different technologies but you have no skills in how to connect with thoses technologies or if you are a company or developer that want to connect different services but don't want to loose a lot of time to learn all those technologies and how to interact with it in order to just focus on your most important work. 

Also if you are worried about data centralisation and single points of failures, workflows are great because running in a secure decentralised architecture.

## Steps in a workflow

There are 4 different steps in a workflow with 2 required and 2 optionals.

1. [Source](./source.md) (required): The event that will trigger this workflow. 
2. [Filter](./filter.md) (optional): Some filter to select only some event that matches your needs
3. [Parameters](./parameters.md) (optional): Parameters required to trigger the action
4. [Action](./action.md) (required): Action to trigger

## Exemples of workflows

1. **When** I receive a payment on Ethereum blockchain, **then** send me an email notification
2. **When** I call a specific webhook **then** trigger a payment in Bitcoin blockchain
3. **When** I receive a payment on Stripe **then** save it in a spreadsheet
4. ...