---
layout: default
title: script tag
parent:
  title: Tag Reference
  url: tag-reference.html
---

# script

Please make sure you have read the [Tag Syntax](tag-syntax) document and understand how tag attribute syntax works.

## Description

Provides an easy way for the developers to adopt CSP without having to think about nonce values explicitly. By using a `<s:script>` for JSP and `<@s.script>` for FreeMarker instead of `<script>` in their template files, developers will get the nonce attribute automatically added to their HTML elements when the template renders, if the [`CspInterceptor`](../core-developers/csp-interceptor.html) is enabled and a nonce value exists in the session object. Else `<s:script>` will operate like the `<script>` tag. The `s:script` tag includes all the regular HTML attributes associated with the `script` tag, if they are specified, and will add a nonce attribute. For example, in JSP the tag renders like this:
```
<s:script src="mysrc.js"...></s:script>
<script nonce="r4nd0m" src="mysrc.js">...</script>
```

## Attributes

{% remote_file_content https://raw.githubusercontent.com/apache/struts/master/core/src/site/resources/tags/script-attributes.html %}

## Examples

```jsp
<s:script src="mysrc.js">console.log("hello");</s:script>
```
