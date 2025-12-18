curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash
wget https://github.com/derailed/k9s/releases/latest/download/k9s_linux_amd64.deb && apt install ./k9s_linux_amd64.deb && rm k9s_linux_amd64.deb
    curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash

k3d
Usage:
  k3d [flags]
  k3d [command]

Available Commands:
  cluster      Manage cluster(s)
  completion   Generate completion scripts for [bash, zsh, fish, powershell | psh]
  config       Work with config file(s)
  help         Help about any command
  image        Handle container images.
  kubeconfig   Manage kubeconfig(s)
  node         Manage node(s)
  registry     Manage registry/registries
  version      Show k3d and default k3s version

Flags:
  -h, --help         help for k3d
      --timestamps   Enable Log timestamps
      --trace        Enable super verbose output (trace logging)
      --verbose      Enable verbose output (debug logging)
      --version      Show k3d and default k3s version

Use "k3d [command] --help" for more information about a command.

k3d cluster create --config cluster-config.yaml

k3d cluster create mycluster --servers 1 --agents 10 --k3s-server-arg "--no-deploy=traefik"

k3d cluster create mycluster --servers 1 --agents 10 --k3s-server-arg "--no-deploy=traefik" \
--k3s-server-arg "--kubelet-arg=--max-pods=100" \
--k3s-agent-arg "--kubelet-arg=--max-pods=100" \
--agents-memory 2GB --agents-cpu 2

 k3d cluster create mycluster --servers 3 --agents 6 --api-port 6443

 kubectl config view

 kubectl config get-clusters

kubectl config get-users   
NAME
admin@k3d-mycluster
dev-cluster
my-cluster
rancher-desktop

kubectl config get-clusters
rancher-desktop
dev-cluster
k3d-mycluster
my-cluster



curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version --client

sudo mv ./kubectl /usr/local/bin/kubectl

curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash

k3d --version

k3d cluster create mycluster

curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"

k3d cluster create mycluster
--servers 3
--agents 10
--servers-memory 2048MB \ # 2GB per server --servers-cpu 1.5 \ # 1.5 CPU per server --agents-memory 1024MB \ # 1GB per worker --agents-cpu 0.5 \ # 0.5 CPU per worker --api-port 6443 \ # Port API Kubernetes --wait # Tunggu hingga klaster siap


kubectl create deployment nginx --image=fuad1983/web
kubectl autoscale deployment nginx --cpu-percent=50 --min=2 --max=6

docker run -itd -p 3003:3000 --name ntop  --net=host junquera/ntopng --memory 512m --cpus 0.5 -i eth0

# Determine cluster name used by current context
cluster=$(kubectl config view --minify -o jsonpath='{.contexts[0].context.cluster}')

# 1) Set cluster server to localhost (recommended)
kubectl config set-cluster "$cluster" --server=https://127.0.0.1:6443

# 2) Or regenerate/merge kubeconfig from k3d (replace mycluster)
k3d kubeconfig merge mycluster
# or to overwrite:
k3d kubeconfig get mycluster > ~/.kube/config

# 3) Temporary (not recommended) — skip TLS verification
kubectl config set-cluster "$cluster" --insecure-skip-tls-verify=true
