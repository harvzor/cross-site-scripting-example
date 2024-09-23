## What is this?

[![Video showing cross site scripting](http://img.youtube.com/vi/uiNkXxWoh2w/0.jpg)](http://www.youtube.com/watch?v=uiNkXxWoh2w "Video showing cross site scripting")

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
