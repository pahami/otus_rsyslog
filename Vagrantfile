Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-22.04"
    config.vm.provider :virtualbox do |v|
        v.memory = 1024
        v.cpus = 1
    end
    boxes = [
        {
            :name => "web",
            :ip => "192.168.56.10",
        },
        {
            :name => "log",
            :ip => "192.168.56.15",
        },
        {
            :name => "client",
            :ip => "192.168.56.11",
        }
    ]
    boxes.each do |opts|
        config.vm.define opts[:name] do |config|
            config.vm.hostname = opts[:name]
            config.vm.network "private_network", ip: opts[:ip]
        end
        if opts[:name] == boxes.last[:name]
          config.vm.provision "ansible" do |ansible|
#            ansible.verbose = "vvv"      # Уровень отображения процессов выполнения ansible
            ansible.playbook = "provision/playbook.yml"
            ansible.become = "true"
            ansible.limit = "all"
          end
        end
    end
end