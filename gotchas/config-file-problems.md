## Config file problems

##### PROBLEM

> After preparing your project via CLI, you may notice the platform config files don’t pick up exactly what’s in your root config file, and instead show the stock “Hello Cordova” info.

##### SOLUTION

The `config.xml` file is generated from a file called `defaults.xml` located in `platform/ios/cordova`. This is not documented, [I’ve filed a bug](https://issues.apache.org/jira/browse/CB-5894) so hopefully it will be soon. Edit the `defaults.xml` file and your generated files will more closely resemble the desired output. 

==

##### PROBLEM 

>Why are there multiple config files under the platform directory? 

##### SOLUTION

Another undocumented mystery for the ages. Do you know why? Please fork this repo and contribute the answer in this .md file.
