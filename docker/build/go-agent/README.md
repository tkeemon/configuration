##Usage
Start the container with this:

```docker run -ti -e GO_SERVER=your.go.server.ip_or_host gocd/gocd-agent```

If you need to start a few GoCD agents together, you can of course use the shell to do that. Start a few agents in the background, like this:

```for each in 1 2 3; do docker run -d --link angry_feynman:go-server gocd/gocd-agent; done```

##Getting into the container
Sometimes, you need a shell inside the container (to create test repositories, etc). docker provides an easy way to do that:

```docker exec -i -t CONTAINER-ID /bin/bash```

To check the agent logs, you can do this:

```docker exec -i -t CONTAINER-ID tail -f /var/log/go-agent/go-agent.log``` 

##Agent Configuration
The go-agent expects it's configuration to be found at ```/var/lib/go-agent/config/```. Sharing the 
configuration between containers is done by mounting a volume at this location that contains any configuration files 
necessary.


**Example docker run command:**
```docker run -ti -v /tmp/go-agent/conf:/var/lib/go-agent/config -e GO_SERVER=gocd.sandbox.edx.org 718d75c467c0 bash```

[How to setup auto registration for remote agents](https://docs.go.cd/current/advanced_usage/agent_auto_register.html)
