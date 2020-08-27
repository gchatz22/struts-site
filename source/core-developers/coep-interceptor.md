---
layout: default
title: COEP Interceptor
parent:
    title: Interceptors
    url: interceptors.html
---

# Fetch Metadata Interceptor

## Description

Interceptor that implements Cross-Origin Embedder Policy on incoming requests.

COEP prevents a document from loading any non-same-origin resources which don't explicitly grant the document permission to be loaded. This permission can be given via CORP (with a `Cross-Origin-Resource-Policy` header with a value which includes the requester, e.g `same-site`, or `cross-origin` for public resources)  or with CORS (by responding with appropriate `Access-Control-Allow-*` headers for requests in CORS mode).  The only allowed value for COEP is `require-corp`.
COEP prevents the document from loading any framed documents which don’t opt-in by setting the COEP header. (`Cross-Origin-Embedder-Policy: require-corp`). This provides protection for documents that don’t restrict framing. A document that doesn’t set COEP cannot be framed by another document with COEP. All descendents of a document with COEP will also enforce the same restrictions.

COEP is now supported by all major browsers.



[More information about COEP](https://web.dev/why-coop-coep/#coep).

## Parameters

- `exemptedPaths` - Set of opt out endpoints that are meant to serve cross-site traffic
- `enforcingMode` - Boolean variable allowing the user to let COEP operate in `enforcing`, which blocks both resource and reports violation, or `report-only` mode, which only reports violation.
- `disabled` - Boolean variable disabling and enabling COEP

## Examples

```xml
<interceptor name="coep" class="org.apache.struts2.interceptor.CoepInterceptor"/>

<action  name="someAction" class="com.examples.SomeAction">
    <interceptor-ref name="defaultStack">
    <interceptor-ref name="coep">
            <param name="exemptedPaths">path1,path2,path3 <param>
            <param name="enforcingMode">false<param>
            <param name="disabled">false</param>
    <interceptor-ref>
    <result name="success">good_result.ftl</result>
</action>
```