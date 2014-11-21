Vagrant + KVM
-------------

:Sauce: https://github.com/adrahon/vagrant-kvm/blob/master/INSTALL.md

::

	yum -y install vim zsh qemu-kvm libvirt libvirt-daemon-kvm redir policycoreutils-python

	curl -LO 'https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.5_x86_64.rpm'
	rpm -i vagrant_1.6.5_x86_64.rpm

	semanage fcontext -a -t virt_image_t "~/.vagrant.d/tmp/storage-pool(/.*)?"
	semanage fcontext -a -t virt_image_t "~/.vagrant.d/boxes(/.*)?"

	cat > /etc/polkit-1/localauthority/50-local.d/50-libvirt-remote-access.pkla <<EOF
	[libvirt Management Access]
	Identity=unix-user:username
	Action=org.libvirt.unix.manage
	ResultAny=yes
	ResultInactive=yes
	ResultActive=yes
	EOF

	/etc/init.d/libvirtd restart

	yum -y install gcc make rubygem-rake ruby-devel libvirt-devel libxslt-devel libxml2-devel

	vagrant plugin install vagrant-kvm


cd Vagrant
NUM_INSTANCES=1 START_IP=210 RAM_PER_INSTANCE=1024 vagrant up
