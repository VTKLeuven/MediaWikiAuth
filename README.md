MediaWikiAuth
=============

Custom MediaWiki module that authenticates against Litus.

## Requierements

* A working [Litus](https://github.com/LitusProject/Litus) webserver with a working API.
* A MediaWiki installation, version 1.13+
* The domain of the wiki has to be a subdomain of the domain of the Litus server, or the same domain (e.g. if the Litus server is litus.cc, wiki.litus.cc or litus.cc/wiki will both work, lituswiki.cc won't)
* Optional: the PHP curl module (on ubuntu: install the php5-curl package)

## Installation

You have to have mediawiki installed and configured.
To use curl instead of the standard PHP http requests, make sure php5-curl (on ubuntu) is installed.

Execute in a shell:
```bash
cd <path to your mediawiki folder>/extensions
git clone https://github.com/LitusProject/MediaWikiAuth.git LitusAuth
```

Edit your LocalSettings.php, add somewhere at the bottom:
```php
require_once($IP . '/extensions/LitusAuth/LitusAuthPlugin.php');

/* The Litus API Server to use for authentication, without trailing slash. */
$wgLitusAPIServer = 'https://litus.cc/api';

/* The API key */
$wgLitusAPIKey = 'abcdefghijklmnopqrstuvwxyz';

/* The Litus server itself, for the login link, without trailing slash! */
$wgLitusServer = 'https://litus.cc';

/* Required status to be allowed to log in */
$wgLitusRequiredStatus = array(
    'university_status' => false,
    'organization_status' => false
);

/* The web page to redirect to if the user has an invalid status. */
$wgLitusInvalidStatusRedirect = false;
```

Replace the $wgLitusAPIServer, $wgLitusAPIKey and $wgLitusServer values with the real values for your Litus installation.

## License
```
Copyright 2012 The Litus Project and other contributors
<https://github.com/LitusProject>

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
