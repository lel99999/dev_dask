Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = "1024"
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
  end
# config.trigger.after :up do |trigger|
#   run "subscription-manager register --username <username> --password <password> --auto-attach
#   trigger.name = "After-Up Trigger ..."
#   trigger.info = "Trigger Execution ..."
#   trigger.run = { path:"subscription-manager register --username <username> --password <password> --auto-attach"}
# end

  config.vm.define "daskRH7" do |daskRH7|
#   daskRH7.vm.box = "generic/rhel7"
    daskRH7.vm.box = "RH7.5_baserepo"
    #daskRH7.vm.box = "javier-lopez/rhel-7.4"
    #daskRH7.vm.box = "xianlin/rhel-7.4"
    daskRH7.vm.hostname = "daskRH7"
    daskRH7.vm.network "private_network", ip: "192.168.60.141"
    daskRH7.vm.provision "shell", :inline => "sudo echo '192.168.60.141 daskRH7.local daskRH7' >> /etc/hosts"
    daskRH7.vm.provision "ansible" do |ansible|
      ansible.playbook = "deploy_dask.yml"
      ansible.inventory_path = "vagrant_hosts"
      #ansible.tags = ansible_tags
      #ansible.verbose = ansible_verbosity
      #ansible.extra_vars = ansible_extra_vars
      #ansible.limit = ansible_limit
    end
  end
# config.trigger.before :destroy do |trigger|
#   run "rm -Rf /tmp/abc/*"
    # subscription-manager remove --all
    # subscription-manager unregister
    # subscription-manager clean
#   trigger.name = "Destroy Trigger ..."
#   trigger.info = "Destroy Trigger Execution ..."
#   trigger.run = { path: "subscription-manager remove --all"}
#   trigger.run = { path: "subscription-manager unregister"}
#   trigger.run = { path: "subscription-manager clean"}
# end
end
