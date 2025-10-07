# DataRobot Community



## Foundational AI Application Templates

Application templates provide a code-first, end-to-end pipeline for provisioning DataRobot resources. With customizable components, templates assist you by programmatically generating DataRobot resources that support predictive and generative use cases. The templates include necessary metadata, perform auto-installation of dependencies configuration settings, and seamlessly integrate with existing DataRobot infrastructure to help you quickly deploy and configure solutions.

For detailed information, see our [Documentation](https://docs.datarobot.com/en/docs/workbench/wb-apps/app-templates/index.html). To jump into the code, here our the repositories:

* https://github.com/datarobot-community/talk-to-my-docs-agents
* https://github.com/datarobot-community/talk-to-my-data-agent
* https://github.com/datarobot-community/predictive-content-generator
* https://github.com/datarobot-community/guarded-rag-assistant
* https://github.com/datarobot-community/forecast-assistant
* https://github.com/datarobot-community/predictive-ai-starter

## Declarative API

DataRobot offers a Terraform-native declarative API used to programmatically provision DataRobot entities such as models, deployments, applications, and more. DataRobot has two services for using the declarative API: Pulumi and Terraform. DataRobot recommends using the service that supports your engineering needs. Pulumi is based on Python, while Terraform is based on yaml. Note that application templates are configured for Pulumi by default. See our complete [Product Documentation](https://docs.datarobot.com/en/docs/api/reference/declarative-api.html), our [Pulumi Registry Documentation](https://www.pulumi.com/registry/packages/datarobot/) or our [Terraform Registry Documentation](https://registry.terraform.io/providers/datarobot-community/datarobot/latest).

To jump into the code or contribute, we build our Pulumi provider from our Terraform repo: https://github.com/datarobot-community/terraform-provider-datarobot


**Please note:** The code in these repos is sourced from the DataRobot user community and is not owned or maintained by DataRobot, Inc. You may need to make edits or updates for this code to function properly in your environment.
