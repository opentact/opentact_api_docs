Friends
=======

Friends in Opentact are relations between subacounts. One subaccount can make a friend with other subaccount. Friends can make calls and send IMs each other.


Be a friend
----------------

To be a friend, make an HTTP POST request to below URI:

    /v1/friends/sid.json or /v1/friends/sid.xml


If successful, Opentact responds with a successful message.


Parameters
^^^^^^^^^^^

========== ===========
Property   Description
========== ===========
friend_sid which sid you want to be a friend
========== ===========


Example
^^^^^^^^


curl -k -u 54af9a2623d399e38299e143:76612d48070140ccb819dd9099f6672a -d friend_sid=54af9aa7afd129484fd600bb  https://api.opentact.org/v1/friends/54af9a97afd129484fd600b9.json::

    {
        "message": "The friend [54af9aa7afd129484fd600bb] is added to [54af9a97afd129484fd600b9] successfully",
        "friend_sid": "54af9aa7afd129484fd600bb",
        "sid": "54af9a97afd129484fd600b9"
    }
    
    
Friends List Resource
------------------------------

To get friends, make an HTTP GET request to below URI:

    /v1/friends/sid.json or /v1/friends/sid.xml
    

Example
^^^^^^^^

curl -k -u 54af9a2623d399e38299e143:76612d48070140ccb819dd9099f6672a https://api.opentact.org/v1/friends/54af9a97afd129484fd600b9.json::


    {
        "friends": [
            "54af9aa7afd129484fd600bb"
        ]
    }
    
    
    
 
