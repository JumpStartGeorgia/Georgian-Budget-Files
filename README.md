# Georgian-Budget-Files

This repository contains all of the files necessary for running the budget data uploader, which creates a structured database of information about the Georgian Budget. This uploader can be found in the [JumpStartGeorgia/Georgian-Budget-API repo](https://github.com/JumpStartGeorgia/Georgian-Budget-API/).

## How to update this Repo

The Georgian government creates new documents over time, containing financial information about the Georgian budget. It is necessary to add those documents to this repo every once in a while to keep this project up to date.

The process of updating this repo with the new documents isn't always straightforward, so it's outlined here and explained in detail in the sections below. If the files released by the Georgian government have changed, you may have to modify this process.

1. Add new monthly spreadsheets, yearly spreadsheets, and priority PDFs
2. Run the uploader
3. Update the program and agency translations
4. Update the possible duplicates
5. Update the priority associations
6. Run the uploader again with the newly updated support files
7. Check that the data has been correctly uploaded

## Running the uploader

Look at the Georgian-Budget-API's documentation for info on how to run the uploader.

TODO: Check that the API has documentation on running the uploader

## Monthly Spreadsheets

### Add new monthly spreadsheet

1. Modify the spreadsheet to adhere to the format described below.
1. Copy the modified spreadsheet to this path:

`files_from_government/monthly_spreadsheets/<year>/monthly_spreadsheet-mm.yyyy.xlsx`

### Format

Each spreadsheet must have four columns, one each for codes, names, planned finances and spent finances. The columns must have the text within these strings as headers:

Code: "ორგანიზაც. კოდი"
Name: "დ ა ს ა ხ ე ლ ე ბ ა"
Planned Finances: "გეგმა"
Spent Finances: "გადახდა"

Columns with other headers will be ignored.

## Yearly Spreadsheets

### Add new yearly spreadsheet

1. Modify the spreadsheet to adhere to the format described below.
1. Copy the CSV into the `files_from_government/yearly_spreadsheets` directory. If you did not need to change the format of the spreadsheet, then use this file name:

`yearly_spreadsheet-yyyy-formatted.xlsx`

If you did change the format of the spreadsheet, then use this file name:

`yearly_spreadsheet-yyyy-original-formatted.xlsx`

Note: The idea behind this naming scheme was that it should be clear when the government's documents have been reformatted for the purposes of this uploader. Ideally, we would use a similar naming scheme in the monthly spreadsheets above.

### Format

TODO

## Priority PDFs

The priority PDFs are not used directly by the uploader, but are kept here because they are a source of info for the translations and the priority associations files.

### Add new priority PDF

Copy the priority pdf to `files_from_government/priority_pdfs/priorities-yyyy.pdf`.

## Update translations file

Process for translating the name of a program or spending agency:

1. Run rake task for outputting translations TODO. If all names are translated, you can stop here. If there are new names to be translated, continue.
1. Copy the current `budget_item_translations.csv` file contents to a spreadsheet somewhere.
1. Add the new, untranslated names to the bottom of the spreadsheet.
1. Translate them according to the below procedure.
1. When finished, export to CSV and update this repo's `budget_item_translations.csv` file

### How to translate a name

1. Search for the code in the English version of the 2012 priorities PDF.
1. If the code is there, and the English name is clearly a translation of the Georgian name, then use that English name.
1. If the code is not there, or the English name is not a correct translation of the Georgian name (the code might have changed since 2012), then you have to translate the name yourself.

Note: The government translated its budget (the priority PDF) into English in 2012, but not in subsequent years.

## Update possible duplicates

TODO

## Update priority associations

TODO

## Check that data has been correctly uploaded

 At the very least, you should compare a few values from the spreadsheets to the values on the site. You may want to take a more systematic approach if you have added a lot of data.
