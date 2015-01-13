Accounts
============

When you first sign up with Opentact, you have just one account, your Master account. But you can also create more accounts... subaccounts are useful for things like segmenting phone numbers and usage data for your customers and controlling access to data. For more information on subaccounts see Using Subaccounts.

Account Instance Resource
----------------------------------------

An Account instance resource represents a single Opentact account.

Resource URI
^^^^^^^^^^^^^^

/v1/accounts/{sid}.json or /v1/accounts/{sid}.xml 

Resource Properties
^^^^^^^^^^^^^^^^^^^^

An Account resource is represented by the following properties:

============  ===========
Property      Description   
============  ===========
sid           A character string that uniquely identifies this account.
type          The type of this account. Either **trial** or **full** if you've upgraded.
owner_sid     The Sid of the parent account for this account. The owner_sid of a parent account is its own sid.    
status        The status of this account. Usually active, but can be **suspended** or **closed**.
name          A human readable description of this account, up to 64 characters long. By default the name is your email address.
date_created  The date that this account was created, in GMT in RFC 2822 format
date_updated  The date that this account was last updated, in GMT in RFC 2822 format.
============  ===========

HTTP GET
^^^^^^^^^

Returns a representation of an account, including the properties above.

Example
""""""""

curl -k -u 54af9a2623d399e38299e143:76612d48070140ccb819dd9099f6672a  https://api.opentact.org/v1/accounts/54af9a2623d399e38299e143.json::
    
    
    {
        "owner_sid": "None",
        "name": "Peter Dao",
        "sid": "54af9a2623d399e38299e143",
        "date_created": "2014-01-01 00:00:00",
        "date_updated": "2014-01-01 00:00:00",
        "status": "active",
        "type": "full"
    }

HTTP POST and PUT
^^^^^^^^^^^^^^^^^^

Allows you to modify the properties of an account.

See the Subaccounts reference for more information on suspending, unsuspending or closing subaccounts using the 'Status' parameter.


Optional Parameters
"""""""""""""""""""

You may POST the following parameters:

======== ===========
Property Description
======== ===========
name	 A human readable description of this account, up to 64 characters long. By default the name is your email address.
status   Alter the status of this account: use closed to irreversibly close this account, suspended to temporarily **suspend** it, or **active** to reactivate it.
======== ===========

Example
"""""""

close a subaccount by POSTing 'status' = 'closed':

curl -k -u 54af9a2623d399e38299e143:76612d48070140ccb819dd9099f6672a -d "status=closed"  https://api.opentact.org/v1/accounts/54af9a97afd129484fd600b9.json::

    {
        "owner_sid": "54af9a2623d399e38299e143",
        "name": "userA",
        "sid": "54af9a97afd129484fd600b9",
        "date_created": "2015-01-09 17:08:39",
        "date_updated": "2015-01-12 19:15:27",
        "status": "closed",
        "type": "full"
    }



