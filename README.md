# Simple Islandora 7.x to CLAW migration via REST

## Overview

No code!

```javascript
{
	"responseHeader": {
		"status": 0,
		"QTime": 1,
		"params": {
			"q": "RELS_EXT_isMemberOfCollection_uri_mt:\u0022vpl:collection\u0022\u0026RELS_EXT_hasModel_uri_mt\\:info:fedora",
			"json.nl": "map",
			"fl": "PID,fgs_label_t",
			"start": "0",
			"fq": "RELS_EXT_isViewableByUser_literal_ms:\u0022anonymous\u0022 OR RELS_EXT_isViewableByRole_literal_ms:\u0022anonymous user\u0022 OR ((*:* -RELS_EXT_isViewableByUser_literal_ms:[* TO *]) AND (*:* -RELS_EXT_isViewableByRole_literal_ms:[* TO *]))",
			"rows": "10",
			"version": "1.2",
			"wt": "json"
		}
	},
	"response": {
		"numFound": 1351,
		"start": 0,
		"docs": [{
			"PID": "vpl:122",
			"fgs_label_t": "Chinese business damaged by race riot"
		}, {
			"PID": "vpl:1224",
			"fgs_label_t": "Doukhobors at cenotaph with Lebedoff sign"
		}, {
			"PID": "vpl:1225",
			"fgs_label_t": "Doukhobors praying at cenotaph"
		}, {
			"PID": "vpl:1221",
			"fgs_label_t": "Doukhobors entering office in Parliament Buildings"
		}, {
			"PID": "vpl:1223",
			"fgs_label_t": "Doukhobors at cenotaph in Downtown Vancouver"
		}, {
			"PID": "vpl:1222",
			"fgs_label_t": "Doukhobors standing next to buses in Downtown Vancouver"
		}, {
			"PID": "vpl:1219",
			"fgs_label_t": "Doukhobors waiting in Parliament Buildings"
		}, {
			"PID": "vpl:1220",
			"fgs_label_t": "Doukhobors in Parliament Buildings"
		}, {
			"PID": "vpl:100",
			"fgs_label_t": "C.P.R. wooden bridge at M.204.25 near Ashcroft"
		}, {
			"PID": "vpl:10",
			"fgs_label_t": "Komagata Maru incident"
		}]
	}
}
```

## Requirements

* On the source Islandora 7.x instance
  * [Islandora REST](https://github.com/discoverygarden/islandora_rest)
* On the target Islandora CLAW instance
  * [Migrate Plus](https://www.drupal.org/project/migrate_plus)
  * [Migrate Tools](https://www.drupal.org/project/migrate_tools)

## Usage

### Step 1: Preparing your Islandora Image content type

Add a `field_pid` field to our Islandora Image content type.

### Step 1: Importing the configuration

1. Import this configuration by going to Configuration > Configuration synchronization > Import > Single item.
1. Choose "Migration" from the "Configuration type" list.
1. Paste the .yml file in this Git repository into the "Paste your configuration here" field.

### Step 2: Running the migration

In your Drupal installation directory, run `drush migrate-import islandora_basic_image_json_over_rest`.

## Contributing

## Maintainers/Sponsors

* Mark Jordan, [Simon Fraser University Library](http://www.lib.sfu.ca/)

## License

The Unlicense.
