# Azure Terraform Projects

This repository will hold a series of Azure Terraform projects demonstrating infrastructure-as-code best practices. Each project lives in its own subfolder with its own documentation, variables and modules where appropriate.

## Projects

- `Scalable-Web-App` – A virtual machine scale set fronted by a load balancer in a custom VNet.
- *(future: `aks-cluster`, `kubernetes-eks`, etc.)*

## Structure

```
azure-terraform-projects/
├── Scalable-Web-App/     # first project
│   ├── modules/          # reusable components (optional)
│   ├── envs/             # tfvars by environment
│   ├── scripts/          # helper scripts (user-data.sh, etc.)
│   ├── README.md         # project description and usage
│   ├── *.tf              # terraform configurations
│   └── README.md         # project-specific instructions
├── aks-cluster/          # next project
└── README.md             # this file
```

## Getting started

Each project folder contains a `README.md` that explains how to initialize, plan and apply that particular infrastructure.  Clone the repo, `cd` into a project and follow the instructions there.

> **Note:** Terraform state files (`*.tfstate`) and the `.terraform/` directory are excluded from version control via `.gitignore`.  Remote backends are configured (see individual projects) to keep state secure.
