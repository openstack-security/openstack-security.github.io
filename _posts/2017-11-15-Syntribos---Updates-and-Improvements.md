---
layout: post
title:  "Syntribos - Updates and Improvements"
date:   2017-11-15
categories: syntribos
tags: OSSP Python Security Syntribos
author: "mdong @ Rackspace"
---

It has been a while since the last official release of [Syntribos][] - a whole year, in fact! But we haven't been sitting idle. This week, we're happy to be releasing Syntribos 0.4.1, which comes with significant improvements on usability and performance. These efforts were based, in large part, on feedback from Rackspace security engineers, who have been using Syntribos for their API security testing needs on a variety of projects. We hope that these changes will make Syntribos better suited to your testing needs as well.

## Multithreading

One of the biggest pain points that testers had when using Syntribos has been its performance. Because Syntribos serialized its requests, a full run on a large project running on a remote host could sometimes take hours. In Syntribos 0.4.1, we have made wholesale changes to the runner, allowing a configurable number of workers to send requests in parallel. What this means in practice is a dramatic improvement in performance.

![Old: Single threaded](https://i.imgur.com/FKdH0a9.png)

![New Multithreaded](https://i.imgur.com/jnHlAbt.png)

These images show the significant speed-up we are able to achieve with our new multi-threaded runner in Syntribos 0.4.1 compared to Syntribos 0.3.1. These tests were run with against a small API with ~50ms network lag. 

Of course, this behavior is fully configurable with command line options or config file parameters, should you be testing against rate-limited endpoints or endpoints that don't handle concurrent connections well.

## Template Meta-Variables

Request templates in Syntribos have always had the advantage of being very similar to raw HTTP requests, which makes it easy for testers to create them for a project. However, this process usually involves a fair bit of tedious copy-and-pasting, even on attributes that are shared across templates. That means any changes to a group of templates required the user to open them up individually and editing them one-by-one, a slow manual process that was prone to mistakes. Furthermore, in order for request templates to fully take advantage of Syntribos' extensions or any other external libraries, they were cluttered with long, ugly `CALL_EXTERNAL` directives. In addition, these request templates could only hold a limited amount of information - Syntribos treated nearly every part of the template identically, and there was no way for the user to specify, for example, that certain fields should be only fuzzed with url-encoded characters, or with strings of a certain length, etc. 

To solve these problems, we introduced the concept of *meta-variables*. Meta-variables are simply JSON objects stored in a file separate from the request templates that define reusable variables to be referenced in request template parsing. These meta-variables can be referenced by any number of request templates, and they can even inherit values from other meta-variable files based on the directory they're in. 

It's probably easiest to demonstrate meta-variables by way of example.  

This is a typical request template, `post_image.template`:

```http
POST /v2/images HTTP/1.1
X-Auth-Token: CALL_EXTERNAL|syntribos.extensions.identity.client:get_token_v2:["user"]|

{
    "name": "Test",
    "id": "CALL_EXTERNAL|syntribos.extensions.random_data.client:get_uuid:[]|"
    ...
}
```

This request template is perfectly usable as-is, and indeed, Syntribos remains fully backwards-compatible with any request templates that you have already created. 

But maybe you want to make a change to something like that `x-auth-token` header, which would be one you'd likely want to reflect to many other templates as well. Before, the only way to do so would be to manually edit all these templates one at a time. 

Also, maybe you know that the API does some input validation, and only accepts ASCII characters for the `name` in the body. Before, there would be no way to pass that information to Syntribos.

Finally, it's not very pretty to look at. Before, you'd just have to live with it.

Meta-variable files allow you to create a file, `meta.json` in the same directory as your template. Such a file might look like this:

```json
{
  "token": {
    "type": "function", 
    "val": "syntribos.extensions.identity.client:get_scoped_token_v3",
    "args": ["user"]
  },
  "id": {
    "type": "function",
    "val": "syntribos.extensions.random_data.client:get_uuid"
  },
  "name": {
    "val": "Test"
    "fuzz_types": ["ascii"]
  }
}
```

This would allow your template to now look like this:

```http
POST /v2/images HTTP/1.1
X-Auth-Token: |token|

{
    "name": "|name|",
    "id": "|id|"
    ...
}
```

Now, your templates are simplified while holding more information. And of course, you can reference all those variables defined in `meta.json` in your other request templates as well.

For more detailed information on meta-variables, refer to our documentation here: https://docs.openstack.org/syntribos/latest/test-anatomy.html#meta-variable-file

## What's Next?

We have big plans ahead for Syntribos. We would like to enable Syntribos to understand context beyond a single request, allowing more complex tests that create, modify, and clean up a resource. Another goal of ours is to make Syntribos more CI/CD friendly, and we're exploring ways to integrate Syntribos into gate jobs and build pipelines. We are also always working on improvements to the test cases themselves, as well to the documentation, so that Syntribos will be more accurate and user-friendly.

If you have any questions about Syntribos, we are available at `#openstack-security` on freenode. User feedback is so important to us as we continue development, and we'd love to hear from you! 

If you'd like to contribute to Syntribos, please refer to https://docs.openstack.org/syntribos/latest/contributing.html . We are proud to be part of the Openstack community, and we always welcome contributors!



[syntribos]: https://github.com/openstack/syntribos