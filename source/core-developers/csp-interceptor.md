---
layout: default
title: CSP Interceptor
parent:
    title: Interceptors
    url: interceptors.html
---

# Content Security Policy Interceptor

## Description

An interceptor that implements the Content Security Policy (CSP) on incoming requests.

Content Security Policy is a mitigation against XSS and CSS injection attacks. The recommended way to use CSP is to implement [strict CSP](https://csp.withgoogle.com/docs/index.html).

CSP can enabled by setting either the `Content-Security-Policy` or the `Content-Security-Policy-Report-Only` HTTP response headers, which instruct the browser whether to enforce the policy or evaluate and report only. In enforcing mode, scripts and stylesheets that violate the policy will not be executed and if the policy specifies a value for the `report-uri` directive, a violation report will be sent to the specified endpoint. In reporting mode, while scripts and stylesheets are always allowed to run, CSP violation reports will be logged in DevTools and optionally sent to the defined `report-uri` endpoint.

Struts provides a `DefaultCspSettings` class that generates a strong strict-dynamic, nonce-based policy. This object will automatically generate a nonce value scoped to the current request. This design provides developers with a robust policy while giving them the flexibility to implement their own policy and use it with the CspInterceptor if they need to. The interceptor calls the `addCspHeaders` method of `DefaultCspSettings` which adds the CSP header to the response and attaches the nonce value in the request's session. The session's life cycle is tied to that of the request's.

Refer to the security [index file](https://github.com/apache/struts-site/blob/master/source/security/index.md) for more infomation about the CSP policy and design.

```
Content-Security-Policy:
  object-src 'none';
  script-src 'nonce-{random}' 'strict-dynamic' https: http:;
  base-uri 'none';
  report-uri https://your-report-collector.example.com/csp-report
```


## Parameters

- `enforcingMode` - Boolean variable the defines whether the policy is enforced. In enforcing mode, scripts and stylesheets that violate the policy won't be executed and, if the `reportUri` directive is set, a violation report will be sent to it. In reporting mode, all scripts and stylesheets are allowed to executed with violation reports sent to the defined `reportUri`. Default value for variable is `false`.
- `reportUri` - String URI where the CSP violation reports will be sent to. Path can be either relative with leading slashes or absolute. This field is empty by default.

## Examples

```xml
<action  name="someAction" class="com.examples.SomeAction">
    <interceptor-ref name="defaultStack">
            <param name="cspInterceptor.enforcingMode">false</param>
    </interceptor-ref>
    <result name="success">good_result.ftl</result>
</action>
```