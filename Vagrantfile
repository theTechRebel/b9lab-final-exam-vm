Vagrant.configure("2") do |config|
  config.vm.define "dapps" do |dapps|
    dapps.vm.box = "b9lab/eth_2019_03_21"
    dapps.vm.box_url = [
      "https://d3mgdk0lg98lr1.cloudfront.net/truffle-vagrant-package-2019-03-21.box",
      "https://b9-academy-assets.s3.amazonaws.com/public/boxes/truffle-vagrant-package-2019-03-21.box",
      "http://localhost:8080/ipfs/QmQupMizFJqaLBM8RjMzQxfxVuNYuFiipjK3F5dQz5aKJL",
      "http://ipfs.b9lab.com:8080/ipfs/QmQupMizFJqaLBM8RjMzQxfxVuNYuFiipjK3F5dQz5aKJL",
      "http://ipfs.io/ipfs/QmQupMizFJqaLBM8RjMzQxfxVuNYuFiipjK3F5dQz5aKJL"
    ]
    config.vm.box_download_checksum = "fccd0fff1dcf6b10c11df8571cbbbc9e2b6b88567dfd13afb3600c39c24edd8e"
    config.vm.box_download_checksum_type = "sha256"
    # Change from "~/DAPPS" to an existing, and non-encrypted, folder on your host if the mount fails
    dapps.vm.synced_folder "~/DAPPS", "/home/vagrant/DAPPS", nfs: false, nfs_udp: false, create: true
    dapps.vm.network "private_network", type: "dhcp"
    dapps.vm.network :forwarded_port, guest: 8000, host: 8000
    dapps.vm.network :forwarded_port, guest: 8545, host: 8545

    # IPFS
    dapps.vm.network :forwarded_port, guest: 4001, host: 4001
    dapps.vm.network :forwarded_port, guest: 5001, host: 5001
    dapps.vm.network :forwarded_port, guest: 8080, host: 8080

    dapps.vm.provider "virtualbox" do |v|
      host = RbConfig::CONFIG['host_os']

      # Give VM 1/5 system memory & access to all cpu cores on the host
      if host =~ /darwin/
        cpus = `sysctl -n hw.ncpu`.to_i
        # sysctl returns Bytes and we need to convert to MB
        # mem = `sysctl -n hw.memsize`.to_i / 1024 / 1024 / 2
        mem = 3572
      elsif host =~ /linux/
        cpus = `nproc`.to_i
        # meminfo shows KB and we need to convert to MB
        # mem = `grep 'MemTotal' /proc/meminfo | sed -e 's/MemTotal://' -e 's/ kB//'`.to_i / 1024 / 4
        mem = 3572
      else # sorry Windows folks, I can't help you
        cpus = 2
        mem = 3572
      end

      v.customize ["modifyvm", :id, "--memory", mem]
      v.customize ["modifyvm", :id, "--cpus", cpus]
      v.customize ["guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 1000]
    end

    dapps.vm.provision "file", source: "dotscreenrc", destination: "~/.screenrc"

    # dapps.vm.provision :shell, path: "bootstrap.sh"
  end
  # config.ssh.username = "ubuntu"
  # config.ssh.password = "cdce84730f0efe3c8bdf3638"
  # config.ssh.insert_key = false
end
