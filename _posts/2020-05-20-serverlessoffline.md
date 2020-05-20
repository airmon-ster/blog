---
layout: single
classes: wide
title:  "Serverless Without the Cloud?"
---

A look into serverless-offline!

What’s going on everybody? Today I want to write a quick blog post about something I started using that has dramatically changed how I write and test APIs in AWS.
If you still haven’t started using an API Gateway/Lambda/DynamoDB flow in AWS or GCF/Azure equivalent, you are really missing out! Serverless allows you to skip most of the capacity planning as it relates to standing up infrastructure quickly in the cloud. API Gateway can take requests in, manipulate them to your heart’s content, and pass them to Lambda for action. Or, perhaps maybe, you don’t care about data manipulation and want to proxy it straight into Lambda! Regardless of implementation, serverless is awesome. So, when something new comes along that makes something awesome even better, it is worth taking note. Enter [serverless-offline](https://www.npmjs.com/package/serverless-offline).

{:refdef: style="text-align: center;"}
![](/assets/images/serverlessoffline.jpg)
{: refdef}
{:refdef: style="text-align: center;"}
*serverless.yml configuration change*
{: refdef}

Imagine being able to even take out the small effort of uploading changes to your Lambda functions as you write your code with the serverless framework. Afterall, are the new changes to your functions even going to work? Are the access controls to your environment deployment ready? It would be so much simpler if you could emulate API Gateway and Lambda locally. Well now you can in three easy steps.

1.	```yarn add serverless-offline (npm install serverless-offline)```
2.	Add serverless-offline to your serverless.yml's plugin section.
3.	```serverless offline```

After those three steps, assuming everything goes well, you will have an API Gateway/Lambda environment emulated on localhost. Additionally, there is also an [offline version of DynamoDB]( https://www.npmjs.com/package/sls-plugin-dynamodb-offline), but it requires some additional JRE setup and I have not tested it yet... However, assuming that your access key and token have the correct permissions, DynamoDB interaction will still work via calling serverless-offline functions by forwarding them to AWS.

{:refdef: style="text-align: center;"}
![](/assets/images/serverlessrunning.jpg)
{: refdef}
{:refdef: style="text-align: center;"}
*serverless-offline up and running*
{: refdef}

Anyway, just a quick blog to keep track of another project. More posts to come!
