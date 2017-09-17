Vagrant.configure("2") do |config|
  config.vm.define "dapps" do |dapps|
    dapps.vm.box = "b9lab/eth13"
    dapps.vm.box_url = [
      "https://dst5e0zgbst3t.cloudfront.net/truffle-vagrant-eth-13-package.box",
      "https://b9-academy-assets.s3.amazonaws.com/9-Exam/boxes/truffle-vagrant-eth-13-package.box",
      "http://ipfs.b9lab.com:8080/ipfs/QmU7jS738UsWFDjJZ9STPcDBxPzJipJ1kYLSRSVcQ37FGh",
      "http://ipfs.io/ipfs/QmU7jS738UsWFDjJZ9STPcDBxPzJipJ1kYLSRSVcQ37FGh"
    ]
    config.vm.box_download_checksum = "d0a91725d46d2b6e2c177581045e4c42530506f475947e21b971943d145cc6ab"
    config.vm.box_download_checksum_type = "sha256"
    # Change from "~/DAPPS" to an existing, and non-encrypted, folder on your host if the mount fails
    dapps.vm.synced_folder "~/DAPPS", "/home/vagrant/DAPPS", nfs: true, nfs_udp: false, create: true
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
        mem = 3072
      elsif host =~ /linux/
        cpus = `nproc`.to_i
        # meminfo shows KB and we need to convert to MB
        # mem = `grep 'MemTotal' /proc/meminfo | sed -e 's/MemTotal://' -e 's/ kB//'`.to_i / 1024 / 4
        mem = 3072
      else # sorry Windows folks, I can't help you
        cpus = 2
        mem = 3072
      end

      v.customize ["modifyvm", :id, "--memory", mem]
      v.customize ["modifyvm", :id, "--cpus", cpus]
    end

    dapps.vm.provision "file", source: "dotscreenrc", destination: "~/.screenrc"

    #dapps.vm.provision :shell, path: "bootstrap.sh"
  end
  config.ssh.password = "vagrant"
  config.ssh.insert_key = true
end
