# How to create components in Yii2

> Components are reusable classes that can be loaded in config file and can be used at any where in your application, Including frontend and backend.

Below we will create a component to sen SMS to someone

Create a SmsMessage.php file in common/components directory.
If it doesn't exists, Create it.
```
<?php

namespace common\components;

use yii;

class SmsMessage
{
    /**
     * Send SMS Notification method
     * @param $number
     * @param $message
     */
    private static function send($number, $message)
    {
        $uri = 'https://example.net/';
        $response = \Httpful\Request::get($uri)->send();

        if($response->code = 200)
        {
            return true;
        }

        return false;
    }
}
```

Now our compomnent is ready, We just need to configure this in the main.php file.

in common/config/main.php file

```
<?php
return [
    'vendorPath' => dirname(dirname(__DIR__)) . '/vendor',
    'components' => [
        'sms' => [
            'class' => 'common\components\SmsMessage'
        ],
    ],
];
```

This will autoload this component in application initialization for each HTTP request.


To use this component, Just use the Yii:$app property:
```
Yii::$app->sms->send('9716014362', 'Hi, Saurabh. How are you today ?');
```


> We had used Httpful class here, That's just for an example.
