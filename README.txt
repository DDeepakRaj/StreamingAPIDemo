Use following steps to get the Streaming API Demo running on your org.

1. Create a new custom field on Opportunity Object as following

type: Picklist
		values: North, South, East, West
name: Region
API Name: Region__c

Update all Opportinities so they have value for this newly created Region field.


2. Create Push Topic or channel by running following code using "Excecute Anonymous" in eclipse or in developer console.

-----------------------------------------
PushTopic pushTopic = new PushTopic();
pushTopic.Name = 'OpportunityUpdates';
pushTopic.Query = 'SELECT Id, Name, AccountId, StageName, Amount,ExpectedRevenue, Region__c FROM Opportunity';
pushTopic.ApiVersion = 25.0;
pushTopic.NotifyForOperations = 'All';
pushTopic.NotifyForFields = 'Referenced';
insert pushTopic;
-----------------------------------------

Alternatively, you can use workbench.developerforce.com to create PushTopic.

3. Create three new static resources on your org. Use files  from "staticresources" folder. Keep the name of resources as following

-----------------------------------------
File Name				Resource Name
-----------------------------------------
cometd.js				cometd
jquery_cometd.js		jquery_cometd
jQueryMobile.zip		jQueryMobile
-----------------------------------------

4. Create a new page and paste all the code from "pages\StreamingDemo.page" file.

5. Make sure the Name of PushTopic created in step 2, is used to subscribe the topic in cometd's subscribe method (StreamingDemo.page:Line 49)


