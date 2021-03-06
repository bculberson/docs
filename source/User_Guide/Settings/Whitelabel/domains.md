---
layout: page
weight: 0
title: Domains
seo:
  title: Whitelabel Domains
  description: Whitelabeling domains allows you to use your domain's reputation when sending.
  keywords: whitelabeling, domain Whitelabeling
navigation:
  show: true
---

<iframe src="https://player.vimeo.com/video/149585179" width="500" height="281" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

{% info %}
When in doubt, contact your DNS registrar or web hosting service’s technical support department. All information in this document complies with the DNS standards, but some registrars and web hosting providers handle things differently.
{% endinfo %}

SendGrid’s domain whitelabel allows you to whitelabel your domain and get rid of the “via sendgrid.net” message on your emails, even if you don’t have a dedicated IP address with SendGrid. You can start to build your domain’s email reputation and explicitly show all your recipients that you actually sent these emails. This should help increase your deliverability and reduce your potential for spam reports.

{% info %}
Marketing Campaigns [Sender Identities]({{root_url}}/User_Guide/Marketing_Campaigns/senders.html) that use the same domain as your domain whitelabel will automatically verify.
{% endinfo %}

Whitelabeling is critical to your email reputation and there are a couple things you should know:

1. You can only have one active and verified whitelabel per root domain. example.com is a root domain, where em.example.com is a subdomain.
2. You will actually whitelabel a subdomain of your root domain.
3. Your email reputation will be based on your root domain, regardless of the subdomain you use or if you switch subdomains.
4. You can only have 1 default subdomain, which will be the fallback domain for your domain whitelabeling.
5. Whether you use the automated or manual method, you will have to add DNS entries at least once.
6. Subusers can only access their own whitelabels.They cannot access the parent whitelabels or other subuser whitelabels.
7. Once you have everything set up, you will need to verify the whitelabel with SendGrid.

We provide all the information about every step of the process below, so that you can set up your whitelabel quickly and easily.

{% anchor h2 %}
Domain Whitelabel Settings
{% endanchor %}

{% anchor h3 %}
On Behalf Of User
{% endanchor %}

This setting lets you assign a whitelabel to a subuser account or the account you are currently using. A subuser can set up their own whitelabel, of course. However, if the parent account assigns a whitelabel to a subuser, that subuser will not be able to edit or modify the settings of the assigned whitelabel.

{% anchor h3 %}
Subdomain
{% endanchor %}

This is the “prefix” of the domain that you are actually whitelabeling. Historically, we have suggested prefixes like “em,” “em1,” etc. However, you can use whatever subdomain you would like to use.

We do not suggest that you use “mail” as the subdomain, because this is a subdomain that many registrars or hosting companies will automatically set up for your personal email usage. This can cause conflicts and affect your email reputation.

{% warning %}
The domain whitelabel subdomain MUST be different from your email link whitelabel subdomain because you will need different CNAME DNS entries for each type of whitelabel and DNS does not allow multiple CNAMEs for each subdomain.
{% endwarning %}

Even though your domain whitelabel and email link whitelabel are different subdomains, the reputation of your root domain and your IP are what recipient servers and spam filters look at to determine whether your email is delivered.

{% anchor h3 %}
Domain
{% endanchor %}

{% warning %}
If you add a new default domain whitelabel for a domain that is already whitelabeled on your account, you risk invalidating and removing the default status of the previously set up whitelabel.
{% endwarning %}

{% info %}
Your domain whitelabel will not affect your email link whitelabel and vice versa.
{% endinfo %}

The domain is the root domain for your subdomain. This is the domain that will receive the email reputation from the whitelabel.  Your root domain should match your FROM email address. If you are sending from newsletter@example.com, then you should whitelabel subdomain.example.com so the root domains match.

{% anchor h3 %}
Use new Domain
{% endanchor %}

Allows you to add a new domain to your whitelabel options.

{% anchor h3 %}
Default Whitelabel
{% endanchor %}

{% info %}
There can be only one!
{% endinfo %}

Your default whitelabel is your fallback when you send emails. It will be used for all sending on your account, unless you have multiple valid whitelabels and one of them matches your FROM email domain. If there is no valid whitelabel match to your FROM email domain, then your whitelabel will fall back to your default domain whitelabel. For more information see the [Whitelabel Application Logic]({{root_url}}/User_Guide/Settings/Whitelabel/index.html#-Whitelabel-Application-Logic).

{% anchor h3 %}
Automated security
{% endanchor %}

{% info %}
This is the “set it once and forget it” option. You must turn this on for each subdomain you whitelabel.
{% endinfo %}

{% warning %}
If you are not allowed to have underscores in your CNAME records, you will not be able to use this feature. We will still provide the DNS records you will need.
{% endwarning %}

Instead of managing your DNS records for every single change you make, like adding an IP address, SendGrid can manage your SPF and DKIM record updates for you. This option will change the DNS records that you point at SendGrid for your domain, allowing the responsibility of updating the records to pass through to SendGrid. This means that DKIM and SPF records will all be handled by SendGrid once this whitelabel is verified.

Setting up two custom DKIM keys allows SendGrid to rotate these two keys periodically without requiring the customer to make additional changes/updates to their DNS. Rotating DKIM means that we will rotate between the two DKIMs. SendGrid will also generate a custom SPF that includes only the IPs the customer is sending from (as opposed to ~ all sendgrid.net). SendGrid will generate these records but the customer MUST enter the CNAME records into their DNS host.

If you choose not to have SendGrid manage your DNS records, then you’ll be shown all of the manual DNS records that you need to enter at your registrar or host. You will be responsible for making any updates to your DNS for any changes on your account. The records you are given will be MX, DKIM, and SPF records to enter at your registrar, hosting company, or DNS manager. This will also mean that your SPF record will include all of SendGrid's IP addresses.

{% anchor h3 %}
Creating a Domain Whitelabel
{% endanchor %}

When you enter the information for your whitelabel and click “Save,” SendGrid will update its own internal DNS to prepare for your whitelabel settings. This process may take up to 20 seconds.

We will then give you the DNS entries that you need to make to match the settings you provided. The DNS records you receive will depend on whether you chose automated or manual security, the IP addresses on your account, and the domain you are whitelabeling.

{% anchor h3 %}
Validate Your Domain Whitelabel
{% endanchor %}

{% warning %}
SendGrid will not start using your  whitelabels until they are validated! Until they are validated, you may see “via sendgrid.net” on your emails.
{% endwarning %}

Once you have made the DNS changes, you need to validate your whitelabel:

1. Return to domain whitelabels
2. Click the whitelabel you just added (or the gear icon to the right of the whitelabel)
3. Click “Validate”


If everything is set up properly and the DNS records have propagated, then SendGrid will verify your whitelabel and email sending will use this whitelabel following the Whitelabel Application Logic.

{% anchor h2 %}
Changing or Replacing a Whitelabel Domain
{% endanchor %}

{% anchor h3 %}
Examples Of Why You Might Change Or Replace A Domain Whitelabel
{% endanchor %}

1. If you were a Sendgrid customer before May 27th, 2015 and you want to update to the new whitelabel system
2. You want to change your domain whitelabel
3. [You add IP addresses to your SendGrid account]({{root_url}}/Classroom/Basics/Account/adding_an_additional_dedicated_ip_to_your_account.html)

The steps for changing or replacing a whitelabel are easy!

1. Follow the steps to create a new whitelabel
2. Verify your whitelabel

That’s it! Easy!

{% anchor h2 %}
Managing and Viewing Your Domain Whitelabel
{% endanchor %}

If you need to check the status of a whitelabel, you can see the “at a glance” information from the Domains Whitelabel page. However, if you’re looking for more in-depth information or you need to find the DNS settings for your whitelabel then just click the gear icon next to the whitelabel and select “View.”

From this page, you’ll be able to see all of the settings you entered when setting up your whitelabel, whether the whitelabel is valid, and all of the DNS settings you need for this whitelabel.

{% anchor h3 %}
Adding An IP To Your Account
{% endanchor %}

When you add an IP address to your SendGrid account and you have automated security turned on, SendGrid will add your IPs to your SPF record automatically. When you get to 10 IPs, we will use SendGrid.net ~all due to the character limitation of SPF records. At that point, it may make sense to manually control your DNS records and chain the SPF records as well.

If you have automatic DNS security turned off, you will need to manually add your IPs to your SPF records each time you purchase a new IP address.

{% anchor h2 %}
Deleting a Domain Whitelabel
{% endanchor %}

{% info %}
Deleting a domain whitelabel is permanent and can not be rolled back.
{% endinfo %}

When you view your detailed whitelabel information, you will notice at the bottom of the page that you can delete this whitelabel. If you click the button and then confirm that you are sure you want to delete this whitelabel, then SendGrid will delete it.

{% info %}
You can NOT delete the default domain whitelabel. You must replace it if you want it to change.
{% endinfo %}

Once deleted, the internal SendGrid DNS entries will be deleted and any email you send will fall back to the appropriate whitelabel settings according the [Whitelabel Application Logic]({{root_url}}/User_Guide/Settings/Whitelabel/index.html#-Whitelabel-Application-Logic).

{% anchor h2 %}
Using the API
{% endanchor %}

[Manage your domain whitelabel via our v3 API]({{root_url}}/API_Reference/Web_API_v3/Whitelabel/domains.html)
