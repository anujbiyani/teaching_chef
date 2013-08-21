# Teaching Chef

!SLIDE

# Chef

## abiyani@lytro.com

!SLIDE left

# The Framework

### Chef vs Chef-Solo
* Chef-Solo runs on the local machine and requires dependencies to be on that machine
* Chef has a server and nodes
  * the server contains dependencies and instructions
  * the node communicates with the server to configure itself

I don't know much about Chef-Solo.

!SLIDE left

# The Framework

### Chef Server
* stores data needed for the chef run (more on this later)
* has a web UI
* indexes data about nodes for searching

### Two options:
#### Hosted Chef
* pay OpsWorks to provide the Chef server
* support

#### Open Source Chef
* build your own server
* no support, but also no boundaries
