# opentelemetrydemo_on_k3s_vagrant_libvirt_ansible

Vagrant-libvirt setup that creates a VM with a [k3s](k3s.io) Kubernetes cluster.
In the cluster, the [OpenTelemetry
Demo](https://opentelemetry.io/docs/kubernetes/helm/demo/) is installed.

Default OS is openSUSE Leap 15.5, but that can be changed in the Vagrantfile.
Please be aware, that this might break the Ansible provisioning.

## Vagrant

1. You need `vagrant`, obviously. And `git`. And Ansible...
1. Fetch the box, per default this is `opensuse/Leap-15.5.x86_64`, using
   `vagrant box add opensuse/Leap-15.5.x86_64`.
1. Make sure the git submodules are fully working by issuing
   `git submodule init && git submodule update`
1. Run `vagrant up`
1. Open the "WebShop" at the URL that Ansible printed at the end and do some
   shopping.
1. Open Grafana, Locust or the Jaeger UI at the URLs that Ansible printed at the
   end.
1. Party!

## Disabling the Ansible provisioning

In case you do not want Ansible to install k3s or the OpenTelemetry Demo
(because you want to install it yourself), just comment out the following lines
in the `Vagrantfile`:

```
    node.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "ansible/playbook-vagrant.yml"
    end # node.vm.provision
```

## Cleaning up

The VMs can be torn down after playing around using `vagrant destroy`. This will
also remove the kubeconfig file `ansible/k3s-kubeconfig`.
