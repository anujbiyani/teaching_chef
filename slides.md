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

!SLIDE left

# The Guts

Basically two components: the Chef Repo and Cookbooks

### Chef Repo
* analogous to a rails app; it's the driver of your infrastructure
  * knife gem for operating on the chef server
  * cucumber-chef gem for BDD

### Cookbooks
* analogous to a gem, but more integral
  * contains the code necessary to accomplish some specific goal (e.g. install monit, or update the apt-cache)

!SLIDE left

# Initial setup
1. Init the chef-repo
  * https://github.com/opscode/chef-repo
2. Set up the chef server
  * http://docs.opscode.com/install_server.html
3. Connect your chef repository to the server
  * http://docs.opscode.com/chef/install_workstation.html
4. Make your first cookbook
  * TDD it using [ChefSpec](https://github.com/acrmp/chefspec/)
5. Use it in your chef-repo
  * Gems like [Librarian-Chef](https://github.com/applicationsonline/librarian-chef) and [Berkshelf](https://github.com/RiotGames/berkshelf) (both are like Bundler) are useful for managing cookbooks
  * BDD it using [Cucumber-Chef](https://github.com/Atalanta/cucumber-chef/)
      * Runs code against an actual server (EC2 or Vagrant)

!SLIDE left

# Initial setup - continued

6. Run it on a node
  * Use [Knife-EC2](https://github.com/opscode/knife-ec2) to launch nodes
  * Run the chef-client. Two options:
    * ssh onto the target machine
      * `chef-repo $ knife node show NODE_NAME`
      * `chef-repo $ ssh user@ip`
      * `chef-node $ chef-client`
    * use `knife ssh`
      * `bundle exec knife ssh 'name:NODE_NAME' 'chef-client'`
        * useful switches:
          * `-i /path/to/chef.pem`
          * `-x root` run as root user (default is ubuntu)

!SLIDE left

# Anatomy of a Chef Repo

* chef-repo/
  * config/
      * rake.rb
  * cookbooks/
  * data_bags/
  * environments/
  * roles/
  * Rakefile
  * chefignore
  * README.md

!SLIDE left

# Anatomy of a Chef Repo

My additions:
* chef-repo/
  * ...
  * features/
      * step_definitions/
      * support/
          * environments/
              * test.rb
          * env.rb
  * lib/
      * tasks/
  * Cheffile
  * Cheffile.lock
  * Gemfile
  * Gemfile.lock
