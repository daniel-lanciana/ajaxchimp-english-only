# ajaxChimp

AjaxChimp is a jQuery plugin that lets you ajaxify your mailchimp form.

Use this if you hate the jarring transition to the mailchimp website upon submitting an email address to mailchimp.

**Note**: This relies on an undocumented feature at mailchimp that uses JSONP to allow cross-domain ajax to work. You have been warned. (It has however, been around for at least 3 years that I know of, and probably more.)

## Install

Fork of https://github.com/scdoshi/jquery-ajaxchimp with the following changes:

* HTTPS support
* Trailing semicolon
* Removed translations (reduce file size for English-only sites)
* Support for firstname, lastname
