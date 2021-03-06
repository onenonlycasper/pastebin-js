pastebin-js
===========

NodeJS module to access the Pastebin API

```js
var PastebinAPI = require('pastebin-js'),
    pastebin = new PastebinAPI('devkey');
```


## Features

* getPaste : get a raw paste
* createAPIuserKey : get a userkey for the authenticated user
* listUserPastes : get a list of the pastes from the authenticated user
* getUserInfo : get a list of info from the authenticated user
* listTrendingPastes : get a list of the trending pastes on Pastebin
* createPaste : create a paste
* createPasteFromFile : read a file (UTF8) and paste it

## Example

```js
var PastebinAPI = require('./index'),
    pastebin = new PastebinAPI({
      'api_dev_key' : 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
      'api_user_name' : 'PastebinUserName',
      'api_user_password' : 'PastebinPassword'
    });

pastebin
    .createPasteFromFile("./uploadthistopastebin.txt", "pastebin-js test", null, 1, "N")
    .then(function (data) {
        // we have succesfully pasted it. Data contains the url
        console.log(data);
    })
    .fail(function (err) {
        console.log(err);
    });
```

## API

**PastebinAPI()** : Constructor.

```js
var PastebinAPI = require('./index');

// Without any parameter you can only use getPaste!
var pastebin = new PastebinAPI();

// Provide a developer key as string, this key can be found when logged in.
// This can be found here: http://pastebin.com/api#1
var pastebin = new PastebinAPI('xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx');

// Provide an object containing the api_dev_key, api_user_name and api_user_password
pastebin = new PastebinAPI({
                'api_dev_key' : 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
                'api_user_name' : 'PastebinUserName',
                'api_user_password' : 'PastebinPassword'
               }); 
```

### Methods

**pastebin.getPaste(pasteID)** : get a raw paste, providing the ``pasteID``

```js
pastebin
  .getPaste('76b2yNRt')
  .then(function (data) {
    // data contains the raw paste
    console.log(data);
  })
  .fail(function (err) {
    // Something went wrong
    console.log(err);
  })
```

**pastebin.createPaste(text, title, format, privacy, expiration)** : creates a paste. ``text`` is required, other
arguments are optional. For ``format``, ``privacy`` and ``expiration``, have a look at **lib/config.js** for the allowed input.
If ``privacy`` is set to **2**, you will need to provide a username && password in the constructor (Pastebin requires a api_user_key)

```js
pastebin
  .createPaste("Test from pastebin-js", "pastebin-js")
  .then(function (data) {
    // paste succesfully created, data contains the paste url
    console.log(data);
  })
  .fail(function (err) {
    // Something went wrong
    console.log(err);
  })
```

**pastebin.createPasteFromFile(filename, title, format, privacy, expiration)** : tries to read the file provided in ``filename``
(UTF-8) and paste it. Works the same as previous method.

**pastebin.deletePaste()** : NOT YET IMPLEMENTED! (Will be in future version)

**pastebin.getUserInfo()** : gets the userinfo 

**pastebin.listUserPastes(limit)** : gets a list of pastes from the user. ``limit`` is optional, from 1 - 100 (default: 50)

**pastebin.listTrendingPastes()** : gets a list of trending pastes on Pastebin


## Bugs / issues

Please, if you find any bugs, or are a way better developer than I am (as in, you are thinking 'spaghetti' when looking at my
code), feel free to create an issue or provide me with some pull requests! This is my first full module ever written for
NodeJS.

## License

Copyright (c) 2013-2013 J.W. Lagendijk &lt;jwlagendijk@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
