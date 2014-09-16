A demo on how to stand up a Consul cluster on Vagrant with Ansible.

Versions used:
- Consul 0.4.0
- Ansible 1.7.1
- Vagrant 1.6

### To use:

Install Vagrant and VirtualBox
Install Ansible.  (note that Ansible needs a Mac OS X or Linux host)
Clone this repo
Type this command
    vagrant up
    
Vagrant will create three VMs, then run Ansible against each of them.
To reprovision the boxes, simply do
    vagrant provision
    
To get rid of them and start new, use
    vagrant destroy
    
### Using Consul UI
Consul UI works over Consul's HTTP bindings, which are localhost only.  You can use SSH to make a little tunnel
over to a Vagrant box, though--to do that, use this command:

    vagrant ssh db0 -- -L 8500:127.0.0.1:8500

Then in a browser on your Vagrant host, go to http://127.0.0.1:8500/ui/ to see the Consul UI.