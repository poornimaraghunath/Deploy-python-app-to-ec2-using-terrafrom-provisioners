# Deploy-python-app-to-ec2-using-terrafrom-provisioners

Provisioner : They are a mechanism for running scripts or commands on local or remote resources during the resource creation or destruction process. 

Provisioners can be used to configure, bootstrap, or perform any necessary setup on the target resources after they have been created

Terraform supports several type of provsioners.

1. Local-exec Provisioner:

Executes commands on the machine running Terraform.
Useful for running scripts or commands locally.

eg. 

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  provisioner "local-exec" {
    command = "echo 'Hello, World!'"
  }
}


2. Remote-exec Provisioner:

Connects to the created resource using SSH or WinRM and executes commands.
Typically used for configuring remote servers.


resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  provisioner "remote-exec" {
    inline = ["echo 'Hello, World!'"]
  }
}


3. File Provisioner:

Copies files or directories from the machine running Terraform to the target resource.
Useful for copying configuration files or scripts.

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  provisioner "file" {
    source      = "path/to/local/file.txt"
    destination = "/path/on/target"
  }
}


4. Chef Provisioner:

Configures resources using Chef recipes.
Requires a Chef server.



resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  provisioner "chef" {
    server_url   = "https://example-chef-server.com"
    node_name    = "example-node"
    run_list     = ["recipe[example-cookbook::default]"]
  }
}

5. Puppet Provisioner:

Configures resources using Puppet manifests.
Requires a Puppet master.


resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  provisioner "puppet" {
    server = "https://example-puppet-master.com"
    manifest_file = "path/to/manifest.pp"
  }
}


Note: Command for generating ssh key on local machine is mentioned below
 ssh-keygen -t rsa 


