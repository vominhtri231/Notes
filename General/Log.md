# Log level
* Fatal: Represent errors that lead the application to abort, usually end up in catastrophic failures.
* Error: Represent errors that still allow the application continue to run, with reduced capabilities 
* Warning: Represent events that less harmful than errors  
* Info: Represent important events and informational messages
* Debug: Represent specific and detail imformation, mainly used for debug purposes
* Trace: represent most low-level information to provide the most information on a certain event/context, help to inspect the variable values and full error stack

# What to log or not

## What to log
* Incomming and outcomming messages
* Service and function invocations  
 Logging its context in lower log level helps for investigating issue related to business easily.
* User interaction and business stats  
They reveal insights for domain experts
* System event
* Performance stats
* Thread and vulnerabilities

## What not to log

* Personal identifiable information, business name and contact information
* Financial data
* Password, security key, etc
