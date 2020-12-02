# CHARITY

The Charity component is the ABAP layer of the application and it has two responsibilities. First, it handles the message coming in from Enterprise Messaging and updates our custom table in our Steampunk system.  Secondly, it exposes the data in our custom table via an OData service leveraging the ABAP RESTful Application Programming(RAP) model.

## Overview

The context in which it runs is shown as the highlighted section of the whiteboard:

![whiteboard, with CHARITY highlighted](./whiteboard-charity.jpg)

The first task of the Charity componet is to handle the incoming message from the webhook subscription in Enterprise Messaging. The webhook subscription is configured to trigger a POST method of our HTTP Service endpoint URL in Steampunk. The ABAP HTTP handler class which is tied to this endpoint URL expects a certain payload containing the relevant data. 

'''abap
* Expected payload example
*{
*    "data": {
*        "data": {
*            "specversion": "1.0",
*            "type": "z.internal.charityfund.increased.v1",
*            "datacontenttype": "application/json",
*            "id": "4c8f6699-f08f-4a3b-8fd6-0b4f26687091",
*            "time": "2020-10-02T13:51:30.888Z",
*            "source": "/default/cap.brain/1",
*            "data": {
*                "salesorder": "1234567",
*                "custid": "USCU-CUS10",
*                "creationdate": "2020-10-02",
*                "credits": 2.27,
*                "salesorg": "1720"
*            }
*        }
*    }
*}

'''

The handler class then updates the custom table with the data coming from Enterprise Messaging.



## Prerequisites

* You have downloaded and installed ABAP Development Tools (ADT). Make sure to use the most recent version as indicated on the installation page.
* You have created an ABAP Cloud Project in ADT that allows you to access your SAP Cloud Platform ABAP Environment instance (see here for additional information). Your log-on language is English.
* You have installed the abapGit plug-in for ADT from the update site http://eclipse.abapgit.org/updatesite/.

## Installation & Configuration

Once you have installed the abapGit plug-in for ADT, you can now clone this repo to your ABAP system and create the required ABAP Objects.  

Currently abapGit does not handle the creation of the HTTP service, so you will need to create that manually and configure that service to point to the handler class ZCL_CDC_REST_SERVICE.

## Running the app

Now that all objects are activated, you can test the RAP application by going to the service binding selecting the entity, and clicking the "Preview" button. 

