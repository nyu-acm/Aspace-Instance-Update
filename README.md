# Aspace-Instance-Update
This application is used to batch update Top Container URIs (box numbers) and Child Indicators (folder numbers) for Archival Object's within a Resource. The application uses the work order output from the [Hudson Molonglo's Digitization Work Order Plugin](https://github.com/hudmol/digitization_work_order).

usage<br/>
`$ aspace-instance-update --workorder your-workorder.tsv --environment your-environment`

Configuration
-------------
This application requires a go-aspace configuration file to be located at: /etc/go-aspace.yml on your system<br>
See: https://github.com/nyudlts/go-aspace/blob/main/go-aspace.yml_template

Options
-------
* --workorder, required,	/path/to/workorder.tsv
* --environment, required,      aspace environment to be used: dev/stage/prod
* --undo, optional,	runs a work order in reverse, undo a previous run
* --test, optional,	test mode does not execute any POSTs, this is recommended before running on any data
* --help	print this help message

Work-Order Specification
------------------------
| Resource ID	| Ref ID	| URI	| Container Indicator 1	| Container Indicator 2	| Container Indicator 3	| Title	| Component ID | Barcode |
| ---	| ---	| ---| ---	| --- | --- | ---	| --- | --- |
| TAM.011	| ref14	| /repositories/2/archival_objects/154967	| 1 | 	1 |  | Correspondence	| cuid34043 | 31142063615275 |

In a spreadsheet editor add two columns to the work order: 'New Container Indicator 2' and 'New Barcode'.

| Resource ID	| Ref ID	| URI	| Container Indicator 1	| Container Indicator 2	| Container Indicator 3	| Title	| Component ID | Barcode | New Container Indicator 2	| New Barcode |
| ---	| ---	| ---| ---	| --- | --- | ---	| --- | ---	| --- | --- |
| TAM.011	| ref14	| /repositories/2/archival_objects/154967	| 1 | 	1 |  | Correspondence	| cuid34043 | 31142063615275 | 2 | 31142063615276 |

The updater will update the reference to the top container (based on the new barcode field) and the child indicator 2 in the Instance.

Logging
-------
aspace-instance update will create a logfile that will be named "AIU-" plus the filename of the workorder being used. <br>
For example, using a workorder name 'alba_updates.tsv' will yield a log file named "AIU-alba_updates.tsv"

