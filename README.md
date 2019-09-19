![Kubernetes Logo](https://raw.githubusercontent.com/kubernetes-sigs/kubespray/master/docs/img/kubernetes-logo.png)

## Provisioning Kubernetes Cluster

#### Requirements (Terraform Server) :
- Python 2.7 (or newer)
- Ansible 2.7 (or newer)
- Jinja 2.9 (or newer)
- Terraform 0.11 .XX

#### Install requirements
    # Install dependencies from ``requirements.txt``
    sudo pip install -r requirements.txt
    
    #install terraform
    wget https://releases.hashicorp.com/terraform/0.11.14/terraform_0.11.14_linux_amd64.zip
    unzip terraform_0.11.14_linux_amd64.zip
    mv terraform /usr/local/bin/
    terraform --version
    
#### Deploy instances
    # login file rc
    source filerc
    
    # exec terraform
    cd kubespray/inventory/cluster1/
    terraform init --var-file=cluster.tf contrib/openstack/
    terraform plan --var-file=cluster.tf contrib/openstack/
    terraform apply --var-file=cluster.tf contrib/openstack/  # deploying instnaces
    
    # verification
    terraform show --var-file=cluster.tf contrib/openstack/
    
#### Create cluster
     # exec ansible
     cd ../.. # change directory to kubespray
     ansible-playbook -i inventory/cluster1/hosts --become cluster.yml
     
     # verification
     ssh -l ubuntu <floating IP master>
     sudo kubectl get nodes
