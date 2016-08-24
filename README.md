django-crowd
============
Simple Atlasian CROWD authentication backend for Django with SSO support



Configuration:
==============
Put a CROWD configuration in your `settings.py`:

```
CROWD = {
    'url': 'http://your.crowd.url:port/crowd/rest',         # your CROWD rest API url
    'app_name': 'your-registered-crowd-application-name',   # appname, registered with CROWD
    'password': 'application-password',                     # correct password for provided appname
    'superuser': True,                                      # if set makes CROWD-authorized users superusers;
    'staffuser': True,                                      # BE CAREFUL WITH THIS PARAMETER!
    'validation':'10.11.40.34',                             # The ipaddress the Crowd server is responding to
    'sso': False,
}
```

Add `crowd.CrowdBackend` in your `AUTHENTICATION_BACKENDS` settings list.
Put it first so that password are only kept in CROWD:

```
AUTHENTICATION_BACKENDS = (
    'crowd.backends.CrowdBackend'
    'django.contrib.auth.backends.ModelBackend',
)
```


Add     'crowd.middleware.CookieMiddleware' to the Middleware 


AUTHENTICATION_BACKENDS list to make sure you always start with crowd authentication before falling over to
a local account.



**NEW for version 0.50**

Added import_users_from_email_list that takes a array of emails and returns an array of usernames that collate to those emails, and an array of not found emails
```
from crowd.backends import import_users_from_email_list

        added, not_found = import_users_from_email_list(users)
```

Credits:
========

Originally written for Django v1.3 by Konstantin J. Volkov <konstantin-j-volkov@yandex.ru> at 12.07.2012

Refactored, put together and tested with Django v1.4 by Grigoriy Beziuk <gbezyuk@gmail.com> at 27.08.2012

Refactored and added SSO by Tobias Carlander <tobias.carlander@wfp.org>
