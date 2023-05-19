In web applications, you need to display a one-time notification message (also known as “flash message”)

For this, Django provides full support for cookie- and session-based messaging, for both anonymous and authenticated users.
Every message is tagged with a specific `level` that determines its priority (e.g., `info`, `warning`, or `error`).

>The default `settings.py` created by `django-admin startproject` already contains all the settings required to enable message functionality:
>
>If you don’t want to use messages, you can remove `'django.contrib.messages'` from your [`INSTALLED_APPS`](https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-INSTALLED_APPS), the `MessageMiddleware` line from [`MIDDLEWARE`](https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-MIDDLEWARE), and the `messages` context processor from [`TEMPLATES`](https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-TEMPLATES).

![[Pasted image 20230505193954.png]]

![[Pasted image 20230505194143.png]]

![[Pasted image 20230505194227.png]]

If you’re using the context processor, your template should be rendered with a `RequestContext`. Otherwise, ensure `messages` is available to the template context.

Even if you know there is only one message, you should still iterate over the `messages` sequence, because otherwise the message storage will not be cleared for the next request.

![[Pasted image 20230505194651.png]]

![[Pasted image 20230505194706.png]]

![[Pasted image 20230505194723.png]]
