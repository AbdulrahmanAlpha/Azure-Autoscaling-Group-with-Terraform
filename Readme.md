# Azure Autoscaling Group with Terraform

This project demonstrates how to create an autoscaling group for a web application on Azure using Terraform. The autoscaling group automatically adjusts the number of instances based on CPU usage, ensuring that the application can handle varying levels of traffic. The project uses Azure resources such as a virtual network, load balancer, and availability set to create a scalable infrastructure, and includes Terraform configuration files for easy deployment.

## Prerequisites

Before you begin, you will need the following:

- An Azure subscription
- A service principal with Contributor role access to the subscription. Follow these steps to create a service principal:
  1. From the Azure portal, navigate to Azure Active Directory.
  2. Select App registrations and then select New registration.
  3. Enter a name for the application, select "Accounts in this organizational directory only" as the supported account type, and enter the redirect URI.
  4. Select Register to create the application.
  5. Record the Application (client) ID and Directory (tenant) ID.
  6. Select Certificates & secrets and then select New client secret.
  7. Enter a description for the secret, select an expiration date, and select Add.
  8. Record the client secret value.

## Getting Started

To deploy the autoscaling group, follow these steps:

1. Clone the repository to your local machine:

```
git clone https://github.com/your_username/azure-autoscaling-group.git
```

2. Change directory to the cloned repository:

```
cd azure-autoscaling-group
```

3. Create a `terraform.tfvars` file and set the following variables:

```
subscription_id = "<your_subscription_id>"
client_id       = "<your_client_id>"
client_secret   = "<your_client_secret>"
tenant_id       = "<your_tenant_id>"
```

4. Initialize Terraform:

```
terraform init
```

5. Plan the deployment:

```
terraform plan
```

6. If the plan looks good, apply the deployment:

```
terraform apply
```

7. Wait for the deployment to complete.

## Architecture

The autoscaling group is deployed using the following Azure resources:

- Resource group: A container for the autoscaling group resources.
- Virtual network: A logical representation of the network that the autoscaling group instances are connected to.
- Subnet: A segment of the virtual network that the autoscaling group instances are assigned to.
- Load balancer: Distributes traffic evenly across the autoscaling group instances.
- Public IP address: Provides a public IP address for the load balancer.
- Network security group: Specifies inbound and outbound traffic rules for the autoscaling group instances.
- Availability set: Ensures that the autoscaling group instances are distributed across multiple fault domains.
- Virtual machine scale set: Defines the autoscaling group and its instances. The scale set automatically adjusts the number of instances based on CPU usage.

## Autoscaling Configuration

The autoscaling group scales based on CPU usage. If the CPU usage is greater than 70% for a sustained period of time, the autoscaling group adds one instance. If the CPU usage is less than 80% for a sustained period of time, the autoscaling group removes one instance. The autoscaling group has a minimum of 2 instances and a maximum of 5 instances.

## Conclusion

This project demonstrates how to create an autoscaling group for a web application on Azure using Terraform. The autoscaling group ensures that the application can handle varying levels of traffic by automatically adjusting the number of instances based on CPU usage. The project uses Azure resources such as a virtual network, load balancer, and availability set to create a scalable infrastructure, and includes Terraform configuration files for easy deployment.