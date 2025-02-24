+++
date = '2020-06-09T16:18:50-05:00'
draft = false
title = 'Terraform Secrets'
+++
---
Terraform is a great tool for automating your infrastructure.  We have been using it recently to capture some OpenStack infrastructure as code (IaC).  I am reading through the 2nd edition of _Terraform: Up & Running_ by Yevgeniy Brikman.  I just finished reading chapter 3 which is about managing your Terraform state.  One of the sidebars was about secrets.

One of the best practices with IaC is to make sure your secrets never wind up in your source repositories.  Terraform has the ability to accept environment variables as parameters which would certainly make life easier if we put them in our shell startup script.  But how can we set up environment variables as Terraform parameters without storing our passwords in plain text in say `.zshrc` or in our shell history?  A solution proposed in chapter 3 is to use a tool like http://passwordstore.org to secure your secrets at rest.

For this solution, you will need a GPG key, the password manager from http://passwordstore.org. You will modify your `.zshrc` to invoke new environment variables and modify your .tf files to use those variables.

If you need a gpg key run this command and follow the prompts:
```
gpg --full-generate-key
```

Choose RSA + RSA, use key size 4096, set the key expiry and enter your details.

You will get some output that looks like this:
```
gpg: key 866F4C51D21B52CA marked as ultimately trusted
gpg: directory '/Users/neilderraugh/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/Users/neilderraugh/.gnupg/openpgp-revocs.d/9BCFAF34DC248F0C3BF998A03FC9BC700DD0A19A.rev'
```

Next step install _pass: the standard unix password manager_.  Note that you'll need the key id (`866F4C51D21B52CA`)from the previous step.
```
brew install pass

pass init "866F4C51D21B52CA"

pass insert openstack_password "some password"
```

Add the Terraform environment variables you want to your `.zshrc`:
```
export TF_VAR_openstack_password=$(pass openstack_password)
export TF_VAR_openstack_user_name=service_account_user
export TF_VAR_openstack_auth_url=http://some_url:5000/v3
export TF_VAR_openstack_tenant_id=some_id
```

And then modify your `var.tf` to leverage those new environment variables including the secrets:
```
variable "openstack_user_name" {
  type=string
}

variable "openstack_password" {
  type=string
}

variable "openstack_auth_url" {
  type=string
}

variable "openstack_tenant_id" {
  type=string
}
```

Your `main.tf` will look something like this
```
provider "openstack" {
  user_name   = var.openstack_user_name
  tenant_name = var.openstack_user_name
  password    = var.openstack_password
  auth_url    = var.openstack_auth_url
  tenant_id   = var.openstack_tenant_id
  region      = "RegionOne"
}
...
```
Safety first kids!