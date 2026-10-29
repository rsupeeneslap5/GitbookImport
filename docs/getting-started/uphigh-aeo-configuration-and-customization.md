---
description: >-
  This section describes the steps to take to activate SlapFive UpHigh to
  optimize how your company and products are included in AI bots like ChatGPT,
  Claude, and Gemini.
---

# UpHigh AEO Configuration and Customization

### Overview

UpHigh publishes approved customer evidence on a branded, publicly accessible microsite. It is designed to make customer stories easy for people to read and for search and answer-engine crawlers to discover. Publishing does not guarantee indexing, citations, or search rankings.

This guide covers custom-domain setup, sitemap discovery, branding, templates, and privacy integration. Your web/DNS team, SEO team, and privacy team should coordinate with SlapFive before launch.

### 1. Choose your microsite address

Recommended address:

```
https://customerstories.{your-domain}.com/customer-stories
```

Every SlapFive instance already has a required SlapFive subdomain, established during instance setup. Your UpHigh microsite uses that existing address:

```
https://{your-slapfive-subdomain}.slapfive.com/customer-stories
```

**A custom domain is optional, but strongly recommended for production use.** Publishing at an address such as `customerstories.your-domain.com` places your customer evidence on a domain your organization controls, making its connection to your brand explicit in the URLs that visitors, search engines, and answer engines encounter. Combined with links from your corporate website, consistent branding, and accurate structured metadata, this provides a clearer basis for identifying the content as an official, brand-published source rather than relying on a third-party hosting address alone.

This is a source-attribution and brand-trust recommendation—not a guarantee that crawlers assign a specific authenticity score, that the microsite automatically inherits the parent website's ranking signals, or that a custom domain increases rankings or AI citations. The custom domain is a branded address for your existing instance; it does not replace the required SlapFive subdomain.

A custom subdomain does not require moving your main website. DNS maps a hostname, not a URL path: do not put `https://` or `/customer-stories` in a CNAME record.

### 2. Create the DNS record

Ask your DNS administrator to create:

| Setting        | Value                                                |
| -------------- | ---------------------------------------------------- |
| Type           | CNAME                                                |
| Host / Name    | `customerstories`                                    |
| Target / Value | `app.slapfive.com`                                   |
| TTL            | Your provider's default, or 300 seconds during setup |

Some providers expect the full hostname, `customerstories.your-domain.com`, rather than just `customerstories`.

Equivalent DNS zone entry:

```dns
customerstories.your-domain.com. 300 IN CNAME app.slapfive.com.
```

Do not change the DNS for your apex domain or `www` website. Have your DNS administrator resolve any conflicting records at the new hostname. If you use DNS proxying, a corporate CDN, or restrictive certificate-authority authorization (CAA) policies, coordinate these with SlapFive before activation; they can affect routing, validation, and certificate issuance. Do not disable existing security controls to complete setup.

Send the full hostname to SlapFive after creating the record.

### 3. Activate the domain with SlapFive

The CNAME alone does not activate your microsite. SlapFive must associate the hostname with your account, configure UpHigh routing and its supporting assets/discovery endpoints, and provision a valid HTTPS certificate.

Before announcing the site, confirm with SlapFive that:

* DNS resolves correctly and HTTPS works without certificate warnings.
* The custom hostname shows your organization's content, not another account's content.
* The story index, a published story, images, and media load correctly.
* `/sitemap.xml`, `/robots.txt`, and `/llms.txt` are reachable on the custom hostname.
* The sitemap and page canonical tags use the agreed public hostname.

Agree on one primary public hostname before submitting URLs to search engines. Do not assume the SlapFive-hosted address automatically redirects to your custom hostname; confirm the intended behavior during activation.

### 4. Enable publishing and choose content

In your client workspace, open **Settings → UpHigh AEO** and enable UpHigh. Supply the brand description used in `llms.txt`.

Work with your SlapFive administrator to select the Stories approved for public use and enable their UpHigh publication. Account-level enablement does not replace individual content approval. Review customer consent, attribution, and usage permissions before publishing.

### 5. Connect the microsite to search discovery

#### Use the root sitemap URL

The UpHigh sitemap is served at the hostname root:

```
https://customerstories.example.com/sitemap.xml
```

It is **not** served at `/customer-stories/sitemap.xml`. UpHigh generates the sitemap from eligible published content; you do not need to maintain individual Story URLs manually.

#### Submit it directly

Have your SEO team verify ownership of the microsite in Google Search Console and submit its sitemap. A verified Domain property for `example.com` covers its subdomains; otherwise use the appropriate verified property for the microsite. Use the equivalent submission workflow for other search engines your organization supports.

UpHigh also advertises its sitemap in the microsite's own `/robots.txt` file.

#### Strongly recommended: include it in your corporate sitemap index

**Treat discovery from your established corporate website as a launch priority.** A new microsite may have few or no inbound links, so crawlers may not discover it promptly. Referencing the UpHigh sitemap from your corporate sitemap index provides an additional discovery route through your existing web presence. Do this alongside direct sitemap submission and a crawlable link from the corporate website; do not rely solely on the microsite advertising its own sitemap.

If your corporate sitemap, such as `https://www.example.com/sitemap.xml`, is a **sitemap index** with a `<sitemapindex>` root, have your SEO team add this entry while preserving all existing entries:

```xml
<sitemap>
  <loc>https://customerstories.example.com/sitemap.xml</loc>
</sitemap>
```

A sitemap index lists other sitemaps. An ordinary sitemap has a `<urlset>` root and lists web pages: do not add a `<sitemap>` element to it or list the XML sitemap as though it were a content page. If your CMS produces a `<urlset>`, submit the UpHigh sitemap separately or ask your SEO team to configure a proper sitemap index without removing existing coverage.

`www.example.com` and `customerstories.example.com` are different hosts. Google's sitemap-index rules require same-site hosting unless cross-site submission is configured. Have your SEO team confirm ownership verification and cross-site acceptance in Search Console rather than assuming a common parent domain is sufficient. Direct submission of the microsite's own sitemap is a straightforward alternative.

**Also strongly recommended:** add a normal, crawlable link from your corporate website to the customer-story index—for example, from your customer-success or resources section. This gives crawlers and visitors a direct path to the content, independent of sitemap processing. Sitemap references and links support discovery; neither guarantees crawling, indexing, or answer-engine inclusion.

### 6. Branding and visual customization

#### Design philosophy

**UpHigh is a branded customer-evidence publishing surface, not a general-purpose website builder. Its architecture prioritizes fast delivery, readable content, stable URLs, and search/answer-engine accessibility over elaborate visual effects.**

The public experience uses server-rendered SvelteKit pages: the initial HTML contains the content and structured metadata rather than requiring a browser to assemble the story after login. Shared components provide consistent story cards, navigation, media presentation, and responsive layouts. Public pages and assets use cache-friendly delivery rules; this is a performance-oriented design, not a guaranteed load-time or Core Web Vitals score. Media sizes, visitor networks, and added integrations still affect performance.

#### Current standard branding

Coordinate these account-level settings with SlapFive:

| Setting                    | Current effect on the public microsite           |
| -------------------------- | ------------------------------------------------ |
| Company name               | Attribution, page copy, and return-link label    |
| Logo image                 | Branded header                                   |
| Primary color              | Main brand color in the shared design system     |
| Secondary color            | Accent color in the shared design system         |
| Company website URL        | Destination of the “Back to” link                |
| Approved Stories and media | The customer evidence presented on the microsite |

Primary and secondary colors do not replace every color in the design system. Fonts, spacing, card geometry, navigation structure, footer design, and responsive behavior are controlled by the standard layouts. A font setting elsewhere in the SlapFive platform should not be assumed to change the public UpHigh microsite.

#### How the template system is organized

The **Settings → UpHigh AEO** area also contains a template/configuration system:

* **Templates** describe presentation using HTML with Handlebars placeholders, CSS, and default theme values. The editor also includes optional content-query and query-variable fields.
* **Global templates** provide shared starting points. An administrator can clone a global template to create a client-owned version rather than editing the shared original.
* **Configurations** select a template for a viewing mode, with an active flag, theme overrides, and content-filter settings. Defined modes include public Story, consensus, list, modal, and analytics views.
* The configuration resolver is designed to prefer an active client-specific configuration for a mode and fall back to a global configuration. The template theme resolver combines system defaults, template defaults, client branding, and configuration overrides, with configuration overrides taking final precedence.

**Current applicability:** the standard public `/customer-stories` pages use shared Svelte layouts and do not currently invoke this template/configuration renderer. Saving or activating a template is therefore **not a self-service way to replace the public microsite's layout**. Confirm the target surface and rendering support with SlapFive before commissioning or editing a template. The existence of an editor or stored setting does not mean that every public view applies it.

#### Setting expectations for custom design

Provide SlapFive with your brand guide, desired changes, reference screenshots, and accessibility requirements. SlapFive can assess the request and confirm what is configuration versus implementation work before committing to scope.

* **Standard configuration:** the active branding controls listed above.
* **Implementation review required:** custom fonts, new page sections, card/layout changes, corporate navigation/footer reproduction, custom CSS behavior, or a consent-management integration.
* **Not a standard microsite capability:** a drag-and-drop page builder, unrestricted third-party JavaScript, animation-heavy campaign pages, or a pixel-for-pixel reproduction of an arbitrary corporate website.

These are product-scope boundaries, not a claim that server-rendered sites cannot be visually rich. Custom work should preserve readable initial HTML, structured data, accessibility, tenant isolation, and an agreed performance budget. Third-party scripts require security and privacy review as well as visual testing.

### 7. Cookies, privacy, and compliance snippets

#### Does the public microsite need cookies?

Anonymous visitors do not need to sign in to read published UpHigh Stories. The reviewed public rendering code does not set authentication or advertising cookies or install a third-party analytics tag by default. This differs from the authenticated SlapFive application and other SlapFive products.

The UpHigh Customer Voice Portal does not use JavaScript-visible cookies or local-storage entries. SvelteKit may use session-storage entries for scroll position and page snapshots. Customer-added integrations and existing parent-domain cookies are addressed below.

#### Does it need a cookie-consent banner?

A site does not need an “accept cookies” prompt merely because it is a website or uses a custom domain. The relevant questions are what it stores or accesses on visitors' devices, for what purpose, and which laws and corporate policies apply.

Where consent is required for a non-essential storage/access or tracking technology, it must be obtained before that activity begins; a notice or “OK” button alone is not necessarily valid consent. Strictly necessary technologies can qualify for exemptions, subject to applicable conditions and transparency requirements. Exceptions differ by jurisdiction, and some have additional conditions. Your privacy/legal team should approve the final classification and implementation.

#### Cookie-free does not mean no personal-data processing

UpHigh's server-side visit/crawler logging can record IP address, user-agent, requested resource, Story identifier, and referrer. A browser banner does not automatically control that server-side processing. Review its purpose, lawful basis, retention, processor terms, and privacy disclosures with SlapFive and your privacy team.

Existing parent-domain cookies may also be sent to a custom subdomain, even when UpHigh did not create them. Added analytics, marketing scripts, external embeds, media providers, or a corporate consent manager can change the assessment. Test the final custom hostname in a clean browser, including media playback and repeat visits.

#### What to provide if your organization requires its own snippet

A corporate “cookie acknowledgement snippet” usually refers to a consent-management platform (CMP), such as OneTrust, Cookiebot, or TrustArc. It can be a corporate policy requirement even on a site without optional cookies.

Provide SlapFive with:

1. The provider, exact approved script/snippet, and environment/site identifier.
2. The hostname(s) that the CMP must recognize, and whether preferences should be shared across your corporate subdomains.
3. Your privacy/cookie policy URLs and required languages and regional behavior.
4. Which technologies/categories it must control, default consent state, and any opt-out/preference-signal requirements.
5. Required script order, network domains, and security-policy requirements.
6. A privacy/security contact and acceptance-test criteria, including reject, accept, preference changes, and withdrawal.

There is currently no verified public-UpHigh self-service field for installing an arbitrary CMP script. Do not assume that a template's HTML or a general platform “head tags” setting installs a working consent manager on these pages. This requires a scoped integration and validation. SlapFive should review the approved script and its permissions without weakening existing security controls.

Keep public Story content readable independently of optional tracking consent. If a CMP must gate server-side analytics, additional server-side integration is needed; a client-side banner by itself cannot prevent a log entry already generated when the page was requested.

### 8. Launch checklist

* [ ] Custom hostname and CNAME confirmed with SlapFive.
* [ ] Correct tenant mapping, UpHigh routing/assets, and HTTPS verified.
* [ ] Primary public hostname and canonical behavior agreed.
* [ ] Account publishing enabled; individual Stories approved for public use and publication.
* [ ] Logo, colors, company name, and return link reviewed on desktop and mobile.
* [ ] `/sitemap.xml`, `/robots.txt`, and `/llms.txt` accessible on the launch hostname.
* [ ] Sitemap submitted; any parent sitemap-index integration validated by the SEO team.
* [ ] Privacy disclosures and server-side logging reviewed.
* [ ] Any CMP integration scoped, approved, and tested before launch.
* [ ] Requested visual customization classified as configuration or implementation work.
