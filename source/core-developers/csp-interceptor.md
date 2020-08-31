---
layout: default
title: CSP Interceptor
parent:
    title: Interceptors
    url: interceptors.html
---

# Fetch Metadata Interceptor

## Description

An interceptor that implements the Content Security Policy (CSP) on incoming requests.

Content Security Policy is a mitigation against XSS and CSS injection attacks. The recommended way to use CSP is to implement [strict CSP](https://csp.withgoogle.com/docs/index.html).

CSP is enabled by setting the `Content-Security-Policy` or `Content-Security-Policy-Report-Only` HTTP response headers, based on whether it’s in enforcing or reporting mode, respectively. In enforcing mode, any event that violates the policy is not executed and if the policy specifies  a `reportUri` a JSON object with the details of the CSP violation is sent to the specified endpoint. In reporting mode, the event is executed normally and a CSP report is being sent to the defined `reportUri`.

We provide a `DefaultCspSettings` class that specifies a strict-dynamic nonce-based policy, which means the `DefaultCspSettings` also handles generating a nonce value. With each response, a new nonce value is generated which is specific to each request cycle. This design provides developers with a robust policy they can use, but also the flexibility to implement their own policy and use it with the CspInterceptor if they need to. The interceptor calls the `addCspHeaders` method of `DefaultCspSettings` which adds the CSP header to the response and attaches the nonce value in the request's session. The session is a generic map of key, value pairs unique to every request.

Refer to the security [index file](https://github.com/apache/struts-site/blob/master/source/security/index.md) for more infomation about the CSP policy and design.

```
Content-Security-Policy:
  object-src 'none';
  script-src 'nonce-{random}' 'strict-dynamic' https: http:;
  base-uri 'none';
  report-uri https://your-report-collector.example.com/csp-report
```


## Parameters

- `enforcingMode` - Boolean variable the defines whether the `CspInterceptor` operates under enforcing or reporting mode. In enforcing mode, any event that violates the policy is not executed and if the policy specifies  a `reportUri` a JSON object with the details of the CSP violation is sent to the specified endpoint. In reporting mode, the event is executed normally and a CSP report is being sent to the defined `reportUri`. Default vaulue for variable is `false`.

## Examples

```xml
<action  name="someAction" class="com.examples.SomeAction">
    <interceptor-ref name="defaultStack">
            <param name="cspInterceptor.enforcingMode">false</param>
    </interceptor-ref>
    <result name="success">good_result.ftl</result>
</action>
```