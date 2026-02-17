---
description: >-
  By default, SlapFive notification and prompt emails are sent from
  admin@slapfive.com. This section shows you how to have them sent from your
  users' email addresses.
---

# Send emails from your own domain and email addresses

When SlapFive sends email invitations and notifications for things such as sending prompts, sharing boards, or new requests, you want them to be sent from the email addresses of your own employees, so that the recipients are more likely to recognize the sender and open the emails.

To avoid these emails from being blocked by anti-spoofing services like Mimecast, your email administrator needs to follow these steps to set up a Custom Email Sending Domain.

1. Log into SlapFive and go to **Admin menu** > **Your\_Company Settings** and click the **Advanced Settings** tab.
2. Scroll down to the **Custom Email Sending Domain** field as shown below in Screen 1, enter _s5sender.your\_company.com,_ substituting your company's primary domain for _your\_company_. This subdomain is not visible to anyone and is used only for DNS configuration. Click the **Create Custom Domain** button and click **Save**.&#x20;
3. Go back to **Admin menu** > **Your\_Company Settings.** Under **Custom Email Sending Domain** section, you will now see two new **DNS TXT Records** that need to be added for your domain. Copy and paste the **Host Name** and **Enter This Value** strings, and give to your Email/DNS administrator to add these records.&#x20;
4. Go back to **Admin menu** > **Your\_Company Settings.** In **Custom Email Sending Domain** section, press the **Verify SPF/DKIM** button. You should see the red X’s replaced by green check marks for both TXT records, indicating they are set up correctly, and SlapFive will start sending emails from your email addresses. If you don’t get green checkboxes, then you should verify that you’ve set your TXT records up correctly.

![Step 2](<../.gitbook/assets/Screenshot 2022-05-16 172058 (1).png>)

![Steps 3 and 5](<../.gitbook/assets/Screenshot 2022-05-16 171342.png>)

{% hint style="info" %}
TEST IT OUT: Send a Prompt or Board to a colleague or to a different email address of your own, and make sure that the sending information on the emails looks just like it does if you had sent it from your own email client.
{% endhint %}

Some email servers also require there to be a DNS record for the new subdomain. Have your Email/DNS administrator create a third DNS record using these fields, substituting your company's primary domain for _your\_company_:\
&#x20;           **Type**: _CNAME_ \
&#x20;           **Name**: _s5sender.your\_company.com_\
&#x20;           **Value**: _mailgun.org_
