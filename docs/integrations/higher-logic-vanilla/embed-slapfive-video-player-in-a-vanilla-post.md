---
description: >-
  This section covers how to embed a SlapFive video into a post in your Higher
  Logic Vanilla community.
---

# Embed SlapFive video player in a Vanilla post

1. In Vanilla Settings, grant permission to Vanilla to access the SlapFive domain by going to **Technical > Security**, and in the **Trusted Domains** box, copy and paste this string:

&#x20;                  \*.slapfive.com

2. In SlapFive, edit the Story that contains the video you want to embed, and from inside the Direct Link to Media field, copy the full URL of the mp4 file.

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-13 142223.png" alt=""><figcaption><p>Copy the full URL for the mp4 file.</p></figcaption></figure>

3. Substitute the copied video URL for the sample URL in this iframe code. Adjust the width, height, and other properties as needed to render the way you want in Vanilla:

{% hint style="info" %}
\<iframe width="100%" height="100%" src="https://media.slapfive.com/cm05qaa9k007c3bah23q6hqda.mp4" title="SlapFive" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen>\</iframe>
{% endhint %}

4. In the Vanilla post, click the Insert Media button, then paste the iframe code into the URL field and click Insert.

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-13 143037.png" alt=""><figcaption><p>Use Insert Media to embed the iframe into the post.</p></figcaption></figure>
