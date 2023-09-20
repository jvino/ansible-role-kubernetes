
Kubernetes Role
=======================

This ansible role installs a [Kubernetes](https://kubernetes.io/) cluster.

Role Variables
----------------

The variables that can be passed to this role and a brief description about them are as follows.

    # Version to install or latest
    kube_version: 1.28.1
	# Type of node front or wn
	kube_type_of_node: front
	# IP address or name of the Kube front node
	kube_server: "{{ ansible_default_ipv4.address }}"
	# Security Token
	kube_token: "kube01.{{ lookup('password', '/tmp/tokenpass chars=ascii_lowercase,digits length=16') }}"
	# Token TTL duration (0 do not expire)
	kube_token_ttl: 0
	# POD network cidr
	kube_pod_network_cidr: 10.244.0.0/16
	# Kubelet extra args
	kubelet_extra_args: ''
	# Flag to set HELM to be installed
	kube_install_helm: true
	# Deploy the Dashboard
	kube_deploy_dashboard:  true
	# value to pass to the kubeadm init --apiserver-advertise-address option
	kube_api_server: 0.0.0.0
	# A set of git repos and paths to be applied in the cluster. Following this format:
	# kube_apply_repos: [{repo: "https://github.com/kubernetes-incubator/metrics-server", version: "master", path: "deploy/1.8+/"}]
	kube_apply_repos: []
	# Flag to set Metrics-Server to be installed
	kube_install_metrics: false
	# Flag to enable GPU support
	enable_gpu: false
	# Name (and version) of the Ansible role to include if `enable_gpu == true'
	gpu_support_role: git+https://baltig.infn.it/infn-cloud/ansible-role-gpu-support,vX.Y.Z

Dependencies
------------

- ansible-role-gpu-support (if `enable_gpu == true`)

Example Playbook
----------------

This an example of how to install this role in the front-end node:

And in the WNs:
