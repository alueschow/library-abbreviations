
# Library Abbreviations and Acronyms

This repository collects all kinds of library abbreviations and acronyms in different file and data formats.

## Used programs and data formats
* CSV (comma-separated, all fields quoted with double quotes)
* JSON
* JSON Lines ([http://jsonlines.org/](http://jsonlines.org/))
* jq ([https://stedolan.github.io/jq/](https://stedolan.github.io/jq/))
* SQLite
* DB Browser for SQLite
* LibreOffice Calc, Microsoft Excel


## Some sample code
### Collect data using your favourite tool
(File: _library-abbreviations.csv_)
* e.g. Microsoft Excel, LibreOffice Calc, ...
* export data as CSV or JSONL

### Convert CSV to JSON using jq
(File: _library-abbreviations.json_)
```
jq -R -s -f csv2json.jq library-abbreviations.csv > library-abbreviations.json
```
(note that _csv2json.jq_ is a file in this repository)

### Convert JSON to JSON Lines using jq
(File: _library-abbreviations.jsonl_)
```
jq -c '.[]' library-abbreviations.json > library-abbreviations.jsonl
```

### Convert JSONL to CSV using jq
(File: _library-abbreviations.csv_)
```
(head -1 library-abbreviations.jsonl | jq -r 'keys_unsorted | @csv' && jq -r '[.[]] | @csv' < library-abbreviations.jsonl) > library-abbreviations.csv
```

### Import CSV into SQLite database
(File: _library-abbreviations.db_)
```
sqlite3 library-abbreviations.db
[DROP TABLE library_abbreviation]
.mode csv
.separator ,
.import library-abbreviations.csv library_abbreviation
```

### Dump SQLite database to SQL statements
(File: _library-abbreviations.sql_)
```
sqlite3 library-abbreviations.db .dump > library-abbreviations.sql
```
These can e.g. be used to import the data into a MySQL database (with a few adjustments beforehand), see _library-abbreviations.mysql_ file.
