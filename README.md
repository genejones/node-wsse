# WSSE

WSSE Username Token generator for Browserify

Based off the excellent [node-wsse by boyuza](https://travis-ci.org/bouzuya/node-wsse), but optimized for in browser usage.
Because node-wsse requires the entire crypto module, this module can be over 400KB when minified!
But the module really only uses SHA1, which is less than 30KB.
To solve this, we just load only the SHA-1, via sha.js. All other usage is identical.

See: http://www.xml.com/pub/a/2003/12/17/dive.html

## Installation

```
$ npm install wsse
```

## Usage

```javascript
var wsse = require('wsse');

var token = wsse({ username: 'bob', password: 'taadtaadpstcsm' });

// 'bob'
console.log(token.getUsername());

// 'taadtaadpstcsm'
console.log(token.getPassword());

// e.g. '2003-12-15T14:43:07Z'
console.log(token.getCreated());

// e.g. 'd36e316282959a9ed4c89851497a717f'
console.log(token.getNonce());

// e.g. 'ZDM2ZTMxNjI4Mjk1OWE5ZWQ0Yzg5ODUxNDk3YTcxN2Y='
console.log(token.getNonceBase64());

// e.g. 'quR/EWLAV4xLf9Zqyw4pDmfV9OY='
console.log(token.getPasswordDigest());

// e.g. 'UsernameToken Username="bob", PasswordDigest="quR/EWLAV4xLf9Zqyw4pDmfV9OY=", Nonce="d36e316282959a9ed4c89851497a717f", Created="2003-12-15T14:43:07Z"'
console.log(token.getWSSEHeader());
console.log(token.toString());
console.log(token + '');

// ----- advanced -----

// you can use `UsernameToken` class.
var token2 = new wsse.UsernameToken({
  username: 'bob',                           // (required)
  password: 'taadtaadpstcsm',                // (required)
  created: '2003-12-15T14:43:07Z',           // (optional) you can specify `craeted`.
  nonce: 'd36e316282959a9ed4c89851497a717f', // (optional) you can specify `nonce`.
  sha1encoding: 'hex'                        // (optional) you can specify `sha1encoding` for wrong WSSE Username Token implementation.
});

// you can use `nonceBase64` option. it encodes the nonce to base64 in header.
// 'UsernameToken Username="bob", PasswordDigest="quR/EWLAV4xLf9Zqyw4pDmfV9OY=", Nonce="ZDM2ZTMxNjI4Mjk1OWE5ZWQ0Yzg5ODUxNDk3YTcxN2Y=", Created="2003-12-15T14:43:07Z"'
console.log(token2.getWSSEHeader({ nonceBase64: true }));
console.log(token2.toString({ nonceBase64: true }));
```

## License

[MIT](LICENSE)


## Author

[user]: https://github.com/generjones
[email]: mailto:iam@genejon.es
