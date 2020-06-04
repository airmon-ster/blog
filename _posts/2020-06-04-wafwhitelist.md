---
layout: single
classes: wide
title:  "DevSecOps: Azure and AWS WAF IP Whitelisting"
---

Whitelist IP’s for app testing!

Hello, Readers! Today I want to write another short blog as the topic has come up a few times while testing web applications for clients. 
First, I should mention that we are not talking about bug bounties here. We are talking about those that test web applications for internal teams as part of a DevSecOps or Secure Software Development Lifecycle (SSDLC) team. When testing an application, it is important that the tester be able to test the application directly as opposed to going through a Web Application Firewall (WAF). Why? Well, the goal is to ensure that the application itself is secured properly by itself. Sometimes app developers come to rely on the use of a WAF completely while paying no attention to the application itself. Not to say that the WAF doesn’t have its use cases, but I believe that any good DevSecOps tester/dev will agree that the WAF should be used as an embodiment of the principle of defense in depth and be that extra little layer that helps secure the entire deployment.
For these reasons, I want to sum up the few, easy steps required to whitelist a tester’s IP address in both Azure at the Application Gateway as well as AWS at CloudFront or API Gateway.
## Azure WAF at the Application Gateway
From the main Azure dashboard search bar, enter WAF and select “Web Application Firewall policies (WAF).” 

{:refdef: style="text-align: center;"}
![](/assets/images/waf/azurewaf1.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*WAF policy from dashboard*
{: refdef}

From there, you will need to either create a new “front door” policy or edit the current policy. In our case, we are creating a new policy for the Application Gateway.

{:refdef: style="text-align: center;"}
![](/assets/images/waf/azurewaf2.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*Create a new policy*
{: refdef}

On the first page of “Create a WAF Policy”, select settings that are appropriate for your deployment. As mentioned above, I am going to create a Regional WAF for the Application Gateway. 

{:refdef: style="text-align: center;"}
![](/assets/images/waf/azurewaf3.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*Edit a policy*
{: refdef}

Following that, move on to the “Policy settings” and, once again, select any options that are appropriate for your deployment. I am going to go directly into the “Prevention” mode for testing purposes. 
It should be noted that if you do not already have WAF rules set up, you may have to tune accordingly to ensure that you do not block all traffic.

{:refdef: style="text-align: center;"}
![](/assets/images/waf/azurewaf4.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*Policy configuration*
{: refdef}

The next screen shows the “Managed rules” which, by default, are the OWASP 3.0 rules. For more information on how the OWASP rule set reacts in a WAF, you can view a white paper that I co-authored during my graduate studies [here](/assets/files/ModSecurity_and_the_OWASP_Ruleset.pdf).

{:refdef: style="text-align: center;"}
![](/assets/images/waf/azurewaf5.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*OWASP default rule set*
{: refdef}

This next screen, “Custom rules” is where the whitelist actually happens. Essentially, we want to say, “Hey, make a new rule, set its priority to 1 so that it precedes the OWASP rules, match on our IP address, and only Log (or Allow) our traffic.” Utilizing this strategy, we are allowing the tester to perform all actions without the OWASP rules getting in the way. The OWASP rules will still apply to any other traffic that does not originate from our IP address.

{:refdef: style="text-align: center;"}
![](/assets/images/waf/azurewaf6.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*Custom rule*
{: refdef}

After this step, just apply the rule to the associated application gateway or “front door” and save the changes. The tester’s IP address should now be whitelisted in Azure.

## AWS WAF
To whitelist a given IP in AWS, the process is not too different. 
Start by searching for “WAF” on the main dashboard search bar and select “WAF & Shield.”

{:refdef: style="text-align: center;"}
![](/assets/images/waf/awswafsearch.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*WAF search bar*
{: refdef}

Next, the top right corner should have a button for “Create web ACL” if you have not set one up before, go ahead and click on that. This should bring you to a screen where you define the ACL details. Enter in the information specific to your deployment and click next.

{:refdef: style="text-align: center;"}
![](/assets/images/waf/awswaf2.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*WAF ACL details*
{: refdef}

Now, we actually need to accept all of the defaults without creating rule sets. We do this because we first need to an an “IP Set” that includes our tester’s IP address. So, for the time being, click through the menus and then select your Web ACL when you return to the AWS WAF dashboard.
Select “IP sets” on the left most menu and create a new one using the button in the top right corner.
Give it a name, region, and then add a CIDR address before clicking “Create IP set.”

{:refdef: style="text-align: center;"}
![](/assets/images/waf/awsIPset.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*WAF IP set*
{: refdef}


Return to the main WAF dashboard, select your ACL, and then in the top right corner create a new rule from the Rules tab to “Add [your] own rules and rule groups.”

{:refdef: style="text-align: center;"}
![](/assets/images/waf/awsAddRule.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*WAF add rule*
{: refdef}

It should be noted that if you do not already have WAF rules set up, you may have to tune accordingly to ensure that you do not block all traffic.
Having said that, select “IP set” as the rule type and give it a name, select your created IP set from the drop-down menu, and allow the traffic before clicking “Add rule.”

{:refdef: style="text-align: center;"}
![](/assets/images/waf/awsWhitelist.jpeg)
{: refdef}
{:refdef: style="text-align: center;"}
*WAF ACL details*
{: refdef}

Finally, select a priority that makes sense within your current rule set as to not block or allow traffic indiscriminately. As mentioned above, this may require tuning depending on your deployment configuration.


## Final Thoughts
This may end up being a trivial and unnecessary blog in some regard, but there have been several circumstances where this process needed to be outlined for my fellow developers and cloud practitioners, so I thought that it was at least worth sharing if not for my own benefit when I need it documented. 
