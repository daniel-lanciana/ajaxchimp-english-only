# ajaxChimp

AjaxChimp is a jQuery plugin that lets you ajaxify your mailchimp form.

Use this if you hate the jarring transition to the mailchimp website upon submitting an email address to mailchimp.

**Note**: This relies on an undocumented feature at mailchimp that uses JSONP to allow cross-domain ajax to work. You have been warned. (It has however, been around for at least 4 years that I know of, and probably more.)

## Fork

Fork of dead project https://github.com/scdoshi/jquery-ajaxchimp (no commits since 2015).

## Features/Changes

* Removed translations (reduce file size for English-only sites)
* Added support for firstname and lastname

## Install

Just add the script to your webpage (along with jQuery ofcourse). Get it here:

```
curl -O https://raw.githubusercontent.com/daniel-lanciana/jquery-ajaxchimp/master/jquery.ajaxchimp-english-only.js
```

#### bower

```
bower install ajaxchimp-english-only
```


## Requirements

* jQuery

**Note**: Developed with 1.9.1, but it should work with earlier versions. If it does or does not work with a particular version, please open an issue on github.

## Use

#### On the mailchimp form element

```js
$('form-selector').ajaxChimp();
```

## Label

If a label element is included in the form for the email input, then the success or error message will be displayed in it. A `valid` or `error` class will also be added accordingly.

#### Example Form

```html
    <form id="mc-form">
        <input id="mc-email" type="email" placeholder="email">
        <label for="mc-email"></label>
        <button type="submit">Submit</button>
    </form>
```

```js
$('#mc-form').ajaxChimp({
    url: 'http://blahblah.us1.list-manage.com/subscribe/post?u=5afsdhfuhdsiufdba6f8802&id=4djhfdsh9'
});
```


## Options

### Callback

Optionally, you can specify a callback with either method to run after the
ajax query to mailchimp succeeds or fails.

```js
$('form-selector').ajaxChimp({
    callback: callbackFunction
});
```

The JSONP response from mailchimp will be passed to the callback function

```js
function callbackFunction (resp) {
    if (resp.result === 'success') {
        // Do stuff
    }
}
```

### URL

You can specify the mailchimp URL to post to (or override the url provided on the form element). Format of the URL is as follows (start with `//` if you want optional HTTPS support:

```js
$('form-selector').ajaxChimp({
    url: '//blahblah.us1.list-manage.com/subscribe/post?u=5afsdhfuhdsiufdba6f8802&id=4djhfdsh99f'
});
```

### Responses

The mapping to english for mailchimp responses and the submit message are as follows:

```js
    // Submit Message
    // 'submit': 'Submitting...'

    // Mailchimp Responses
    // 0: 'We have sent you a confirmation email'
    // 1: 'Please enter a value'
    // 2: 'An email address must contain a single @'
    // 3: 'The domain portion of the email address is invalid (the portion after the @: )'
    // 4: 'The username portion of the email address is invalid (the portion before the @: )'
    // 5: 'This email address looks fake or invalid. Please enter a real email address'

```

### Demo

Code from `demo.html`:

```html
<html>
	<head>
		<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
		<script type="text/javascript" src="jquery.ajaxchimp-english-only.js"></script>
	</head>	

	<body>
		<form id="demo-form">
			<!-- First and last name are optional, or could be hidden -->
		    <input name="firstname" type="text" placeholder="First name">
		    <input name="lastname" type="text" placeholder="Last name">
		    
		    <input id="form--email" type="email" placeholder="Email">
		    
		    <!-- Display set submit/success/error messages -->
		    <label for="form--email"></label>

			<!-- Display custom success/error messages -->
		    <div class="success" style="display: none;">Custom success!</div>
		    <div class="error" style="display: none;">Custom error!</div>

		    <button type="submit">Submit</button>
		</form>

		<script>
			$('#demo-form').ajaxChimp({
			    url: '//blahblah.us1.list-manage.com/subscribe/post?u=5afsdhfuhdsiufdba6f8802&id=4djhfdsh99f',
			    callback: function(response) {
			    	console.log('MailChimp response received', response);

		    		// Hide both messages in case we resubmit..
				$('#demo-form .success').hide();
				$('#demo-form .error').hide();

		    		(response && response.result === 'success') ? $('#demo-form .success').show() : $('#demo-form .error').show();
			    }
			});
		</script>
	</body>
</html>
```
