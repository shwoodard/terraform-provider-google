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
subcategory: "Data catalog"
page_title: "Google: google_data_catalog_tag_template"
description: |-
  A tag template defines a tag, which can have one or more typed fields.
---

# google\_data\_catalog\_tag\_template

A tag template defines a tag, which can have one or more typed fields.
The template is used to create and attach the tag to GCP resources.


To get more information about TagTemplate, see:

* [API documentation](https://cloud.google.com/data-catalog/docs/reference/rest/v1/projects.locations.tagTemplates)
* How-to Guides
    * [Official Documentation](https://cloud.google.com/data-catalog/docs)

<div class = "oics-button" style="float: right; margin: 0 0 -15px">
  <a href="https://console.cloud.google.com/cloudshell/open?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fterraform-google-modules%2Fdocs-examples.git&cloudshell_working_dir=data_catalog_tag_template_basic&cloudshell_image=gcr.io%2Fgraphite-cloud-shell-images%2Fterraform%3Alatest&open_in_editor=main.tf&cloudshell_print=.%2Fmotd&cloudshell_tutorial=.%2Ftutorial.md" target="_blank">
    <img alt="Open in Cloud Shell" src="//gstatic.com/cloudssh/images/open-btn.svg" style="max-height: 44px; margin: 32px auto; max-width: 100%;">
  </a>
</div>
## Example Usage - Data Catalog Tag Template Basic


```hcl
resource "google_data_catalog_tag_template" "basic_tag_template" {
  tag_template_id = "my_template"
  region = "us-central1"
  display_name = "Demo Tag Template"

  fields {
    field_id = "source"
    display_name = "Source of data asset"
    type {
      primitive_type = "STRING"
    }
    is_required = true
  }

  fields {
    field_id = "num_rows"
    display_name = "Number of rows in the data asset"
    type {
      primitive_type = "DOUBLE"
    }
  }

  fields {
    field_id = "pii_type"
    display_name = "PII type"
    type {
      enum_type {
        allowed_values {
          display_name = "EMAIL"
        }
        allowed_values {
          display_name = "SOCIAL SECURITY NUMBER"
        }
        allowed_values {
          display_name = "NONE"
        }
      }
    }
  }

  force_delete = "false"
}
```

## Argument Reference

The following arguments are supported:


* `fields` -
  (Required)
  Set of tag template field IDs and the settings for the field. This set is an exhaustive list of the allowed fields. This set must contain at least one field and at most 500 fields.
  Structure is [documented below](#nested_fields).

* `tag_template_id` -
  (Required)
  The id of the tag template to create.


<a name="nested_fields"></a>The `fields` block supports:

* `field_id` - (Required) The identifier for this object. Format specified above.

* `name` -
  The resource name of the tag template field in URL format. Example: projects/{project_id}/locations/{location}/tagTemplates/{tagTemplateId}/fields/{field}

* `display_name` -
  (Optional)
  The display name for this field.

* `description` -
  (Optional)
  A description for this field.

* `type` -
  (Required)
  The type of value this tag field can contain.
  Structure is [documented below](#nested_type).

* `is_required` -
  (Optional)
  Whether this is a required field. Defaults to false.

* `order` -
  (Optional)
  The order of this field with respect to other fields in this tag template.
  A higher value indicates a more important field. The value can be negative.
  Multiple fields can have the same order, and field orders within a tag do not have to be sequential.


<a name="nested_type"></a>The `type` block supports:

* `primitive_type` -
  (Optional)
  Represents primitive types - string, bool etc.
   Exactly one of `primitive_type` or `enum_type` must be set
  Possible values are `DOUBLE`, `STRING`, `BOOL`, and `TIMESTAMP`.

* `enum_type` -
  (Optional)
  Represents an enum type.
   Exactly one of `primitive_type` or `enum_type` must be set
  Structure is [documented below](#nested_enum_type).


<a name="nested_enum_type"></a>The `enum_type` block supports:

* `allowed_values` -
  (Required)
  The set of allowed values for this enum. The display names of the
  values must be case-insensitively unique within this set. Currently,
  enum values can only be added to the list of allowed values. Deletion
  and renaming of enum values are not supported.
  Can have up to 500 allowed values.
  Structure is [documented below](#nested_allowed_values).


<a name="nested_allowed_values"></a>The `allowed_values` block supports:

* `display_name` -
  (Required)
  The display name of the enum value.

- - -


* `display_name` -
  (Optional)
  The display name for this template.

* `region` -
  (Optional)
  Template location region.

* `force_delete` -
  (Optional)
  This confirms the deletion of any possible tags using this template. Must be set to true in order to delete the tag template.

* `project` - (Optional) The ID of the project in which the resource belongs.
    If it is not provided, the provider project is used.


## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `{{name}}`

* `name` -
  The resource name of the tag template in URL format. Example: projects/{project_id}/locations/{location}/tagTemplates/{tagTemplateId}


## Timeouts

This resource provides the following
[Timeouts](/docs/configuration/resources.html#timeouts) configuration options:

- `create` - Default is 20 minutes.
- `update` - Default is 20 minutes.
- `delete` - Default is 20 minutes.

## Import


TagTemplate can be imported using any of these accepted formats:

```
$ terraform import google_data_catalog_tag_template.default {{name}}
```

## User Project Overrides

This resource supports [User Project Overrides](https://www.terraform.io/docs/providers/google/guides/provider_reference.html#user_project_override).
