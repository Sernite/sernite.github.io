<div class ="app-header">
SERNITE.
<div class = "app-header-underline"> </div>
</div>
<br>

<br>

# Introduction
> High-Level Server-Side Scripting Framework


---
## What is Sernite

Sernite is a server-side scripting framework for building pretty modular web servers. Unlike other frameworks, Sernite has unique components such as [nits](/) and [sernite-scripts](/) and multi language scripting support

## Installation

Sernite can be installed easily by [npm](//npmjs.com/sernite)

```bash
npm install -g sernite
```

## Quickstart

In few steps, your first application will be ready
Open your project directory and create a new director

```bash
cd your/fav/directory
mkdir example-project && cd example-project
```
After creating a new project directory and open it.
Initialize sernite app
```bash
sernite init --yes
```
`--yes` means that skips all questions. Now, sernite app is  ready to start.
```bash
sernite start
```

## Sernite Scripts

sernite script is a script that invoked when its assigned request arrived at the server. After invoking, scripts communicate to Sernite app core with standard output streams so sernite scripts can be written by multiple languages. All sernite scripts have 3 core concepts:

1. **Params** : parameters that passing through argv. it may be URL parameters, form data, etc. It's defined in sernite.json


2. **Done** : a function that exits the script with or without error code. In some languages that function is unnecessary


3. **Handler Function** : a function that handle request. has two parameters:
    -  **send** : a function that sends a message to a web client.

    -  **nitmsg**: a function that sends a message to a nit and waits for a response and then returns it

a sernite script can be added easly to project using

```bash
sernite add script
```
after running this command, you will  fill some area:
  -  **URL** : the URL that invokes this sernite scripts
  
  -  **PATH** : path of the sernite script
  
  -  **PARAMS** : parameters which passing to sernite script. these parameters may be static or dynamic parameters. in example, for ``/user/:id``, ``"url:id"`` passes id url variable to sernite scripts. format : param1,param2,param3...
  -  **HEADERS** : response headers. format : ``key1=val1,key2=val2...``

after that process, your script will be created in path that you define.

some example sernite scripts:

```javascript

function handler(send, nitmsh) {
  let res = nitmsg('sum','4,5,12');
  send(res)
  done()
}

module.exports = handler;
```


```go
package main

import (
	sernite "github.com/Sernite/gosernite"
)

func main() {
	// Set handler function
	sernite.SetHandler(func(send sernite.SendFunc, nitmsg sernite.NitMsg) {
		res := nitmsg("sum", "4,5,12")
		send(res)
	})
	// Start handler
	sernite.Run()
}

```
