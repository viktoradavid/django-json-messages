# django-json-messages
Add json encoded messages (from Django messages framework) to templates

Updated for python3.9 and Django3.2

# Install

```sh
  pip install django-json-messages
```

# Usage

## Django messages

Make sure the [Django messages framework](https://docs.djangoproject.com/en/1.7/ref/contrib/messages/) is installed and working.

## App

Add `json_messages` to your list of `INSTALLED_APPS`

## Context processor

Add `json_messages.context_processors.json_messages` in your `CONTEXT_PROCESSORS` settings.

A `json_messages` property is now available on the context.

It is a dict version of the messages with `msg` and `type` keys

## Template tags

### Loading

Use `{% load json_messages %}` at the top of your template

### Json dump

Use `{% json_messages_dump %}` to simply dump the json encoded messages into your template

**Note** that all messages' `msg` properties are passed through Django's [escapejs](https://docs.djangoproject.com/en/dev/ref/templates/builtins/#escapejs) for security reasons.

### Script

Use `{% json_messages_script %}` to dump the messages array into a Javascript window variable called ` messages `

This is equivalent to writing

```
<script type="text/javascript">
	window.messages = {% json_messages_dump %};
</script>
```

#### Configuration

- Set a context variable `js_variable` to override the name of the window variable use by `{% json_messages_script %}`  
*Example:* 
```
  {% json_messages_script js_variable="blop" %}
``` 
results in
```
<script type="text/javascript">
	window.blop = [{"type":"danger", "msg":"Something"}];
</script>
```
Defaults to *"messages"*


## Package dependencies

None


