# Payara Server Administration and Monitoring API


<a name="overview"></a>
## Overview
This API allows users to interact with the Payara Server's DAS through a REST interface. It allows execution of administration commands in a similar way as the `asadmin` utility, such as:

* Execute administration commands to modify the domain's configuration.
* Retrieve monitoring statistics
* Look at the domain's log entries.

To change the configuration of the domain, it is really necessary to understand how the configuration resources are organized in a tree model. To interact with a resouce, it is recommended to first call the `GET` method of the `  /management/domain/{resource}` endpoint to understand what operations are supported and other details (parameters, subcommands, etc.)

To execute the API calls to the server, consider the following URL as an example:

  ***http(s)://localhost:4848/management/domain***

Remember to change the administration port (usually **4848** by default on most domain configurations).

In order to successfully consume the endpoints in this API, it must be taken into consideration if the domain's access is already secured. If so, then one of the *2* decribed security schemes must be used.


### Version information
*Version* : 1.0.0


### URI scheme
*Host* : localhost  
*Schemes* : HTTP, HTTPS


### Tags

* configuration : Used for domain configuration operations
* logging : Used for domain logging purposes
* monitoring : Used for monitoring operations
* sessions : Used for session management
