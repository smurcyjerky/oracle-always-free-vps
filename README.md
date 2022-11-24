# oracle-always-free-vps

Larry Ellison will pay for your linux server.

## Introduction

Oracle Cloud Infrastructure will provide you with a 4-core 3GHz ARM machine with 24GB of RAM and 200GB of storage in perpetuity, in their Always Free tier. You also get 10TB/month of free outgoing bandwidth. So you can do some fairly serious stuff on here. Put a minecraft server on it, or maybe host your toy mastodon instance. Contained within this repo is a terraform build that will provision all of those resources into a single server, with a default network. If you want something other than that, fork this repo and/or write your own terraform.

## Disclaimer

* I don't like Oracle and I have no opinion about the quality of their cloud service since I've barely used it. What I do like is getting a hobby-grade linux server completely for free. It's free, and Oracle is within their rights to shut everything down and destroy everything you've done with no notice or recourse. Oracle sales is also super desperate and thirsty. A real life human will both email and call you. You can safely ignore them of course, but don't say I didn't warn you.
* I've made a best effort to limit the provisioned resources to the Always Free tier, but I can't guarantee with 100% certainty that I have succeeded. You are responsible for any charges to your account.

## Usage

### Oracle Cloud account

1. Go to the [Oracle Cloud free tier registration page](https://www.oracle.com/cloud/free/) and create an account. Come back here once you're signed in to the dashboard.
1. Go to the [API Key management](https://cloud.oracle.com/identity/domains/my-profile/api-keys) section of the dashboard and add a new key by clicking the Add API key button and following the onscreen instructions for your preferred method. Make sure you copy and edit the provided `~/.oci/config` file, since terraform will use the settings in this file to communicate with the Oracle Cloud API.

### Tools

1. [Install Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Launch the instance

1. Clone the repo:
    ```
    git clone https://github.com/Fitzsimmons/oracle-always-free-vps.git
    ```
1. Copy `example.tfvars` to `terraform.tfvars` and modify it as needed, likely to just add your own ssh key. The defaults for variables are intended to use the full capacity of the Always Free tier. If this is not what you want, see the full list of variables in `variables.tf`. The region for the instance will be the default region supplied in your `~/.oci/config`.
1. Launch the instance and networking infrastructure:
    ```
    terraform apply -var-file=mastodon.tfvars
    ```
1. Terraform has printed the public IP address of your instance, so you can SSH to it, point DNS at it, etc.

### Now what?

* You could put a minecraft server on it (WIP).
* You could put a [mastodon instance](https://github.com/l3ib/mastodon-ansible) on it.
