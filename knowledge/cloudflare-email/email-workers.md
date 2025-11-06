[Skip to content](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#_top)
[ ![](https://developers.cloudflare.com/_astro/logo.DAG2yejx.svg) Cloudflare Docs  ](https://developers.cloudflare.com/)
Search`⌘``K`
[Docs Directory](https://developers.cloudflare.com/directory/)[APIs](https://developers.cloudflare.com/api/)[SDKs](https://developers.cloudflare.com/fundamentals/api/reference/sdks/)Help
[ Log in ](https://dash.cloudflare.com/) Select theme Dark Light Auto
[ **Email Routing** ](https://developers.cloudflare.com/email-routing/)
No results found. Try a different search term, or use our global search. 
  * [ Overview ](https://developers.cloudflare.com/email-routing/)
  * Get started
    * [ Overview ](https://developers.cloudflare.com/email-routing/get-started/)
    * [ Enable Email Routing ](https://developers.cloudflare.com/email-routing/get-started/enable-email-routing/)
    * [ Test Email Routing ](https://developers.cloudflare.com/email-routing/get-started/test-email-routing/)
    * [ Analytics ](https://developers.cloudflare.com/email-routing/get-started/email-routing-analytics/)
    * [ Audit logs ](https://developers.cloudflare.com/email-routing/get-started/audit-logs/)
  * Setup
    * [ Overview ](https://developers.cloudflare.com/email-routing/setup/)
    * [ Configure rules and addresses ](https://developers.cloudflare.com/email-routing/setup/email-routing-addresses/)
    * [ DNS records ](https://developers.cloudflare.com/email-routing/setup/email-routing-dns-records/)
    * [ Disable Email Routing ](https://developers.cloudflare.com/email-routing/setup/disable-email-routing/)
    * [ Configure MTA-STS ](https://developers.cloudflare.com/email-routing/setup/mta-sts/)
    * [ Subdomains ](https://developers.cloudflare.com/email-routing/setup/subdomains/)
  * Email Workers
    * [ Overview ](https://developers.cloudflare.com/email-routing/email-workers/)
    * [ Enable Email Workers ](https://developers.cloudflare.com/email-routing/email-workers/enable-email-workers/)
    * [ Edit Email Workers ](https://developers.cloudflare.com/email-routing/email-workers/edit-email-workers/)
    * [ Reply to emails from Workers ](https://developers.cloudflare.com/email-routing/email-workers/reply-email-workers/)
    * [ Send emails from Workers ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/)
    * [ Runtime API ](https://developers.cloudflare.com/email-routing/email-workers/runtime-api/)
    * [ Local Development Beta ](https://developers.cloudflare.com/email-routing/email-workers/local-development/)
    * [ Demos ](https://developers.cloudflare.com/email-routing/email-workers/demos/)
  * Troubleshooting
    * [ Overview ](https://developers.cloudflare.com/email-routing/troubleshooting/)
    * [ DNS records ](https://developers.cloudflare.com/email-routing/troubleshooting/email-routing-dns-records/)
    * [ SPF records ](https://developers.cloudflare.com/email-routing/troubleshooting/email-routing-spf-records/)
  * [ Limits ](https://developers.cloudflare.com/email-routing/limits/)
  * [ Postmaster ](https://developers.cloudflare.com/email-routing/postmaster/)
  * [ API reference ↗ API ](https://developers.cloudflare.com/api/resources/email_routing/subresources/addresses/methods/list/)
  * LLM resources
    * [ llms.txt ](https://developers.cloudflare.com/llms.txt)
    * [ prompt.txt ](https://developers.cloudflare.com/workers/prompt.txt)
    * [ Email Routing llms-full.txt ](https://developers.cloudflare.com/email-routing/llms-full.txt)
    * [ Developer Platform llms-full.txt ](https://developers.cloudflare.com/developer-platform/llms-full.txt)


[GitHub](https://github.com/cloudflare/cloudflare-docs)[X.com](https://x.com/cloudflare)[YouTube](https://www.youtube.com/cloudflare)
Select theme Dark Light Auto
On this page Overview 
  * [ Overview ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#_top)
  * [ Types of bindings ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#types-of-bindings)
  * [ Example Worker ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#example-worker)


## On this page
  * [ Overview ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#_top)
  * [ Types of bindings ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#types-of-bindings)
  * [ Example Worker ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#example-worker)

  

## Was this helpful?
  

[ ](https://github.com/cloudflare/cloudflare-docs/edit/production/src/content/docs/email-routing/email-workers/send-email-workers.mdx) [ ](https://github.com/cloudflare/cloudflare-docs/issues/new/choose)
  1. [ Directory ](https://developers.cloudflare.com/directory/)
  2. … 
  3. [ Email Routing ](https://developers.cloudflare.com/email-routing/)
  4. [ Email Workers ](https://developers.cloudflare.com/email-routing/email-workers/)
  5. [ Send emails from Workers ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/)


Copy page
# Send emails from Workers
You can send an email about your Worker's activity from your Worker to an email address verified on [Email Routing](https://developers.cloudflare.com/email-routing/setup/email-routing-addresses/#destination-addresses). This is useful for when you want to know about certain types of events being triggered, for example.
Before you can bind an email address to your Worker, you need to [enable Email Routing](https://developers.cloudflare.com/email-routing/get-started/) and have at least one [verified email address](https://developers.cloudflare.com/email-routing/setup/email-routing-addresses/#destination-addresses). Then, create a new binding in the Wrangler configuration file:
  * [ ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#tab-panel-1513)
  * [ ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#tab-panel-1514)


```

{



"$schema":"./node_modules/wrangler/config-schema.json",




"send_email":[



{



"name":"<NAME_FOR_BINDING>",




"destination_address":"<YOUR_EMAIL>@example.com"



}


]


}

```

```


send_email=[




{name="<NAME_FOR_BINDING>",destination_address="<YOUR_EMAIL>@example.com"},



]

```

## Types of bindings
[](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#types-of-bindings)
There are several types of restrictions you can configure in the bindings:
  * **No attribute defined** : When you do not define an attribute, the binding has no restrictions in place. You can use it to send emails to any verified email address [through Email Routing](https://developers.cloudflare.com/email-routing/setup/email-routing-addresses/#destination-addresses).
  * **`destination_address`**: When you define the`destination_address` attribute, you create a targeted binding. This means you can only send emails to the chosen email address. For example, `{type = "send_email", name = "<NAME_FOR_BINDING>", destination_address = "<YOUR_EMAIL>@example.com"}`.   
For this particular binding, when you call the `send_email` function you can pass `null` or `undefined` to your Worker and it will assume the email address specified in the binding.
  * **`allowed_destination_addresses`**: When you specify this attribute, you create an allowlist, and can send emails to any email address on the list.
  * **`allowed_sender_addresses`**: When you specify this attribute, you create a sender allowlist, and can only send emails from an email address on the list.


You can add one or more types of bindings to your Wrangler file. However, each attribute must be on its own line:
  * [ ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#tab-panel-1515)
  * [ ](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#tab-panel-1516)


```

{



"$schema":"./node_modules/wrangler/config-schema.json",




"send_email":[



{



"name":"<NAME_FOR_BINDING1>"



},


{



"name":"<NAME_FOR_BINDING2>",




"destination_address":"<YOUR_EMAIL>@example.com"



},


{



"name":"<NAME_FOR_BINDING3>",




"allowed_destination_addresses":[




"<YOUR_EMAIL>@example.com",



"<YOUR_EMAIL2>@example.com"


]


}


]


}

```

```


send_email=[




{name="<NAME_FOR_BINDING1>"},




{name="<NAME_FOR_BINDING2>",destination_address="<YOUR_EMAIL>@example.com"},




{name="<NAME_FOR_BINDING3>",allowed_destination_addresses=["<YOUR_EMAIL>@example.com","<YOUR_EMAIL2>@example.com"]},



]

```

## Example Worker
[](https://developers.cloudflare.com/email-routing/email-workers/send-email-workers/#example-worker)
Refer to the example below to learn how to construct a Worker capable of sending emails. This example uses [MIMEText ↗](https://www.npmjs.com/package/mimetext):
The sender has to be an email from the domain where you have Email Routing active.
JavaScript```


import {EmailMessage} from "cloudflare:email";




import {createMimeMessage} from "mimetext";




exportdefault{




asyncfetch(request,env){




constmsg=createMimeMessage();




msg.setSender({ name:"GPT-4", addr:"<SENDER>@example.com"});




msg.setRecipient("<RECIPIENT>@example.com");




msg.setSubject("An email generated in a worker");




msg.addMessage({




contentType:"text/plain",




data:`Congratulations, you just sent an email from a worker.`,




});




varmessage=newEmailMessage(




"<SENDER>@example.com",




"<RECIPIENT>@example.com",




msg.asRaw(),




);




try{




awaitenv.SEB.send(message);




}catch (e) {




returnnewResponse(e.message);



}



returnnewResponse("Hello Send Email World!");



},


};

```

## Was this helpful?
[](https://github.com/cloudflare/cloudflare-docs/edit/production/src/content/docs/email-routing/email-workers/send-email-workers.mdx)
Last updated: Sep 29, 2025
[ Previous   
Reply to emails from Workers ](https://developers.cloudflare.com/email-routing/email-workers/reply-email-workers/) [ Next   
Runtime API ](https://developers.cloudflare.com/email-routing/email-workers/runtime-api/)
  * **Resources**
  * [ API ](https://developers.cloudflare.com/api/)
  * [ New to Cloudflare? ](https://developers.cloudflare.com/fundamentals/)
  * [ Directory ](https://developers.cloudflare.com/directory/)
  * [ Sponsorships ](https://developers.cloudflare.com/sponsorships/)
  * [ Open Source ](https://github.com/cloudflare)


  * **Support**
  * [ Help Center ](https://support.cloudflare.com/)
  * [ System Status ](https://www.cloudflarestatus.com/)
  * [ Compliance ](https://www.cloudflare.com/trust-hub/compliance-resources/)
  * [ GDPR ](https://www.cloudflare.com/trust-hub/gdpr/)


  * **Company**
  * [ cloudflare.com ](https://www.cloudflare.com/)
  * [ Our team ](https://www.cloudflare.com/people/)
  * [ Careers ](https://www.cloudflare.com/careers/)


  * **Tools**
  * [ Cloudflare Radar ](https://radar.cloudflare.com/)
  * [ Speed Test ](https://speed.cloudflare.com/)
  * [ Is BGP Safe Yet? ](https://isbgpsafeyet.com/)
  * [ RPKI Toolkit ](https://rpki.cloudflare.com/)
  * [ Certificate Transparency ](https://ct.cloudflare.com/)


  * **Community**
  * [ ](https://x.com/cloudflare)
  * [ ](http://discord.cloudflare.com/)
  * [ ](https://www.youtube.com/cloudflare)
  * [ ](https://github.com/cloudflare/cloudflare-docs)


  * © 2025 Cloudflare, Inc.
  * [ Privacy Policy ](https://www.cloudflare.com/privacypolicy/)
  * [ Terms of Use ](https://www.cloudflare.com/website-terms/)
  * [ Report Security Issues ](https://www.cloudflare.com/disclosure/)
  * [ Trademark ](https://www.cloudflare.com/trademark/)
  * ![privacy options](https://developers.cloudflare.com/_astro/privacyoptions.BWXSiJOZ_22PXh4.svg) Cookie Settings


Back to top
