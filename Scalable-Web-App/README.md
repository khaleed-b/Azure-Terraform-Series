# Scalable Web App (Terraform)

This project deploys a simple scalable web application environment on Azure using Terraform.

It creates:

* A virtual network (VNet)
* A virtual machine scale set (VMSS) with custom `user-data.sh` provisioning
* An autoscale rule (defined in `autoscale.tf`)
* A load balancer (implicit in the VMSS module)

## Prerequisites

* [Terraform 1.9+](https://www.terraform.io/downloads.html)
* Azure CLI logged in (`az login`)
* An Azure Storage Account and container for remote state (configured in `backend.tf`).

## Files

* `main.tf` – your primary configuration (in this project it's split across multiple `*.tf` files)
* `vnet.tf`, `vmss.tf`, `autoscale.tf`, `provider.tf`, `backend.tf` – resource definitions
* `user-data.sh` – script executed by the VMSS instances
* `.terraform.lock.hcl` – provider lock file (commit this)

## Usage

```powershell
git clone https://github.com/<your‑username>/azure-terraform-projects.git
cd azure-terraform-projects/Scalable-Web-App
terraform init -backend-config="resource_group_name=halad-resources" \
               -backend-config="storage_account_name=haladstorageaccount" \
               -backend-config="container_name=tfstate"
terraform plan -out=plan.tfplan
terraform apply "plan.tfplan"
```

For a development environment you could add a `envs/dev.tfvars` and pass `-var-file=envs/dev.tfvars`.

## Screenshot

Include a screenshot of the Azure Portal showing the deployed resources, e.g. a VMSS instance view. Add the image file here and reference it below:

```
![VMSS in Azure](./screenshots/vmss.png)
```

## What *not* to commit

* Any `*.tfstate` or `*.tfstate.backup` files – they contain sensitive outputs (IP addresses, tokens).
* The `.terraform/` directory – it holds the provider plugins and local state.
* The `errored.tfstate` file shown above – remove it before committing.
* Secrets, passwords, or any values explicitly entered in the configuration. Use variables or environment variables instead.

## Next steps

- Clean up the directory (`rm errored.tfstate` and delete `.terraform/` before pushing).
- Add `gitignore` as shown below.
- Push to a new GitHub repo and tag a release when stable.
- Reuse any parts of this project in future ones by moving common resources into `modules/`.
