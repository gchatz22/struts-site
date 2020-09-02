---
layout: default
title: link tag
parent:
  title: Tag Reference
  url: tag-reference.html
---

# link

Please make sure you have read the [Tag Syntax](tag-syntax) document and understand how tag attribute syntax works.

## Description

Provides an easy way for developers to adopt CSP without having to propagate nonces explicitly. By using a `<s:link>` for JSP and `<@s.link>` for FreeMarker instead of regular `<link>` in their template files, developers will get the nonce attribute automatically added to their HTML elements when the template renders, if the [`CspInterceptor`](../core-developers/csp-interceptor.html) is enabled and a nonce value exists in the session object. Otherwise, `<s:link>` will operate just like the `<link>` tag. The `s:link` tag includes all the regular HTML attributes associated with the `link` tag, if they are specified, and will add a nonce attribute. For example, in JSP the tag renders like this:
```
<s:link href="print.css" rel="stylesheet">
<link nonce="r4nd0m" href="print.css" rel="stylesheet">
```

## Attributes

{% remote_file_content https://raw.githubusercontent.com/apache/struts/master/core/src/site/resources/tags/link-attributes.html %}

## Examples

```jsp
<s:link href="print.css" rel="stylesheet">
```
