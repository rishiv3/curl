# cURL

## Introduction

- cURL is a way you can hit a URL from your code to get a HTML response from it. 
- It's used for command line cURL from the PHP language.
- cURL is a library that lets you make HTTP requests in PHP.

PHP supports libcurl, a library created by Daniel Stenberg, that allows you to connect and communicate to many different types of servers with many different types of protocols. libcurl currently supports the http, https, ftp, gopher, telnet, dict, file, and ldap protocols. libcurl also supports HTTPS certificates, HTTP POST, HTTP PUT, FTP uploading (this can also be done with PHP's ftp extension), HTTP form based upload, proxies, cookies, and user+password authentication.

Once you've compiled PHP with cURL support, you can begin using the cURL functions. The basic idea behind the cURL functions is that you initialize a cURL session using the curl_init(), then you can set all your options for the transfer via the curl_setopt(), then you can execute the session with the curl_exec() and then you finish off your session using the curl_close(). 


````PHP
// error reporting
error_reporting(E_ALL);
ini_set("display_errors", 1);

//setting url
$url = 'http://example.com/api';

//data
$data = array("message" => "Hello World!!!");

````


````PHP
try {
    $ch = curl_init($url);
    $data_string = json_encode($data);

    if (FALSE === $ch)
        throw new Exception('failed to initialize');

		curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
		curl_setopt($ch, CURLOPT_POSTFIELDS, $data_string);
		curl_setopt($ch, CURLOPT_RETURNTRANSFER, false);
		curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
		curl_setopt($ch, CURLOPT_HTTPHEADER, array( 'Content-Type: application/json', 'Content-Length: ' . strlen($data_string)));
		curl_setopt($ch, CURLOPT_TIMEOUT, 5);
		curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 5);

    	$output = curl_exec($ch);

    if (FALSE === $output)
        throw new Exception(curl_error($ch), curl_errno($ch));

    // ...process $output now
} catch(Exception $e) {

    trigger_error(sprintf(
        'Curl failed with error #%d: %s',
        $e->getCode(), $e->getMessage()),
        E_USER_ERROR);
}
````


## For more information, please check -

[cURL Functions](http://php.net/manual/en/ref.curl.php)
