BestCaptchaSolver.com php API wrapper
=========================================

bestcaptchasolver-php is a super easy to use bypass captcha php API wrapper for bestcaptchasolver.com captcha service

## Installation

    composer require bestcaptchasolver/bestcaptchasolver

or
    
    git clone https://github.com/bestcaptchasolver/bestcaptchasolver-php

## How to use?

Simply require the module, set the auth details and start using the captcha service:

``` php
require('lib/bestcaptchasolver.php'); 
```

Initialize library with access token

Get token from [https://bestcaptchasolver.com/account](https://bestcaptchasolver.com/account)
``` php
$bcs = new BestCaptchaSolver($ACCESS_TOKEN);   
```

Once you've set your authentication details, you can start using the API

**Get balance**

Returns balance in USD
``` php
$balance = $bcs->account_balance();
```

**Submit image captcha**

You can give it a b64 encoded string or a file path as `image` parameter

``` php
$p = array();
$p['image'] = 'captcha.jpg';
$id = $bcs->submit_image_captcha($p);
```

Optional parameters:
- case_sensitive - TRUE or FALSE, default: FALSE
- affiliate_id - ID of affiliate, can be gathered from /account page

**Retrieve image text**

Once you have the captcha ID, you can check for completion of captcha
```php
$image_text = NULL;
while($image_text === NULL) {
    $image_text = $bcs->retrieve($id)['text'];  // get the image text (if completed)
    sleep(2);                           // retry every 2 seconds
}
```

**Submit recaptcha details**

For recaptcha submission there are two parameters that are required an others that are optional
- page_url
- site_key
- type (optional)
- v3_action (optional)
- v3_min_score (optional)
- user_agent (optional)
- affiliate_id (optional)
- proxy (optional)

Check the [/api](https://bestcaptchasolver.com/api) page for more about this parameters

``` php
$p = array();
$p['page_url'] = $PAGE_URL;
$p['site_key'] = $SITE_KEY;
$id = $bcs->submit_recaptcha($p);
```


**Retrieve recaptcha gresponse**

Just as the image captcha, once you have the ID, you can start checking for it's
completion using the same retrieve method. The response (when ready) will be a gresponse code

```php
$gresponse = NULL;
while($gresponse === NULL) {
    $gresponse = $bcs->retrieve($id)['gresponse'];  // get the image text (if completed)
    sleep(2);                           // retry every 2 seconds
}
```

**If submitted with proxy, get proxy status**
```
$proxy_status = $bcs->retrieve($id)['proxy_status']
```

**Set captcha bad**

When a captcha was solved wrong by our workers, you can notify the server with it's ID,
so we know something went wrong.

``` php
$bcs->set_captcha_bad(50); 
```

## Examples
Check example.php

## License
API library is licensed under the MIT License

## More information
More details about the server-side API can be found [here](https://bestcaptchasolver.com/api)


<sup><sub>captcha, bypasscaptcha, decaptcher, decaptcha, 2captcha, deathbycaptcha, anticaptcha, 
bypassrecaptchav2, bypassnocaptcharecaptcha, bypassinvisiblerecaptcha, captchaservicesforrecaptchav2, 
recaptchav2captchasolver, googlerecaptchasolver, recaptchasolverpython, recaptchabypassscript, bestcaptchasolver</sup></sub>

