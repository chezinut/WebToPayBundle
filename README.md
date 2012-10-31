#WebToPayBundle

##What is WebToPayBundle?
WebToPayBundle is a small bundle that can serve as a bridge between your Symfony framework and the original web to pay library.

We encourage you to first take a look at the [original library](https://bitbucket.org/webtopay/libwebtopay)


##Sections
* [Requirements](#requirements)
* [Installation](#installation)
* [Code samples](#code-samples)
* [Code samples](#contacts)

##Requirements
* Symfony 2.0+

##Installation
* Download the original WebToPay library (can be downloaded [here](http://bitbucket.org/webtopay/libwebtopay/get/default.zip))
* The downloaded library can be placed in the vendors catalogue ("vendor/evp/webtopay" is the recommended path)
* Create a directory called Evp in your src directory
* Use ```git clone https://github.com/evp/WebToPayBundle.git``` in your src/Evp directory to retrieve the WebToPayBundle
* Add the following code to your app/autoload.php:

```php
   $loader->add('WebToPay', __DIR__.'/../vendor/evp/webtopay/src');
```
* Update your AppKernel by adding the new bundle to the list

```php
         $bundles = array(
             // ... your existing bundles here
             new \Evp\Bundle\WebToPayBundle\EvpWebToPayBundle()
         );

         if (in_array($this->getEnvironment(), array('dev', 'test'))) {
             // ... your existing bundles here
             $bundles[] = new \Evp\Bundle\WebToPayBundle\EvpWebToPayBundle();
         }
```

* Configure your app/config/config.yml
```
   evp_web_to_pay:
       credentials:
           project_id: your_project_id
           sign_password: your_password
```
Don't forget to replace *your_project_id* and *your_password* with the actual credentials.

That's it, you are now ready to use WebToPayBundle.

##Code samples
###CallbackValidation
Use the evp_web_to_pay.callback_validator service to perform callback validation

```php
   try {
     $callbackValidator = $this->get('evp_web_to_pay.callback_validator')->validateAndParseData($request->query->all());
     $data = $callbackValidator->validateAndParseData($request->query->all());
     if ($data['status'] == 1) {
       // Provide your customer with the service
     }

   } catch (\Exception $e) {
    //handle the callback validation error here
   }
```
###Creating a request
Use the evp_web_to_pay.request_builder service to create a request:

```php
->get('evp_web_to_pay.request_builder')->buildRequest(array(
  // information about the current payment request
));
```
Information about the current payment request has to be an array and may contain the following indexes
```
      orderid
      accepturl
      cancelurl
      callbackurl
      lang
      amount
      currency
      payment
      country
      paytext
      p_firstname
      p_lastname
      p_email
      p_street
      p_city
      p_state
      p_zip
      p_countrycode
      test
      time_limit
```
Orderid,accepturl,cancelurl and callbackurl parameters are ***mandatory***. The rest are optional.


##Contacts
If you have any further questions feel free to contact us:

```
"EVP International", UAB
Mėnulio g. 7
LT-04326 Vilnius
Email: pagalba@gsms.lt
Tel. +370 (5) 2 03 27 19
Faksas +370 (5) 2 63 91 79
```