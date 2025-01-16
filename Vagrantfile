MACHINES = {
  :"ansible-nginx" => {
              :box_name => "ubuntu/jammy64",
              :box_version => "1.0.0",
              :cpus => 2,
              :memory => 1024,
            }
}
ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'
Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.network "public_network", type: "dchp"
    config.vm.define boxname do |box|
      box.vm.box = boxconfig[:box_name]
      box.vm.box_version = boxconfig[:box_version]
      box.vm.host_name = boxname.to_s
      box.vm.provider "virtualbox" do |v|
        v.memory = boxconfig[:memory]
        v.cpus = boxconfig[:cpus]
      end
    config.vm.provision "ansible", playbook: "./ansible/playbooks/play.yml"

    end
  end
end
