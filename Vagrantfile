
desired_variables = [
  'ADAPTER_NAME',
  'BOX_URL'
]


if File.exists?('.env')
  File.foreach('.env') do |line|
    if line =~ /^(.+)=(.+)$/ && desired_variables.include?($1)
      ENV[$1] = $2.strip
    end
  end
end

Vagrant.configure("2") do |config|
  adapter_name = ENV['ADAPTER_NAME']
  box_url = ENV['BOX_URL']

  
  config.vm.box = "opnsense"
  config.vm.box_url = box_url

  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"  
    vb.cpus = 2
  end

  
  config.vm.network "public_network", bridge: adapter_name, auto_config: false, adapter: 1  
  config.vm.network "public_network", bridge: adapter_name, auto_config: false, adapter: 2  
end
