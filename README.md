# Ansible

[Ansible](https://www.ansible.com/) is an open-source automation platform that simplifies IT tasks such as configuration management, application deployment, and cloud provisioning. It uses a simple, human-readable language (YAML) to describe automation jobs, allowing for easy and efficient management of IT infrastructure. Ansible operates without the need for an agent, utilizing SSH for communication, which streamlines the setup process and reduces overhead. Its modular architecture supports a wide range of modules for different systems and applications, making it highly versatile and adaptable to various environments. Overall, Ansible enhances operational efficiency, consistency, and scalability in managing complex IT workflows.

## Ansible vs Terraform

Ansible and Terraform are both powerful tools used for automation in IT environments, but they serve different purposes and have distinct features. Ansible is better at managing configuration while Terraform is more suited for infrastructure provisioning. Therefore, it is very common to see both tools being used together in a complementary manner to achieve comprehensive automation across the entire IT stack.

## Installation

To install Ansible, you can use the package manager of your choice. For example, on MacOS, you can install Ansible using the following command:

```bash
brew install ansible
```

Please, refer to the official [Ansible documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) for detailed installation instructions on different operating systems.

## Ansible Playbooks

Ansible playbooks are YAML files that define a series of tasks to be executed by Ansible on remote hosts. They are used to automate configuration management, application deployment, and other IT tasks. Playbooks are written in a human-readable format, making them easy to understand and maintain. You can find an example of a simple Ansible playbook in the `playbook.yaml` file in this repository.

## Ansible Galaxy

[Ansible Galaxy](https://galaxy.ansible.com/) is a hub for finding, reusing, and sharing Ansible content. It contains thousands of roles, playbooks, and collections contributed by the Ansible community. You can search for content based on your requirements and easily integrate it into your automation workflows. Ansible Galaxy helps accelerate development by providing pre-built solutions that can be customized and extended to meet your specific needs.

In this repo, Ansible Galaxy is being used to separate the playbooks into roles which can be found in the `roles` directory.

## Running Locally

1. Clone the repository
1. Run `docker compose up -d`
1. Access the `node-01` and `node-02` containers and start the SSH service

   ```bash
   docker exec -it node-0x bash
   service ssh start
   ```

1. Access the `control` container and generate the SSH key

   ```bash
   docker exec -it control bash
   ssh-keygen
   ```

1. Copy the SSH key to the `node-01` and `node-02` containers

   ```bash
   ssh-copy-id -i ~/.ssh/id_rsa.pub root@node-0x
   ```

1. Run the Ansible playbook

   ```bash
   cd /root/ansible && ansible-playbook -i hosts ./roles/main.yaml
   ```

And you should be able to access http://localhost:8080 or http://localhost:8081 to see the the node app response.
