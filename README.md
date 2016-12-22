# Georgian-Budget-Files

This repository contains the spreadsheets and other files related to the budget of the Republic of Georgia. It is used as the data source in the [JumpStartGeorgia/Georgian-Budget repo](https://github.com/JumpStartGeorgia/Georgian-Budget/).

## Monthly Spreadsheets

### Format

Each spreadsheet must have four columns, one each for codes, names, planned finances and spent finances. The columns must have the text within these strings as headers:

Code: "ორგანიზაც. კოდი"
Name: "დ ა ს ა ხ ე ლ ე ბ ა"
Planned Finances: "გეგმა"
Spent Finances: "გადახდა"

Columns with other headers will be ignored.

### Add new monthly spreadsheet

1. Modify the spreadsheet to adhere to the format described above.
2. Add a copy of the modified spreadsheet to this path:

`files/monthly_spreadsheets/<year>/monthly_spreadsheet-mm.yyyy.xlsx`
