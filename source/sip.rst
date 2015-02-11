SIP
=======
Account's sip account


SIP Account
-----------------

To get SIP Account, make an HTTP GET request to below URI::

    /v1/accounts/{sid}/sip.json or  /v1/accounts/{sid}/sip.xml
    

Example
^^^^^^^^^

curl -k -u 54af9a2623d399e38299e143:76612d48070140ccb819dd9099f6672a  https://api.opentact.org/v1/accounts/54af9a97afd129484fd600b9/sip.json::

    {
        "sip_password": "sSGkWsYJVk",
        "sid": "54af9a97afd129484fd600b9",
        "status": "online",
        "sip_number": "142079451943305"
    }
        
    
    
