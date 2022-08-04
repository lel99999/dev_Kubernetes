Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = "1024"
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
  end

  config.vm.define "kubemaster" do |kubemaster|
#   kubemaster.vm.box = "bento/centos-6.10"
#   kubemaster.vm.box = "clouddood/RH7.5_baserepo"
    kubemaster.vm.box = "clouddood/RH7.9_infra"
    kubemaster.vm.host_name = "kubemaster.test.dev"
    kubemaster.vm.network "private_network", ip: "192.168.60.40"
    kubemaster.ssh.forward_agent = true

    kubemaster.vm.provision "ansible" do |ansible|
      ansible.playbook = "deploy_kubemaster.yml"
#     ansible.playbook = "deploy_BaseSystem.yml"
      ansible.inventory_path = "vagrant_hosts"
#     ansible.extra_vars = {:zookeeper_id => "#{id}"}
#    ansible.tags = ansible_tags
#    ansible.verbose = ansible_verbosity
#    ansible.extra_vars = ansible_extra_vars
#    ansible.limit = ansible_limit
    end
  end
  config.vm.define "kubeworker" do |kubeworker|
#   kubeworker.vm.box = "bento/centos-6.10"
#   kubeworker.vm.box = "clouddood/RH7.5_baserepo"
    kubeworker.vm.box = "clouddood/RH7.9_infra"
    kubeworker.vm.host_name = "kubeworker.test.dev"
    kubeworker.vm.network "private_network", ip: "192.168.60.41"
    kubeworker.ssh.forward_agent = true

    kubeworker.vm.provision "ansible" do |ansible|
      ansible.playbook = "deploy_kubeworker.yml"
      ansible.inventory_path = "vagrant_hosts"
#     ansible.extra_vars = {:zookeeper_id => "#{id}"}
#    ansible.tags = ansible_tags
#    ansible.verbose = ansible_verbosity
#    ansible.extra_vars = ansible_extra_vars
#    ansible.limit = ansible_limit
    end
  end
end
