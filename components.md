# Components

Senrite bu

## Sernite Scripts

sernite script is a script that invoked when its assigned request arrived at the server. After invoking, scripts communicate to Sernite app core with standard output streams so sernite scripts can be written by multiple languages. All sernite scripts have 3 core concepts:

1. **Params** : parameters that passing through argv. it may be URL parameters, form data, etc. It's defined in sernite.json


2. **Done** : a function that exits the script with or without an error code. In some languages that function is unnecessary


3. **Handler Function** : a function that handle request. has two parameters:
    -  **send** : a function that sends a message to a web client.

    -  **nitmsg**: a function that sends a message to a nit and waits for a response and then returns it

a sernite script can be added easily to project using

```bash
sernite add script
```
after running this command, you have to  fill some area:
  -  **URL** : the URL that invokes this sernite scripts
  
  -  **PATH** : path of the sernite script
  
  -  **PARAMS** : parameters which passing to sernite script. these parameters may be static or dynamic parameters. in example, for ``/user/:id``, ``"url:id"`` passes a url variable ``id``  to sernite scripts. format : ``param1,param2,param3...``
  -  **HEADERS** : response headers. format : ``key1=val1,key2=val2...``

after that process, your script will be created in path that you define.

some example sernite scripts in sveral languages:

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

## Nits
  Nits are pure javascript functions that take a string and return an object.  Unlike sernite scripts, nits invoke when the app starts and they work continuously, nits are native parts of the app so they can be written with only `javascript`.


nits can be created easily using `sernite add nit` command. after running thi command, you have to fill some area:

- **Name** : name of the nit. a nit invoked by its name.
- **Path** : file path of the nit script.

an example nit script:

```javascript
// example query : 1,5,4,3,5
module.exports = async function (query) {
 let sum = query.split(',')
  .map(v => parseInt(v))
  .reduce((a, b) => a + b, 0);
  return sum;
}
```

