# NotificationPusher - Documentation

## GCM adapter

[GCM](http://developer.android.com/google/gcm/gs.html) adapter is used to push notification to Google/Android devices.

### Custom notification push example

``` php
<?php

require_once '/path/to/vendor/autoload.php';

use Sly\NotificationPusher\PushManager,
    Sly\NotificationPusher\Adapter\Gcm as GcmAdapter,
    Sly\NotificationPusher\Collection\DeviceCollection,
    Sly\NotificationPusher\Model\Device,
    Sly\NotificationPusher\Model\Message,
    Sly\NotificationPusher\Model\Push
;

// First, instantiate the manager.
//
// Example for production environment:
// $pushManager = new PushManager(PushManager::ENVIRONMENT_PROD);
//
// Development one by default (without argument).
$pushManager = new PushManager(PushManager::ENVIRONMENT_DEV);

// Then declare an adapter.
$gcmAdapter = new GcmAdapter(array(
    'apiKey' => 'YourApiKey',
));

// Set the device(s) to push the notification to.
$devices = new DeviceCollection(array(
    new Device('Token1'),
    new Device('Token2'),
    new Device('Token3'),
));

// Then, create the push skel.
$message = new Message('This is an example.');

// Finally, create and add the push to the manager, and push it!
$push = new Push($gcmAdapter, $devices, $message);
$pushManager->add($push);
$collection = $pushManager->push(); // Returns a collection of notified devices

foreach ($collection as $push) {
    $adapter = $push->getAdapter();
    $response = $adapter->getResponse();
    
    foreach ($response as $pushChunk) {
        // combine array of tokens and responses to preserve consistent of indexes
        $tokens = $pushChunk->getMessage()->getRegistrationIds();
        $responses = $pushChunk->getResults();
        var_dump(array_combine($tokens, $responses));
        
        //there are also way to check only count of sent notifications
        //var_dump($pushChunk->getSuccessCount());
        //var_dump($pushChunk->getFailureCount());
    }
}
```

## Documentation index

* [Installation](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/installation.md)
* [Getting started](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/getting-started.md)
* [APNS adapter](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/apns-adapter.md)
* GCM adapter
* [Create an adapter](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/create-an-adapter.md)
* [Push from CLI](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/push-from-cli.md)
