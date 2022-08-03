# Islandora Linked Taxonomies

A place to collect thoughts about linked taxonomies in Islandora.

## Concept

* One site acting as a hub hosting a taxonomy
* Other sites using that taxonomy as an endpoint for reference fields
* IF POSSIBLE: Allow those sites to write new data to that shared taxonomy

## Possible modules to make use of

* https://github.com/mjordan/autocomplete_endpoint?
* https://www.drupal.org/project/linked_data_field 
* https://github.com/digitalutsc/authority-link-auto-complete 

## Process

1. autocomplete_endpoint must be installed and configured on the Provider machine.
2. linked_data_field must be installed and configured on the Client machine.
3. authority-link-auto-complete must be installed and configured on the Client machine.

NOTE: So far we can't test this because we do not have a way of installing modules on a Web-accessible machine.
