---
layout: post
title:  "Basi Authentication with PHP"
date:   2015-10-15 18:32:12
categories: php http authentication
---

It is possible to use the header() function to send an "Authentication Required" message to the client browser causing it to pop up a Username/Password input window. Once the user has filled in a username and a password, the URL containing the PHP script will be called again with the predefined variables PHP_AUTH_USER, PHP_AUTH_PW, and AUTH_TYPE set to the user name, password and authentication type respectively. These predefined variables are found in the $_SERVER array. Both "Basic" and "Digest" (since PHP 5.1.0) authentication methods are supported. See the header() function for more information.

An example script fragment which would force client authentication on a page is as follows:

{% highlight php %}
<?php
if (!isset($_SERVER['PHP_AUTH_USER'])) {
    header('WWW-Authenticate: Basic realm="My Realm"');
    header('HTTP/1.0 401 Unauthorized');
    echo 'Text to send if user hits Cancel button';
    exit;
} else {
    echo "<p>Hello {$_SERVER['PHP_AUTH_USER']}.</p>";
    echo "<p>You entered {$_SERVER['PHP_AUTH_PW']} as your password.</p>";
}
?>
{% endhighlight %}

