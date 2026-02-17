---
description: >-
  This section covers how to establish your Influitive Connection within
  SlapFive's Embedded Integration.
---

# Connect to Influitive

To protect the security and privacy of your Influitive data, SlapFive's Embedded Integration eliminates the need for you to email or message us with your authentication credentials. You or your Influitive Admin can simply connect to Influitive right from within SlapFive. You only have to do this once and it will be used for all Influitive data synchronization scenarios. The login data is encrypted and stored within the Embedded Integration.

1\. In SlapFive, go to the Admin menu, click **Settings**, and click on the **Integrations** sub-tab.

2\. Click the **Influitive Connection** box to expand it. Enter the following fields and click **Connect**.

* [ ] **Connection type:** Leave this set to **Cloud**.
* [ ] **Authentication type:** Select **Header auth**.
* [ ] **Header authorization:** Click the **Show** box to expand it and click the **Add Headers** button.
* [ ] **Key:** Where it says **Enter key**, type _Authorization_.
* [ ] **Value:** Type the word _Token_ followed by _space_, then copy and paste your **Authorization Token**. See the [Setting Up The Influitive API Integration](https://support.influitive.com/article/110-setting-up-the-influitive-api-integration) page in the Influitive documentation for instructions on how to get your Authorization Token.&#x20;
* [ ] Click the **+ Add headers** button to add another blank row to the table.
* [ ] **Key:** Where it says Enter key, type _X\_ORG\_ID_.
* [ ] **Value:** Copy and past your **X\_ORG\_ID** following the instructions in the Influitive doc linked above.

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 132251.png" alt=""><figcaption><p>Connect to Influitive Screen</p></figcaption></figure>

* [ ] **Base URL:** Leave this field blank.
* [ ] **Use custom TLS/SSL certificate settings:** Leave this set to No.

Once you are successfully connected, the button should now say **Disconnect**, and you should see a green <mark style="color:green;">**Connection success**</mark> message.
