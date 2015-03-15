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

## Some builders' inspiration

```ruby
#!/usr/bin/python
import urllib, json,time
url="https://testhospital.api.akidolabs.com?_format=json&issued=>" + str(time.time() - 24*60*60)
response = urllib.urlopen(url);
data = json.loads(response)
for result in data:
  if data["interpretation"]["coding"][0]["code"] != "N":
    print "Patient " + data["subject"]["display"] + " had value " + str(data["valueQuantity"]["value"])
```
