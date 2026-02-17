---
description: >-
  A powerful way to put customer content to work is to embed it on any web,
  mobile or social property. This section gives you some ideas for where and why
  to embed and how to do it.
---

# Embed customer voice on your website or landing page

SlapFive makes this super simple to embed Boards as widgets on your corporate website, campaign landing pages, microsites, blog posts, and social campaigns. You can embed a single Story or a set of related Stories anywhere on your web page. To simplify the display of Stories, SlapFive uses Boards as the container for the one or more Stories, and the Board is then embedded as a widget at your desired location. Here’s how to do it.

### Ideas for where and why to embed stories

1. Rather than in impersonal "logo scroller", put a tray of customers on your homepage to show the types of companies that work with you. Example: [**SlapFive.com**](https://www.slapfive.com/) – scroll down to the “Join the SlapFive Rockstar Family” section.
2. In your Customers section, show a page for each customer, with a spokesperson answering multiple questions. Examples: [**Amplix.com**](https://amplix.com/success-story/bjs-wholesale-club-consolidates-wan-carriers-and-reduces-cost-of-circuits-with-amplix/)**,** [**LoganData.com**](https://logandata.com/kronos/) - The body of these pages is a SlapFive widget.
3. Let customers tell their story on your “Why Us?” page. Example: [**LexiaLearning.com**](https://www.lexialearning.com/why-lexia/) – scroll down to the “Why do you value working with Lexia?” section.
4. Have customers explain why they replaced specific competitors. Example: [**Acumatica.com**](https://www.acumatica.com/acumatica-to-replace-microsoft-dynamics/) - "Hear why people just like you chose Acumatica over Microsoft Dynamics" page.
5. Prove your industry expertise by profiling customers you have in each industry. Example: [**Acutmatica.com**](https://www.acumatica.com/manufacturers-rely-on-acumatica-for-their-success/) - "Manufacturing companies rely on Acumatica for their success" page.
6. Add a page where customers give advice to your prospects to get them in the right mindset for your solution. Example: [**BuyerPersona.com**](https://www.buyerpersona.com/advice-from-your-peers) – Advice from your Peers page.
7. Feature customers in a blog post series. Example: [**Acumatica.com**](https://www.acumatica.com/blog/auto-action-technologies/) – scroll down to the sliding tray with Jared Cohen's stories.
8. Promote customer events by hearing from award winners. Example: [**ITSMA**](https://www.itsma.com/marketing-excellence-award-winning-lessons-from-marketing-leaders/) - scroll down to the "Hear the excitement from some of our MEA winners" section.

### How to do it

1. Make a SlapFive Board that contains the Story(ies) that you want to show. This board should use a template that is designed for being inserted as a widget.
2. Within your web content management (WCM), blog, or landing page editor, go to the location you want to insert the SlapFive Board, and copy and paste the following code snippet:\
   \
   `<div id="board_1"></div>`\
   `<script type="text/javascript" src="//pym.nprapps.org/pym.v1.min.js"></script><script> var pymParent = new pym.Parent('board_1', 'INSERT_URL_HERE', {allowfullscreen: true}); </script>`<br>
3. Where you see the text _INSERT\_URL\_HERE_ in the pasted code snippet, substitute the URL of the Board you want to embed within the single quotation marks. You can find the URL by previewing the Board and copying the address bar contents, or by clicking the Copy URL button next to the Board on the Boards tab in SlapFive.
4. Go to the web page where you pasted the code and make sure the widget displays properly. If not, make sure that when the code was pasted, you ended up with straight quotation marks, not curly quotation marks, or your browser may not like you. You may also need to adjust the size of the page element so that the widget displays properly.
5. If you want to embed more than one board on the same page, for the second board, replace “board\_1” with “board\_2” in both places it appears. Increase the number for each additional board you embed.

{% hint style="info" %}
TEST IT OUT WITH ONE OF OUR URLS: \
`<div id="board_1"></div>`\
`<script type="text/javascript" src="//pym.nprapps.org/pym.v1.min.js"></script><script> var pymParent = new pym.Parent('board_1', 'https://slapfive.slapfive.com/b/cjpyinqpm00l40111j6jt005v/Why_SlapFive_is_a_must_have_widget', {allowfullscreen: true}); </script>`
{% endhint %}
