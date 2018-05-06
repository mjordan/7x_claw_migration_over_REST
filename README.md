# Simple Islandora 7.x to CLAW migration via REST

## Overview

Illustrates a migration from an Islandora 7.x repository to a CLAW repository using only configuration. No custom module code is required. This is possible because Drupal 8 has migration plugins for remote JSON data, and because Islandora 7.x has the ability, via the Islandora REST module, to act as a Drupal 8 migration data source. If you want to see the response body to the REST request that makes this possible, a sample is available in a [gist](https://gist.github.com/mjordan/78c30ce9bb6ec7e3f8f838aa27a39fef).

This is a very early attempt at migrating Islandora 7.x objects into CLAW. A lot of stuff is missing, including:

* migrating into a specific collection
* migrating images, PDFs, etc.

But that stuff will come.

## Requirements

* On the source Islandora 7.x instance
  * [Islandora REST](https://github.com/discoverygarden/islandora_rest)
* On the target Islandora CLAW instance
  * [Migrate Plus](https://www.drupal.org/project/migrate_plus)
  * [Migrate Tools](https://www.drupal.org/project/migrate_tools)

## Usage

### Step 1: Preparing your Islandora Image content type

Add a `field_pid` field to our Islandora Image content type.

### Step 2: Modifying the configuration file to use your Islandora 7.x instance as a source

Line 12 in the configuration file defines an Islandora REST request that queries Solr to retrieve source data to migrate to CLAW:

```
urls: 'http://digital.lib.sfu.ca/islandora/rest/v1/solr/RELS_EXT_isMemberOfCollection_uri_mt:"vpl:collection"&RELS_EXT_hasModel_uri_mt\:info:fedora/islandora:sp_basic_image?fl=PID,fgs_label_t&rows=10'
```

To modify this to use your 7.x, after installing the REST module, change

* `http://digital.lib.sfu.ca` to your Islandora 7.x's hostname
* `vpl:collection` to your source collection's PID
* `islandora:sp_basic_image` to the content model you want to restrict the query to.

Save your configuration file before moving on to Step 3.

### Step 3: Importing the configuration

1. Import the migration configuration into your Drupal 8 instance by going to Configuration > Configuration synchronization > Import > Single item.
1. Choose "Migration" from the "Configuration type" list.
1. Paste the configuration file into the "Paste your configuration here" field.

### Step 4: Running the migration

In your Drupal installation directory, run `drush migrate-import islandora_basic_image_json_over_rest`.

You should see the following output:

```
ubuntu@claw:/var/www/html/drupal/web/modules/contrib$ drush migrate-import islandora_basic_image_json_over_rest
 [notice] Processed 10 items (10 created, 0 updated, 0 failed, 0 ignored) - done with 'islandora_basic_image_json_over_rest'
```

Go to the Content admin menu to see your new nodes.

### Step 5 (optional): Modifying the configuration

You can modify the configuration file within the Drupal admin user interface. To do so:

1. Go to Configuration > Configuration synchronization > Export > Single item.
1. Choose "Migration" from the "Configuration type" list.
1. Choose "Islandora 7.x JSON over REST" from the list of Configuration names.

Your configuration file will appear. Notice that it now has a UUID, at the top.

If you modify the configuration, reimport it using the instructions above, making sure that you do not modify the UUID value.

## Useful commands

* `drush migrate-status islandora_basic_image_json_over_rest`
  Shows the status of your migration.
*  `drush migrate-rollback islandora_basic_image_json_over_rest`
  Will "delete" the results of your migration.
* `drush migrate-reset-status islandora_basic_image_json_over_rest`
  Sets the migration's status to "idle", effectively stopping the migration should it get stuck.

## Contributing

Let's get these things working:

* Migrating into a specific collection
* Images

PRs are welcome!

## Maintainer

* Mark Jordan, [Simon Fraser University Library](http://www.lib.sfu.ca/)

## License

The Unlicense.
