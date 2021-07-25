# Azure Application Insights Terraform module

Application Insights, a feature of Azure Monitor, is an extensible Application Performance Management (APM) service for developers and DevOps professionals. Use it to monitor your live applications. It will automatically detect performance anomalies, and includes powerful analytics tools to help you diagnose issues. This terraform module quickly creates.

## Module Usage

```terraform
# Azurerm Provider configuration
provider "azurerm" {
  features {}
}

module "application-insights" {
  source  = "kumarvna/application-insights/azurerm"
  version = "1.0.0"

  # By default, this module will not create a resource group. Location will be same as existing RG.
  # proivde a name to use an existing resource group, specify the existing resource group name, 
  resource_group_name = "rg-shared-westeurope-01"

  application_insights_config = {
    mydemoappinsightworkspace = {
      application_type = "web"
    }
  }
}
```

## **`application_insights_config`** - Application Insights Settings

`application_insights_config` block helps you setup the application environment and accept following Keys

| Name | Description
|--|--
`name`|Specifies the name of the Application Insights component
`application_type`|Specifies the type of Application Insights to create. Valid values are `ios` for iOS, `java` for Java web, `MobileCenter` for App Center, `Node.JS` for Node.js, `other` for General, `phone` for Windows Phone, `store` for Windows Store and `web` for ASP.NET. Please note these values are case sensitive; unmatched values are treated as ASP.NET by Azure. Changing this forces a new resource to be created.
`daily_data_cap_in_gb`|Specifies the Application Insights component daily data volume cap in GB.
`daily_data_cap_notifications_disabled`|Specifies if a notification email will be send when the daily data volume cap is met. Defaults to `false`
`retention_in_days`|Specifies the retention period in days. Possible values are `30`, `60`, `90`, `120`, `180`, `270`, `365`, `550` or `730`. Defaults to `90`.
`sampling_percentage`|Specifies the percentage of the data produced by the monitored application that is sampled for Application Insights telemetry. Defaults to `100`.
`disable_ip_masking`|By default the real client ip is masked as `0.0.0.0` in the logs. Use this argument to disable masking and log the real client ip. Defaults to `false`.

