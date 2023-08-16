# Digital Scriptorium Data Reconciliation Process through OpenRefine

Digital Scriptorium OpenRefine documentation and JSON recipes for data reconciliation

## General instructions

When utilizing the JSON instructions (also known as recipes) found in this repository for DS data in OpenRefine, find the left column, select the `Undo/Redo` tab, select `Apply`, paste the JSON code, and then select `Perform operations`. This will execute the prewritten commands which perform various actions on the data for the reconciliation process.

Facets and filters can also be used on the data by using drop-down menus available on each column header and displayed in the left column when selecting the `Facet/Filter` tab.

The following notes apply to file naming conventions for editing file name variables found in the [instructions in this repository](/instructions/) (use all lowercase letters where applicable):
- DATE = the date the file/dataset was generated/created/extracted in `YYYYMMDD` format
- INSTITUTION = the code for the name of the institutional source for the data, such as `penn` or `kansas` or `csl`
- DATATYPE = the type of encoding standard or technical format of the metadata source, such as `marcxml` or `mets` or `csv`
- One or more DIFFERENTIATORS may also be added on the file name to disambiguate files, using sources names of collections or databases, such as `bibliophilly`, or batch numbers, such as `batch-1`, `batch-2`, etc.

Examples of correctly formatted file names:
- `20230518-materials-rome-mets-legacy-enriched.csv`
- `20230630-genres-penn-marcxml-bibliophilly-enriched.csv`
- `20230715-names-kansas-marc-enriched.csv`
- `20230816-languages-princeton-marcxml-batch-3-enriched.csv`
- `20230901-places-hrc-csv-fragments-batch-1-enriched.csv`

## Reconciliation instructions by metadata element / authority type

### Genres

[Genre reconciliation instructions](/instructions/genres.md)

### Languages

[Language reconciliation instructions](/instructions/languages.md)

### Materials

[Material reconciliation instructions](/instructions/materials.md)

### Places

[Place reconciliation instructions](/instructions/places.md)



## Reconciling names to Wikidata

1. Load `DATE-names-INSTITUTION-DATATYPE.csv` into OpenRefine; rename `DATE-names-INSTITUTION-DATATYPE-enriched.csv`
2. Add workflow columns: [JSON][name_workflow] (On the left, go to `Undo/Redo`, `Apply` and paste the JSON code, and `Perform operations`)
3. Copy `name_as_recorded` column and reconcile new `recon-human` column against human type (Q5): [JSON][name_recon_human]
4. Apply list of previously reconciled or known human names: 0. [JSON][name_known_human_0], 1. [JSON][name_known_human_1], 2. [JSON][name_known_human_2]
5. Manually reconcile and update known human names: *edit [JSON][name_known_human_2] and submit pull request*
6. Add `human-label`, `instance-of-human`, and `human-qid` columns; rename reconciliation column to `recon-organization` to reconcile against organization type (Q43229): [JSON][name_recon_org]
7. Apply list of previously reconciled or known organization names: [JSON][name_known_org]
8. Manually reconcile and update known organization names: *edit [JSON][name_known_org]*
9. Add `organization-label`, `instance-of-organization`, and `organization-qid` columns; add `instance_of_add`, `authorized_label_add`, and `structured_value_add` columns; finalize workflow: [JSON][name_finalize]
10. Remove any facets and filters
11. Export full CSV from OpenRefine (retain file name)

[name_workflow]:      json/name/010-name-workflow.json
[name_recon_human]:   json/name/030-name-recon-human.json
[name_known_human_0]: json/name/040-name-known-human.json
[name_known_human_1]: json/name/041-name-known-human.json
[name_known_human_2]: json/name/042-name-known-human.json
[name_recon_org]:     json/name/060-name-recon-org.json
[name_known_org]:     json/name/070-name-known-org.json
[name_finalize]:      json/name/090-name-finalize.json

```
json/name/010-name-workflow.json
json/name/030-name-recon-human.json
json/name/040-name-known-human.json
json/name/041-name-known-human.json
json/name/042-name-known-human.json
json/name/050-name-recon-org.json
json/name/060-name-known-org.json
json/name/090-name-finalize.json
```


## Reconciling subjects to FAST

### Reconciling named subjects

1. Load `DATE-named-subjects-combined.csv` into OpenRefine; rename `DATE-named-subjects-combined-enriched.csv`
2. Add workflow columns: [JSON][subject_workflow]
3. Copy `subject_as_recorded` column and reconcile new `recon-subject` column against FAST terms: [JSON][named_subject_recon_1]
4. Apply list of previously reconciled or known FAST terms: [JSON][named_subject_known]
5. Manually reconcile and update known FAST terms: *edit [JSON][named_subject_known]*
6. Add `named-subject-label-1` and `named-subject-fast-1` columns, reconcile next `recon-subject` column: [JSON][named_subject_recon_2]
7. Apply list of previously reconciled or known FAST terms: [JSON][named_subject_known]
8. Manually reconcile and update known FAST terms: *edit [JSON][named_subject_known]*
9. Add `named-subject-label-2` and `named-subject-fast-2` columns; consolidate `authorized_label` and `structured_value` columns; finalize workflow: [JSON][named_subject_finalize]
10. Export three versions from OpenRefine as CSV files: 1) full document, 2) facet by `structured_value` blank (null/empty) = `true`, 3) facet by `structured_value` blank (null/empty) = `false`

[subject_workflow]:         json/subject/010-subject-workflow.json
[named_subject_recon_1]:    json/subject/named/030-named-subject-recon-1.json
[named_subject_known]:      json/subject/named/040-named-subject-known.json
[named_subject_recon_2]:    json/subject/named/060-named-subject-recon-2.json
[named_subject_finalize]:   json/subject/named/090-named-subject-finalize.json


### Reconciling subjects (topical, etc.)

1. Load `DATE-subjects-combined.csv` into OpenRefine; rename `DATE-subjects-combined-enriched.csv`
2. Add workflow columns: [JSON][subject_workflow]
3. Copy `subject_as_recorded` column and reconcile new `recon-subject` column against FAST terms: [JSON][subject_recon_1]
4. Apply list of previously reconciled or known FAST terms: [JSON][subject_known]
5. Manually reconcile and update known FAST terms: *edit [JSON][subject_known]*
6. Add `subject-label-1` and `subject-fast-1` columns, reconcile next `recon-subject` column: [JSON][subject_recon_2]
7. Apply list of previously reconciled or known FAST terms: [JSON][subject_known]
8. Manually reconcile and update known FAST terms: *edit [JSON][subject_known]*
9. Add `subject-label-2` and `subject-fast-2` columns, reconcile next `recon-subject` column: [JSON][subject_recon_3]
10. Apply list of previously reconciled or known FAST terms: [JSON][subject_known]
11. Manually reconcile and update known FAST terms: *edit [JSON][subject_known]*
12. Add `subject-label-3` and `subject-fast-3` columns; consolidate `authorized_label` and `structured_value` columns; finalize workflow: [JSON][subject_finalize]
13. Export three versions from OpenRefine as CSV files: 1) full document (retain file name), 2) facet by `structured_value` blank (null/empty) = `true` and rename it `DATE-subjects-DATATYPE-INSTITUTION-unreconciled.csv`, 3) facet by `structured_value` blank (null/empty) = `false` and rename it `DATE-subjects-DATATYPE-INSTITUTION-reconciled.csv`

[subject_recon_1]:    json/subject/topic/030-subject-recon-1.json
[subject_known]:      json/subject/topic/040-subject-known.json
[subject_recon_2]:    json/subject/topic/060-subject-recon-2.json
[subject_recon_3]:    json/subject/topic/090-subject-recon-3.json
[subject_finalize]:   json/subject/topic/120-subject-finalize.json

```
json/subject/010-subject-workflow.json
json/subject/named/030-named-subject-recon-1.json
json/subject/named/040-named-subject-known.json
json/subject/named/060-named-subject-recon-2.json
json/subject/named/090-named-subject-finalize.json
json/subject/topic/030-subject-recon-1.json
json/subject/topic/040-subject-known.json
json/subject/topic/060-subject-recon-2.json
json/subject/topic/090-subject-recon-3.json
json/subject/topic/120-subject-finalize.json
```


