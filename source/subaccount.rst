Sub Accounts
============

Subaccounts in Opentact are just accounts that are "owned" by another account. Using a subaccount you can segment each of your customers' use of Opentact and keep it separate from all the rest, allowing you to easily manage the activity and resources of each customer independently.

For instance, if you are running a hosted service that relies on Opentact you can create a Opentact subaccount for each customer that signs up. Then if a customer closes his or her account with your service, you can simply deactivate the associated Opentact subaccount.

Subaccounts allow you to use the Opentact REST API just as you would for a single account; a subaccount can have its own phone numbers and caller IDs, applications, IM and SIP Domains. You can manage a subaccount's calls, SMSs, recordings, and transcriptions without affecting other subaccounts.

Billing
----------

Opentact bills all subaccount usage directly to your master account. You'll have one Opentact balance for all subaccounts. If your master Opentact account is ever suspended, your subaccounts will also be suspended.

Authentication
-----------------------

You can use your master Opentact Account credentials (sid and auth_token) to access Opentact's REST API for your master account as well as any of your subaccounts. You can not use a subaccount's credentials to access the resources of your master Opentact account or any other subaccounts.

Creating Sub Accounts
------------------------------------

To create a new subaccount, make an HTTP POST request to your Accounts list resource URI::

    /v1/accounts.json or /v1/accounts.xml
    
If successful, Opentact responds with a representation of the new Account resource.


POST Parameters
^^^^^^^^^^^^^^^^

Optional Parameters
""""""""""""""""""""""""

Your request to create a subaccount may include the following parameters:

============ ===========
Parameter    Description
============ ===========
name         A human readable description of the new subaccount, up to 64 characters. 
============ ===========


The FriendlyName property is useful for organizing accounts and linking them back to information in your own system. For example, you may want to create subaccounts where the FriendlyName is the primary key of the customer in your application's database.

Example
""""""""


curl -k -u 54af9a2623d399e38299e143:76612d48070140ccb819dd9099f6672a -d "name=userA"  "https://api.opentact.org/v1/accounts.json"::

    
    {
        "sid": "54b48588afd1295433f9f199",
        "type": "full",
        "name": "userA",
        "date_updated": "2015-01-13 10:40:08",
        "status": "active",
        "date_created": "2015-01-13 10:40:08",
        "owner_account_sid": "54af9a2623d399e38299e143"
    }
    
    
Finding a Sub Account
-------------------------------

You can query any particular subaccount and its related resources via the REST API by using that its sid in your URLs. For example:    

curl -k -u 54af9a2623d399e38299e143:76612d48070140ccb819dd9099f6672a  "https://api.opentact.org/v1/accounts/54af9a97afd129484fd600b9.json"::

    {
        "status": "closed",
        "date_updated": "2015-01-12 19:15:27",
        "owner_sid": "54af9a2623d399e38299e143",
        "sid": "54af9a97afd129484fd600b9",
        "name": "userA",
        "date_created": "2015-01-09 17:08:39",
        "type": "full"
    }
    
    
Suspending a Sub Account
---------------------------------------

You can suspend a subaccount if you don't want it to incur any usage charges, however, you will be charged the monthly fee for every Opentact phone number owned by your subaccounts, even when they are suspended. While an account is suspended it cannot make or receive phone calls or send and receive SMS messages. This is useful when your customer does not pay their bill and you want to suspend their account until a successful payment is received.

Simply POST the parameter 'Status' with the value 'suspended' to suspend an account. While suspended, the subaccount will not be able to make or receive phone calls, send or receive IM, send or receive SMS messages, etc.

To reactivate a suspended subaccount, just POST the value 'active' for the 'Status' parameter and we will restore the account to full service.

For details and an example, see the Account instance resource POST section.

Note that you must use your master account's authentication credentials to suspend a subaccount. Also you cannot suspend your master account.



Closing a Subaccount
------------------------------

If your customer closes his or her account with you, you can permanently close the associated Opentact subaccount by POSTing the parameter 'Status' with the value 'closed' to the subaccount resource URI.

When you close a subaccount, Opentact will release all phone numbers assigned to it and shut it down completely. You can't ever use a closed account to make and receive phone calls or send and receive SMS messages. It's closed, gone, kaput. It will still appear in your accounts list, and you will still have access to historical data for that subaccount, but you cannot reopen a closed account.

For details and an example, see the Account instance resource POST section.

Note that you must use your master account's authentication credentials to close a subaccount. Also you cannot close your master account.



Sub Accounts List Resource
--------------------------------------

You can use the Accounts list resource to create subaccounts and retrieve the subaccounts that exist under your main account.

Resource URI
^^^^^^^^^^^^

To create a new subaccount, make an HTTP GET request to your Accounts list resource URI::

    /v1/accounts.json or /v1/accounts
    
HTTP GET
^^^^^^^^^

Retrieve a list of the Sub Account resources belonging to the account.

List Filters
""""""""""""

The following query string parameters allow you to limit the list returned. Note, parameters are case-sensitive:

========= ===========
Parameter Description
========= ===========
name      Only return the Account resources with friendly names that exactly match this name.
status    Only return Account resources with the given status. Can be **closed**, **suspended** or **active**.
========= ===========


List all accounts:
"""""""""""""""""""

curl -k -u 54af9a2623d399e38299e143:76612d48070140ccb819dd9099f6672a  "https://api.opentact.org/v1/accounts.json"::


    {
        "page": 0,
        "accounts": [
            {
                "status": "closed",
                "date_updated": "2015-01-12 19:15:27",
                "owner_sid": "54af9a2623d399e38299e143",
                "sid": "54af9a97afd129484fd600b9",
                "name": "userA",
                "date_created": "2015-01-09 17:08:39",
                "type": "full"
            },
            {
                "status": "active",
                "date_updated": "2015-01-09 17:08:55",
                "owner_sid": "54af9a2623d399e38299e143",
                "sid": "54af9aa7afd129484fd600bb",
                "name": "userB",
                "date_created": "2015-01-09 17:08:55",
                "type": "full"
            },
            {
                "status": "active",
                "date_updated": "2015-01-10 10:18:14",
                "owner_sid": "54af9a2623d399e38299e143",
                "sid": "54b08be6afd12930f3efbcca",
                "name": "userC",
                "date_created": "2015-01-10 10:18:14",
                "type": "full"
            },
            {
                "status": "active",
                "date_updated": "2015-01-10 10:18:19",
                "owner_sid": "54af9a2623d399e38299e143",
                "sid": "54b08bebafd12930f3efbccc",
                "name": "userD",
                "date_created": "2015-01-10 10:18:19",
                "type": "full"
            },
            {
                "status": "active",
                "date_updated": "2015-01-13 10:40:08",
                "owner_sid": "54af9a2623d399e38299e143",
                "sid": "54b48588afd1295433f9f199",
                "name": "userA",
                "date_created": "2015-01-13 10:40:08",
                "type": "full"
            }
        ],
        "page_size": 50,
        "total": 5,
        "num_pages": 1
    }