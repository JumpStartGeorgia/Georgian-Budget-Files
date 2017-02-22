# Georgian-Budget-Files

This repository contains all of the files necessary for running the budget data uploader, which creates a structured database of information about the Georgian Budget. This uploader can be found in the [JumpStartGeorgia/Georgian-Budget-API repo](https://github.com/JumpStartGeorgia/Georgian-Budget-API/).

The files presented here are split into two groups:
1. Those received from the Georgian government, either via their website or Freedom of Information requests. The format of these files has been modified to work with the uploader (but the data has not been modified, of course)
2. Support files necessary for running the uploader. These files include a list of the twelve budget priorities, the connections between priorities and their programs and agencies, English translations of the names of all budget items, and a list of budget item pairs that are similar but not identical and whether they should be merged into one item or left as separate items.

## How to update these files

The Georgian government creates new documents over time, containing financial information about the Georgian budget. It is necessary to add those documents to this repo every once in a while to keep this project up to date.

The process of updating this repo with new documents isn't straightforward, so it's outlined here and explained in detail in the sections below. If the files released by the Georgian government have changed, you may have to modify this process.

1. Add new monthly spreadsheets, yearly spreadsheets, and priority PDFs
2. Run the uploader (see Georgian-Budget-API README)
3. Update the program and agency translations
4. Update the possible duplicates
5. Update the priority associations
6. Run the uploader again with the newly updated support files
7. Check that the data has been correctly uploaded

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

The data in the yearly spreadsheet is detected based on the column number, so you may have to rearrange the columns to adapt a spreadsheet to this format.

- Code: Column #2, *required*
- Name: Column #3, *required*
- Spent two years earlier: Column #4
- Planned previous year: Column #5
- Planned current year: Column #6

## Priority PDFs

The priority PDFs are not used directly by the uploader, but are kept here because they are a source of info for the translations and the priority associations files.

### Add new priority PDF

Copy the priority pdf to `files_from_government/priority_pdfs/priorities-yyyy.pdf`.

## Update translations file

Process for translating the name of a program or spending agency:

1. Run rake task for outputting translations (run `rake -T budget_data` in the Georgian-Budget-API app to find this task). If all names are translated, you can stop here.
1. Import this repo's `budget_item_translations.csv` into a spreadsheet.
1. Add the new, exported names to the bottom of the spreadsheet.
1. Translate them according to the procedure below.
1. When finished, export to CSV and update this repo's `budget_item_translations.csv` file

### How to translate a name

1. Search for the code in the English version of the 2012 priorities PDF.
1. If the code is there, and the English name is clearly a translation of the Georgian name, then use that English name.
1. If the code is not there, or the English name is not a correct translation of the Georgian name (it might be a translation of a different program, as the codes change), then you have to translate the name yourself.

Note: The government translated its budget (the priority PDF) into English in 2012, but not in subsequent years.

## Update possible duplicates

1. Run rake task for outputting new possible duplicates (run `rake -T budget_data` in the Georgian-Budget-API app to find this task). If there are no new possible duplicates, you can stop here.
1. Import this repo's `duplicate_pairs.csv` into a spreadsheet.
1. Add the new possible duplicate pairs to the bottom of the spreadsheet.
1. Decide whether each pair should be merged, and if so, whether the name change is significant. (See below instructions.)
1. When finished, export the spreadsheet to CSV and update the repo with the new `duplicate_pairs.csv`.

### How to decide whether a pair of items should be merged

1. Compare the names. If it's obvious just from their names that they're the same or different, then that's all you need to do. If it's not obvious, try the steps below.
1. Compare the descriptions of the programs/agencies in the priority PDFs.
1. You can also compare the amounts at the end of each row for guidance. If the items have similar average monthly amounts, then that may be a hint indicating that they should be merged. If the amounts are very different, then that may indicate that the two items are different. (You probably shouldn't base your decision on this factor alone.)
1. Another hint can come from the first monthly amount of the second item. The amounts in the monthly spreadsheets created by the government are recorded cumulatively, so each finance needs to know about the previous months' finances to be saved correctly to the database. For example, if a program's name changes in the middle of the year, then the first monthly amount of the second item in the pair will likely be higher than the monthly average.

### How to decide whether the name change is significant

If you decide that the items should be merged, then you need to decide whether the name change here is significant. A "significant" name change is one in which both names should ideally be shown to anyone looking at the agency or program.

For example, consider a program in which the names changed in this way:

2012: School development in Vake, Saburtalo, and Sololaki
2013: School development in Vake, Saburtalo, Sololaki, and Gldani

If you decide that these programs are indeed the same and should be merged, then you should probably mark the name change as significant, so that people will know what they are looking at.

## Update priority associations

TODO

## Check that data has been correctly uploaded

 At the very least, you should compare a few values from the spreadsheets to the values on the site. You may want to take a more systematic approach if you have added a lot of data.
