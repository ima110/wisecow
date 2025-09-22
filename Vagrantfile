Vagrant.configure("2") do |config|
  # Ubuntu 22.04 LTS (Jammy Jellyfish)
  config.vm.box = "ubuntu/jammy64"

  # Configuring a private network 
  config.vm.network "private_network", ip: "192.168.56.10"

  # Allocating resources 
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048" # 2GB RAM
    vb.cpus = 2        # 2 CPUs
  end

  # Provision the VM: 
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update

    # Installing prerequisites for the Wisecow app
    apt-get install -y cowsay fortune netcat

    # Installing Docker prerequisites
    apt-get install -y ca-certificates curl gnupg lsb-release

    # Adding Docker's official GPG key and seting up the stable repository
    mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    # Installing Docker Engine
    apt-get update
    apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

    # Adding the 'vagrant' user to the 'docker' group to run docker commands without sudo
    usermod -aG docker vagrant

    # Installing kubectl (Kubernetes CLI)
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
    rm kubectl

    # Installing Minikube (a tool to run a local Kubernetes cluster)
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    install minikube-linux-amd64 /usr/local/bin/minikube
    rm minikube-linux-amd64

    # Start Minikube (this will be done manually later, but the binary is ready)
    # "To start minikube, run: minikube start --driver=docker"

    echo "--------------------------------------------------"
    echo " Provisioning complete!"
    echo " Please run 'vagrant ssh' to connect to the VM."
    echo " Then, navigate to your project directory."
    echo "--------------------------------------------------"
  SHELL
end