# Islandora Linked Taxonomies

A method for providing an authoritative Taxonomy on a Drupal site, and using that Taxonomy on another Drupal site.

## Concept

* One site acting as a hub hosting a taxonomy
* Other sites using that taxonomy as an endpoint for reference fields
* Future goals: Allow those sites to write new data to that shared taxonomy

## Modules required

* https://github.com/mjordan/autocomplete_endpoint
* https://www.drupal.org/project/linked_data_field 

## Process

* autocomplete_endpoint must be installed and configured on the Provider machine.
* linked_data_field must be installed and configured on the Client machine.

### On the Provider machine:

1. Install autocomplete_endpoint
2. Create a Taxonomy to act as your endpoint
3. On that Taxonomy, create a field with the type `Text (plain)` or `Link` to contain a URI to the term
4. Populate your taxonomy with Terms and URIs 
  * Note: the URIs do not technically need to resolve, but they *should* resolve to a valid link to the term on your Provider site.
5. Take note of the Machine Name of (1) the Taxonomy and (2) the URI field you created.
6. Configure an Endpoint:
  * Admin > Configuration > Web Services > Autocomplete Endpoint (admin/autocomplete_endpoint)
  * Label: Whatever you like
  * Type: Vocabulary
  * Vocabulary ID: The machine name for the vocabulary you created
  * URI field: The machine name for the URI field on that vocabulary
7. Make note of the Machine Name of your new Endpoint (from the URL) 
8. Test your endpoint by making a query in your browser: `https://[your website]/autocomplete_endpoint/[endpoint machine name]?q=[query]`. For example, `q=d` will return values from the taxonomy beginning with D.

### On the Client machine (the one looking up data)

1. Install linked_data_field
2. Configure a Linked Data Lookup Endpoint: 
  * Go to Admin > Structure > Linked Data Lookup Endpoint > Add Linked Data Lookup Endpoint
  * Add Linked Data Lookup Endpoint
  * Label: your choice
  * Endpoint type: `URL Argument Type`
  * Base URL: ``https://[your website]/autocomplete_endpoint/[endpoint machine name]?q=` [Note: it must end with `?q=`.]
  * Result record JSON path: `[*]`
  * Label JSON key: `label`
  * URL JSON key: `uri`
  Your endpoint is now configured as a field that can be added to a content type.
3. Add a lookup field to your Content Type:
  * Manage Fields on your content type
  * Field type: `Linked Data Lookup Field`
  * Select the Endpoint you configured above
  * Save

## Future Goals

We'd like to see if there's any way to leverage the REST API to not only read data from the remote endpoint, but also write data to that endpoint when terms entered in the form do not retrieve a lookup result.
