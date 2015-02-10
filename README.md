# mezzanine-domains
This is an example project of multi-site support with different templates (each site) on Mezzanine (a CMS for Django)

Apparently Mezzanine has a functionality for this[0], but after a lot of trying and several google searches I ended up frustrated.
 
Based on a post I found[1], a guy suggested an aproach with django-domains.

So here you have a basic example with 2 sites (sitio1, sitio2 ) and each can manage it's own domain

[0] http://mezzanine.jupo.org/docs/multi-tenancy.html#per-site-themes
[1] https://groups.google.com/forum/#!msg/mezzanine-users/ZGVPCh087Nc/v_GnbU2iBfAJ
[2] https://pypi.python.org/pypi/django-domains

Requirements:
    Mezzanine
    django-domains

For the uploaded sqlite3 db example use:
user: admin@admin.admin
password: admin

Sites:   sitio1.localhost
         sitio2.localhost

Edit your /etc/hosts and add this lines:
127.0.0.1   sitio1.localhost
127.0.0.1   sitio2.localhost

If you want this in your mezzanine project:

Configure your settings.py:

MIDDLEWARE_CLASSES += (
    'domains.middleware.RequestMiddleware',
    'domains.middleware.DynamicSiteMiddleware',
)

Prepend to TEMPLATE_LOADERS the domains loaders like this:
TEMPLATE_LOADERS = (
    'domains.loaders.filesystem.Loader',
    'domains.loaders.app_directories.Loader',
    # another loaders
)


Create a template directory inside your project root folder.
For each domain you want sepparated templates create a domainname.tld folder[3]

In the example:

templates
├── sitio1.localhost
└── sitio2.localhost

Create your templates inside each folder and enjoy!


[3] tld stands for http://en.wikipedia.org/wiki/Top-level_domain
