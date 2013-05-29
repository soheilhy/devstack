Introduction
============
This is a devstack fork for seamless installation of the FlowVisor Quantum
plugin.

Prerequisites
=============
- Install
[FlowVisor](https://github.com/OPENNETWORKINGLAB/flowvisor/wiki/Installation-from-Source)
- You might also want to install and run multiple OpenFlow controllers
  for testing purposes.

Installation
============

Create localrc
--------------
The first step is to create your localrc.

This is a sample localrc file:

    # A sample localrc for flowvisor.

    # Sets the active quantum plugin to flowvisor.
    Q_PLUGIN=flowvisor

    # FlowVisor specific configs.
    # Note: These are all default values. If your config is the same you don't
    # need to set them in your localrc.

    # FlowVisor Host
    FV_HOST=localhost

    # FlowVisor JSON RPC Port.
    FV_JSON_RPC_PORT=8081

    # FlowVisor OpenFlow port.
    FV_OPENFLOW_PORT=6633

    # FlowVisor admin username.
    FV_USERNAME=fvadmin

    # FlowVisor admin password
    FV_PASSWORD=

    # ONL quantum and horizon forks.
    QUANTUM_REPO=git@github.com:OPENNETWORKINGLAB/quantum.git
    QUANTUM_BRANCH=devel/flowvisor

    HORIZON_REPO=git@github.com:OPENNETWORKINGLAB/horizon.git
    HORIZON_BRANCH=devel/flowvisor

    # Services for the flowvisor plugin.
    disable_service n-net
    enable_service q-svc
    enable_service q-dhcp
    enable_service q-l3
    enable_service q-meta
    enable_service quantum
    enable_service flowvisor

Run stack.sh
------------
After creating your localrc, you need to run `./stack.sh`. If you see
the following message, openstack is successfully installed:

    Horizon is now available at http://YOUR_IP/
    Keystone is serving at http://YOUR_IP:5000/v2.0/
    Examples on using novaclient command line is in exercise.sh
    The default users are: admin and demo
    The password: YOUR_PASSWORD
    This is your host ip: YOUR_IP
    stack.sh completed in SOME_SECONDS seconds.


Usage
=====
* Goto your browser and open http://YOUR_IP/
* Goto the project tab, on the left hand side.
* Select the demo project.
    *  Goto "Manage Network / Networks"
    *  Click on "Edit Network" button for the private network.
    *  Add the private network's controller listening address (e.g.,
       192.168.0.2:6666).
    *  Then save changes.
* Select the admin project.
    *  Goto "Manage Network / Networks"
    *  Click on "Edit Network" button for the public network.
    *  Add the public network's controller listening address (e.g.,
       192.168.0.2:6667). **Note**: It should be different than the
       private network's controller.
    *  Then save changes.
* Select the demo project again, and launch a VM.

** Note: ** If you're running devstack inside a VM, make sure you
have configured NAT properly. For instance, on a linux vm with one
bridged interface run to setup NAT:

    sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

Ideas
=====
- We can install FlowVisor inside devstack for user convenience.
