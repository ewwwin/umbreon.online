---
permalink: /fastmail-site-hosting
title: A Minimal Konsole Tab Bar Stylesheet
style: |
    .silly { margin-block: 2rem; }
    .silly :is(h1, h2, h3, h4, h5, h6) {
        margin: 0;
        text-align: justify;
        text-align-last: justify;
    }
---

<div class="silly" markdown=1>

# Have you ever wanted to host a site
## but didn't want it on a personally identifiable IP
### and already been a Fastmail customer using their web file hosting
#### but needed a refresher on how best to sync your changes programmatically when you rebuild your site
##### and how to set up DNS for the new domain without fucking up and wasting 30 minutes for them to pull your fixed records
###### because you want to have an apex domain be the canonical URL but the docs say to CNAME to their servers and you can't CNAME an apex domain and besides enabling HTTPS gives all sorts of errors that way

</div>

Fastmail websites live in the "Files" section of the Fastmail web UI. You create
a website on a domain and point it at a folder and it hosts the static contents
of that folder on that domain. Easy right?

[Fastmail files also supports WebDAV][fastmail-webdav], so [the answer to
syncing changes to your site is `rclone`][webdav-rclone]. run this once to
configure a remote into your files:

<pre><code>rclone config create fastmail webdav \
    url https://myfiles.fastmail.com \
    vendor other \
    user 'whoever@fastmail.com' \
    password '<a href="https://app.fastmail.com/settings/security/apps">yourAppPassword</a>'</code></pre>

then to sync your local changes into Fastmail:

```
rclone sync /path/to/your/site fastmail:path/to/your/website/folder
```

(this process should be similar for any other static hosting provider that lets
you interface with the site's contents via WebDAV. it's kind of neat!)

as far as DNS goes, [the DNS help center article][fastmail-terrible-dns-help]
says you should just CNAME your domain to `web.fastmail.com` or
`web.messagingengine.com`, but if you want an apex domain you can't CNAME
anything. instead you want to look a little deeper and check what DNS records
Fastmail would be serving for your domain if you were using them as your hosting
provider. you can check this in settings > domains > edit a domain > customize
DNS. you'll see that they don't CNAME shit, they just have A records pointing at
their hosting servers `103.168.172.37` and `103.168.172.52`. so you can create
your own A records on your apex domain pointing at those servers and it'll Just
Work.

if you also want to redirect the `www` subdomain back to your apex domain, (and
you should, because people *will* type it anyway,) you'll want to CNAME that
subdomain to your apex domain so Fastmail will be serving both domains, and then
set up a second website in Fastmail for the `www` subdomain and just set it to
redirect to your canonical URL.

and just as a note: setting a low TTL on your DNS records will not save you from
having to wait a long time for Fastmail to re-fetch your records if you fuck up
the first time and have to change them. even with a TTL of 30s, i still waited
at least half an hour before the new records took effect, and the "re-check DNS"
button in domain settings doesn't seem to refresh its view of non-mail records
so there's literally nothing you can do about it.

god i love computers.

[fastmail-webdav]: https://www.fastmail.help/hc/en-us/articles/1500000277882-Remote-file-access
[webdav-rclone]: https://superuser.com/a/1338299
[fastmail-terrible-dns-help]: https://www.fastmail.help/hc/en-us/articles/360060591153-Manual-DNS-configuration
