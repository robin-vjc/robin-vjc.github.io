---
title: "Paypal Adaptive Payments with Python / Django"
excerpt: "Example on how to implement an adaptive paypal payment with python"
---

If you have tried to use Paypal's API to create payments for your website, [you know how painful the experience can be](https://jonathanprior.com/2011/07/11/paypals-dreadful-api-and-documentation/).
For some reason, there is no code snippet on how to implement [adaptive payments](https://developer.paypal.com/docs/classic/adaptive-payments/integration-guide/APIntro/) (parallel and chain) in Python.
Note that for some reason their REST API does not support this particular type of payment, so you can't use
[paypalrestsdk](https://github.com/paypal/PayPal-Python-SDK). You are stuck with the older [NVP API](https://developer.paypal.com/docs/classic/api/NVPAPIOverview/) for this.
{: .text-justify}

Below I provide code snippets to help you get started from your own Django/Flask application. 
{: .text-justify}



First, [get your API credentials](https://developer.paypal.com/docs/classic/lifecycle/sb_credentials/). You should use 
sandbox values while you are still developing your web app.
{: .text-justify}

Then, initialize your credentials and the API endpoint as follows:

{% highlight python %}
HEADERS = {
    'X-PAYPAL-SECURITY-USERID': 'uid_here',
    'X-PAYPAL-SECURITY-PASSWORD': 'pwd_here',
    'X-PAYPAL-SECURITY-SIGNATURE': 'security_sign_here',
    # this application-id is the sandbox value, same for everyone
    'X-PAYPAL-APPLICATION-ID' : 'APP-80W284485P519543T',  
    'X-PAYPAL-REQUEST-DATA-FORMAT': 'JSON',
    'X-PAYPAL-RESPONSE-DATA-FORMAT': 'JSON'
}

# sandbox API endpoint:
ENDPOINT_PAY = 'https://svcs.sandbox.paypal.com/AdaptivePayments/Pay'
{% endhighlight %}

After, define the `dict` that specifies all the payment information:
 
{% highlight python %}
PAYLOAD = {
    'actionType': 'PAY',
    'currencyCode': 'USD',
    'receiverList': {
        'receiver': [
            {'amount': 90, 'email': 'beneficiary1@mail.com'},
            {'amount': 10, 'email': 'beneficiary2@mail.com'}
        ]
    },
    'returnUrl': 'return_url_here',
    'cancelUrl': 'cancel_url_here',
    'requestEnvelope': {
        'errorLanguage': 'en_US',
        'detailLevel': 'ReturnAll'
    },
    # Allowed values: SENDER, PRIMARYRECEIVER, EACHRECEIVER, SECONDARYONLY
    'feesPayer': 'EACHRECEIVER', 
    'reverseAllParallelPaymentsOnError': True,
    'memo': 'Payment description here',
}
{% endhighlight %}

We can now submit our request to create the new payment using `requests`:

{% highlight python %}
import requests
import json

r = requests.post(ENDPOINT_PAY, data=json.dumps(PAYLOAD), headers=HEADERS)
                  
if r.json()['responseEnvelope']['ack'] == 'Success':
    return True
else:
    return False
{% endhighlight %}

Once the transaction is complete, `r` will contain all the confirmation values. You should then 
verify that the payment was succesfully created (`r.json()['responseEnvelope']['ack'] == 'Success'` and
`r.json()['paymentExecStatus'] == 'CREATED'`), and then redirect your user to their page for the payment:

{% highlight python %}
BASE_URL = 'https://www.paypal.com/cgi-bin/webscr?cmd=_ap-payment&paykey='
redirect_url = BASE_URL+r.json()['payKey']
{% endhighlight %}

Hope this helps.
