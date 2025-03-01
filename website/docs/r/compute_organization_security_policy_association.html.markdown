---
# ----------------------------------------------------------------------------
#
#     ***     AUTO GENERATED CODE    ***    Type: MMv1     ***
#
# ----------------------------------------------------------------------------
#
#     This file is automatically generated by Magic Modules and manual
#     changes will be clobbered when the file is regenerated.
#
#     Please read more about how to change this file in
#     .github/CONTRIBUTING.md.
#
# ----------------------------------------------------------------------------
subcategory: "Compute Engine"
page_title: "Google: google_compute_organization_security_policy_association"
description: |-
  An association for the OrganizationSecurityPolicy.
---

# google\_compute\_organization\_security\_policy\_association

An association for the OrganizationSecurityPolicy.

~> **Warning:** This resource is in beta, and should be used with the terraform-provider-google-beta provider.
See [Provider Versions](https://terraform.io/docs/providers/google/guides/provider_versions.html) for more details on beta resources.

To get more information about OrganizationSecurityPolicyAssociation, see:

* [API documentation](https://cloud.google.com/compute/docs/reference/rest/beta/organizationSecurityPolicies/addAssociation)
* How-to Guides
    * [Associating a policy with the organization or folder](https://cloud.google.com/vpc/docs/using-firewall-policies#associate)

## Example Usage - Organization Security Policy Association Basic


```hcl
resource "google_folder" "security_policy_target" {
  provider     = google-beta
  display_name = "tf-test-secpol-%{random_suffix}"
  parent       = "organizations/123456789"
}

resource "google_compute_organization_security_policy" "policy" {
  provider = google-beta
  display_name = "tf-test%{random_suffix}"
  parent       = google_folder.security_policy_target.name
}

resource "google_compute_organization_security_policy_rule" "policy" {
  provider = google-beta
  policy_id = google_compute_organization_security_policy.policy.id
  action = "allow"

  direction = "INGRESS"
  enable_logging = true
  match {
    config {
      src_ip_ranges = ["192.168.0.0/16", "10.0.0.0/8"]
      layer4_config {
        ip_protocol = "tcp"
        ports = ["22"]
      }
      layer4_config {
        ip_protocol = "icmp"
      }
    }
  }
  priority = 100
}

resource "google_compute_organization_security_policy_association" "policy" {
  provider = google-beta
  name          = "tf-test%{random_suffix}"
  attachment_id = google_compute_organization_security_policy.policy.parent
  policy_id     = google_compute_organization_security_policy.policy.id
}
```

## Argument Reference

The following arguments are supported:


* `name` -
  (Required)
  The name for an association.

* `attachment_id` -
  (Required)
  The resource that the security policy is attached to.

* `policy_id` -
  (Required)
  The security policy ID of the association.


- - -



## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `{{policy_id}}/association/{{name}}`

* `display_name` -
  The display name of the security policy of the association.


## Timeouts

This resource provides the following
[Timeouts](/docs/configuration/resources.html#timeouts) configuration options:

- `create` - Default is 20 minutes.
- `delete` - Default is 20 minutes.

## Import


OrganizationSecurityPolicyAssociation can be imported using any of these accepted formats:

```
$ terraform import google_compute_organization_security_policy_association.default {{policy_id}}/association/{{name}}
```
