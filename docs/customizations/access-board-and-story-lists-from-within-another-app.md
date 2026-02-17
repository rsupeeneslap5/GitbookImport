---
description: >-
  A powerful way to give others in your company access to Boards and Stories is
  to embed the list within the apps they use everyday. This section gives you
  some ideas and explains how to do it.
---

# Access Board and Story lists from within another app

You’ve assembled these powerful storyboards, now you want to make them easily available to your sales reps, customer success managers, marketing team and other employees without having them log into SlapFive. You can to embed the SlapFive Story Finder and Board Finder right within other apps.

{% hint style="info" %}
Note: These lists are already embedded in Salesforce as part of the SlapFive Salesforce App, using this same method.
{% endhint %}

### Ideas for where to embed

* To serve up sales tools like Objection Crushers and Recorded References, embed the Story and Board Finders right within Salesforce.com or the sales portal you use to give access to all your sales enablement tools.
* To give Customer Success Managers access to best practices and advice from other customers, so they can share with their customers, embed the Story and Board Finders right within your Customer Success platform such as Gainsight or Totango, or within your intranet site.

### How to do it

To embed Story Finder or Board Finder into any application, simply create a page in that app using whatever mechanism it provides for embedding third-party screens. For example, in Salesforce.com, you can do this with an Visualforce Pages or S-Controls. Other apps may use widgets. Here’s how to do it.

1. Determine the location where you want to embed Stories and Boards, and create the appropriate container object for that application.
2. Use one or both of these URLs substituting the name of your SlapFive instance where it says _your\_instance\_name_:\
   \
   &#x20;        https://your\_instance\_name.slapfive.com/client/stories/embed\
   &#x20;        https://your\_instance\_name.slapfive.com/client/boards/embed
3. To enable tracking of the sharing of these boards, you should set up Single Sign-On with SlapFive, which allows SlapFive to know which users have shared a story or a board. Let us know if you want to do this.

{% hint style="info" %}
TEST IT OUT: Go into the app and make sure you see the list of the embedded object.
{% endhint %}
