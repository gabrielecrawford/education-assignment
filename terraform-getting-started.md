# Getting Started with Terraform

Terraform is HashiCorp's code tool, it allows to define and provision infrastructure as code (IaC).

To install Terraform, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the appropriate file for your system.

With Terraform installed, you can now create infrastructure as code (IaC).

Create a directory named `terraform-demo`

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

In the working directory, create a file named `main.tf`

```shell
$ touch main.tf
```

Paste the below Terraform configuration and save the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Run the `init` command to initialize Terraform, the provider will be installed. 

```shell
$ terraform init
```

If there are no errors, run the `apply` command to provision the resources.

```shell
$ terraform apply
```

The command will take up to a few minutes to run, and will display a message indicating that the resource was created.

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Type `yes` when asking for confirmation and hit ENTER. Terraform will destroy all the resources created.
