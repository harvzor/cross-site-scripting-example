## What is this?

This repo shows how simple and complex cross domain requests can be made to include the target domain's cookies.

[![Video showing cross site scripting](http://img.youtube.com/vi/uiNkXxWoh2w/0.jpg)](http://www.youtube.com/watch?v=uiNkXxWoh2w "Video showing cross site scripting")

There are two websites run from this repo:

- attacker.local
- defender.local:3000

attacker.local is making a cross domain scripting request to defender.local and is trying to include a cookie that is set on defender.local

Requirements for that are:

- the cookie on defender.local must be set with `SameSite: none` and `Secure` in order for simple requests to work

Complex AJAX requests:

- the requesting domain must specify `credentials: 'include'` (if using the Fetch API)
- the responding domain must respond the headers `Access-Control-Allow-Origin: https://attacker.local` and `Access-Control-Allow-Credentials: true`

Note that simple AJAX requests will still be performed even if the responding domain doesn't have the headers set. However, because the simple request occurs without CORS preflight, the receiving server will still receive the request, but the user's browser will block the request after it has seen that the headers are missing.

## How to run

### Setup

The hosts file needs these inputs:

```
127.0.0.1 attacker.local
127.0.0.1 defender.local
```

Requirements:

- Node v18.20.2

### The attacker

```
npm install http-server -g
http-server -p 443 -a attacker.local --ssl
```

### The defender

```
node index.mjs
```
