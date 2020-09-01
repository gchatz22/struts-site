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

Provides an easy way for the developers to adopt CSP without having to think about nonce values explicitly. By using a `<s:link>` for JSP and `<@s.link>` for FreeMarker instead of `<link>` in their template files, developers will get the nonce attribute automatically added to their HTML elements when the template renders, if the [`CspInterceptor`](../core-developers/csp-interceptor.html) is enabled and a nonce value exists in the session object; Else `<s:link>` will operate like the `<link>` tag. The `s:link` tag includes all the regular HTML attributes associated with the `link` tag, if they are specified, and will add a nonce attribute. For example, in JSP it renders from this:
```
<s:link href="print.css" rel="stylesheet">
```
to this
```
<link nonce="r4nd0m" href="print.css" rel="stylesheet">
```

## Attributes

{% remote_file_content https://raw.githubusercontent.com/apache/struts/master/core/src/site/resources/tags/link-attributes.html %}

## Examples

```jsp
<s:link href="print.css" rel="stylesheet">
```
