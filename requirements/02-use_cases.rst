Typical use cases:

1.Ensure Bandwidth

1.1 Use case description:

It's critical to ensure compute nodes with enough bandwidth to run VMs,
especially those who run network-sensitive applications. When the VMs of a host
are running network-sensitive applications  such as Web servers, Ftp servers and vEPC ( a typical telecom application), as a new user, he may raise a request to avoid starting a new network-sensitive VM on the busy host.

In this use case, the VIM should detect that the busy host is not suitable for thenew network-sensitive VM. In other words, the busy host can be filtered when it has not enough bandwith for the new VM. So the VIM should take bandwidth into consideration when the scheduler is allocatinga VM. 
For each host, the VIM should know how much bandwidth is consumed already. Once a user raises a new VM request, he should also define bandwidth restrict for the VM.  
Once a VM is allocated in a host, the host should subtract the new VM's
bandwidth and update its current available bandwidth. 
Once the current available bandwidth is collected, from the scheduler side, it
should support bandwidth filter to filter the hosts that has not enough
bandwidth and allocate a host that is viable for the user's request. In this
way, the scheduler can use the bandwidth infomation to allocate a host with
enough bandwidth for the user.

1.2 Gap:
    
    OpenStack should support collecting network bandwidth of hosts and existed
    instances. In this way, the scheduler can utilize the information to
    schedule a new network-sensitive VM in a better way.

    Collecting network bandwidth of hosts and existed instances, and creating
    new filter possibly named BandwidthFilter that provide the ability to
    filter hosts based bandwidth requested by the instance.
    The patch https://review.openstack.org/#/c/44007/ added network monitor for compute, which collect network related metrics like the rates of packets sent or received for the compute node. But network bandwidth collection, including physical bandwidth and instance bandwidth used was not taken into account.

