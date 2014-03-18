#Mercenary#
*An Open Source Distributed Task Orchestration Framework*

While its intended use case is for managing and reporting on the execution of vendor-agnostic automated testing, its extensible framework means it is not limited to just software testing applications.

As the framework is open source, servers and targets can be implemented in any language on any platform, as long a they can be send and receive HTTP.

Server starts up and listens for two kinds of requests

##The Target##
###Overview###
Target has specific capabilities via plugins
Target has a specific environment

A target receives a request to perform a task detailed in JSON.  If it is not currently engaged in performing a task, and has the environment and capabilities specified in the request, then it passes the request on to the appropriate plugin to execute the task.  The plugin that performs the task has the option to manipulate and/or append to the JSON payload.  Once complete, the payload is returned.

If there is no server (is this an option?  I think it should be) where does the data go?

###Target Configuration###
    {
    	"registration-url" : "192.168.0.1:7001",
    	"listen-on-host"   : "localhost",
    	"listen-on-port"   : "7050",

    	"environment": {...},

    	"capabilities": {...}
    }

##The Server##
Running a target locally without a server is a good way to test and debug, but in a production system, you will likely want to employ a server, as without it you no longer have "distributed" or "orchestration".

When the server starts, it begins listening on the configured port.
Are servers are optional?
Server listens for two different kinds of requests

###Server Configuration###
    {
    	"listening-on"   : "localhost:8080",
    	"listen-on-host" : "localhost",
    	"listen-on-port" : "8080"
    }

##Request Interface##
    {
    	"target-url" : "localhost:8080",

    	"environment":
    	{
    		"os" : "Windows",
    		"video-card" : "NVidia",
    		"x-important-environment" : "y-whatever-value"
    	},

    	"capabilities":
    	[
    		"plugin-name",
    		"other-plugin"
    	]
    }

Notice how this looks very similar to the target configuration file?  A few unnecessary key-value pairs are removed, and the capabilities configuration section is flattened out to an array, as the names are the only relevant information to the server.

###Task Execution Request###



##Server and Target Administration##
Via the url, see status and task history
Turn off a server or a target
Turn off a target, have it notify the server

