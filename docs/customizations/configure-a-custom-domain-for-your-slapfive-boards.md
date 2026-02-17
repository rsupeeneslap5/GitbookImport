---
description: >-
  By default, the URL of SlapFive Boards begins with
  https://your_company.slapfive.com. This section shows you how to have the URLs
  begin with a custom domain.
---

# Configure a custom domain for your SlapFive Boards

By configuring a custom domain, you can make viewers of SlapFive Boards feel like they are on one of your own branded web properties. Instead of having the URL of your Boards begin with _your\_company.slapfive.com_, they will begin with _your\_subdomain.your\_company.com_.

The way you set up a custom domain is by creating a subdomain of your company’s domain. The first thing you need to do is to decide on that subdomain, for example:

&#x20;                _voice.your\_company.com_\
&#x20;                _customers.your\_company.com._

Once you've decided on a subdomain, follow these steps.

1. Have your IT department create the new subdomain using the following fields:\
   \
   &#x20;           **Type**: _CNAME_ \
   &#x20;           **Name**: _your\_subdomain.your\_company.com_\
   &#x20;           **Value**: _app.slapfive.com_\
   &#x20;   &#x20;
2. If your domain has a CAA record to allow Certificate Authorities to issue certificates, you will need to add a CAA record to the subdomain as follows. This enables SlapFive to create and maintain the SSL certificate.\
   \
   &#x20;           _prefix.your\_company.com. 32 IN CAA 0 issue “letsencrypt.org”_<br>
3. Let SlapFive know that your CNAME record has been created. We will create the SSL certificate and activate your subdomain in the SlapFive domain management console, then let you know when it is set up.

{% hint style="info" %}
TEST IT OUT: Go to the Boards tab and open a Board, make sure the Address shows your custom domain and that you don’t get any security warnings. Copy a Board URL and make sure you see your custom domain.
{% endhint %}
