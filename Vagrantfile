desired_variables = [
  'PUBLIC_IP',
  'PRIVATE_IP',
  'ISO_PATH'
]

if File.exists?('.env')
  File.foreach('.env') do |line|
    if line =~ /^(.+)=(.+)$/ && desired_variables.include?($1)
      ENV[$1] = $2.strip
    end
  end
end

Vagrant.configure("2") do |config|
  public_ip = ENV['PUBLIC_IP']
  private_ip = ENV['PRIVATE_IP']
  iso_path = ENV['ISO_PATH']

  config.vm.define "opnsense" do |opnsense|
    opnsense.vm.box = "generic/freebsd12"  

    opnsense.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
      vb.customize ["modifyvm", :id, "--nictype1", "virtio"]
      vb.customize ["modifyvm", :id, "--nictype2", "virtio"]
      vb.customize ["modifyvm", :id, "--boot1", "dvd"]
      vb.customize ["storageattach", :id, "--storagectl", "IDE Controller", "--port", "1", "--device", "0", "--type", "dvddrive", "--medium", iso_path]
    end

    
    opnsense.vm.network "public_network", bridge: "en0: Ethernet 1", ip: public_ip

    
    opnsense.vm.network "public_network", bridge: "en0: Ethernet 1", ip: private_ip

    
    opnsense.ssh.insert_key = false
    opnsense.vm.provision "shell", inline: <<-SHELL
      echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
      echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
      service sshd restart
      echo 'root:opnsense' | chpasswd
    SHELL
  end
end
