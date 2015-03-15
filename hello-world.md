```
title: Hello World
tags: [healthcare, api, development]
date: March 1, 2015
slug: hello-world
excerpt: We’re excited here at Akido to launch our blog. We’re releasing features every week so check back to stay up to date on the Akido platform.
author: Team Akido
```
We’re excited here at Akido to launch our blog! We’re releasing Akido features every week, so check back to stay up to date on the Akido platform. We’ll also share thoughts on digital health innovation and product development. You can also follow us on Twitter at @AkidoLabs.

## What is Akido?

Akido is the easiest and safest way to integrate new software into healthcare provider systems. If you’re a developer, integrate once with our modern API and our platform handles the time consuming, expensive, and custom process of integrating with each of your provider customers. If you’re a provider, we integrate with your system (no matter how custom) and forever eliminate integration costs associated with implementing new software.

## We want to unlock fast, safe, health IT innovation

Digital health developers should be focused on solving problems instead of navigating political and technological red tape. This is no mean feat, as there needs to be a very high bar for safety when accessing health data. Security and patient privacy need to be baked in to every choice a hospital makes. However, this shouldn’t prevent us from leveraging technological innovation to improve the quality and efficiency of healthcare. It just means that we have to do it with utmost care. 

## Some builders' inspiration (simple yet powerful Akido API demos)

### Pull Abnormal Patient Results Over Last 24 Hrs

If you’re a practitioner, you can pull all the abnormal patient results in the last 24hrs like this. You're looking at less than 10 lines of code!

```py
#!/usr/bin/python
import urllib, json,time
url="https://testhospital.api.akidolabs.com?_format=json&issued=>" + str(time.time() - 24*60*60)
response = urllib.urlopen(url);
data = json.loads(response)
for result in data:
  if data["interpretation"]["coding"][0]["code"] != "N":
    print "Patient " + data["subject"]["display"] + " had value " + str(data["valueQuantity"]["value"])
```


### Message Practitioner Upon Abnormal Lab Result

This is a simple app that would poll the electronic medical records system every hour and send an SMS to the practitioner if there was anything amiss. Besides comments and instantiating variables, you're looking at 10 lines of code. 

(Note that to send messages with patient information, you would want to use <a href="https://developer.tigertext.com/" target="_blank">TigerText</a> instead of <a href="https://www.twilio.com/api" target="_blank">Twilio</a> to maintain HIPAA compliance...<a href="https://developer.tigertext.com/" target="_blank">TigerText</a> mashup soon to come)

```py
import urllib 
import json
import time
from twilio.rest import TwilioRestClient

# Twilio info
account_sid = "ACda2817bd10290bff2a66021d6204c94a"
auth_token  = "<SECRET DATA>"
from_phone = "+13107517490"
to_phone = "+18182937524"
client = TwilioRestClient(account_sid, auth_token)

# How far back we want to look for results
start_time = str(time.time() - 60 * 60) # An hour ago
# Practioner to fetch labs for
practioner_id = 259386
# URL to fetch lab results from 
url="".join(["https://api.akidolabs.com?_format=json&preformer=", 
      practioner_id, "&issued=>", start_time])
results = json.loads(urllib.urlopen(url));

# Loop through all results in the past hour to see if they are normal or not
for result in results:
  if data["interpretation"]["coding"][0]["code"] != "N":    
    # if the result is abnormal, send a text message to alert the ordering practioner
    message = client.messages.create(body="Abnormal lab detected for one of your patients.",
    to=to_phone,    # Replace with your phone number
    from_=from_phone) # Replace with your Twilio number
    break # We only need to do this once per result set 
```

For more example apps, check out the <a href="https://dash.readme.io/project/akido/v1.0/docs/example-lab-result-notifier" target="_blank">Akido API Docs</a>. More to come weekly!
