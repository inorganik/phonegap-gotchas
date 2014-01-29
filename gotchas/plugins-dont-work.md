## Cordova 3.X plugins don’t work.

##### PROBLEM

>You install a plugin, but the plugin features are not working, and/or the JavaScript objects they should be creating are undefined.

##### SOLUTION

Although the documentation states, to install a plugin, run:

    cordova plugin add org.apache.cordova.dialogs
    
But that doesn’t actually install it. More like downloads it. You must run

    cordova prepare ios
   
or

    cordova build ios
    
(where `ios` is your platform) before a new plugin work. One of those commands must be run _every time_ you add or remove a plugin for the change to be reflected. This is not mentioned in the documentation. [This is a bug](https://issues.apache.org/jira/browse/CB-5647) that affects Cordova <= 3.3

Please not those commands will also replace whatever `www` files you have in your platform directories with what’s in your root `www` directory. The workflow in Cordova 3.X has changed – you work from the root and run cordova prepare... everytime you edit your files, which is about a million times per day.
