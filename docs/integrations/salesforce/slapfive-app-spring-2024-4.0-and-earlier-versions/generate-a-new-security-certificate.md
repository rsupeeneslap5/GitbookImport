# Generate a New Security Certificate

The security certificate that you download from the Identity Provider and sent to SlapFive when you first set up the Salesforce App typically expires every 12 months. If your certificate has expired, or doesn't match the one SlapFive has uploaded to our authentication server, you must generate a new certificate and send it to SlapFive so we can update your authentication configuration, then update the SlapFive Connected App to use the new certificate.

### Generate the new certificate

* [ ] Go to **Setup** > **Security** > **Certificate and Key Management**.
* [ ] Click the **Create a Self-Signed Certificate** button.
* [ ] Name it: _SelfSignedCert\_today’sDate\_SlapFive_ where you substitute today’s date in any readable format for _today'sDate_, and click **Save**.
* [ ] Click to download it and email it to your SlapFive contact or drop it into the shared folder provided by your SlapFive contact.

### Update the SlapFive Connected App to use the new certificate

* [ ] Go to **Setup > Apps > Connected Apps > Manage Connected Apps**.
* [ ] In the list of Connected Apps, click the **Edit** link next to **SlapFive Connected App**.
* [ ] In the **Idp Certificate** field, click the drop-down and select the Self-Signed Certificate you just generated.
* [ ] Click **Save**.
