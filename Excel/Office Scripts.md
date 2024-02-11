Press the option **Automate** in the top.

# New Script

Every scripts need to have the **Main function** with the parameter **workbook**, this is the type *'ExcelScript.Workbook'*

```typescript
function main(workbook: ExcelScript.Workbook){
	let selectedCell = workbook.getActiveCell();
	let selectedSheet = workbook.getActiveWorkSheet();
	
}
```

The variable **'workbook'** contain all the commands for handled the datasheet in Excel.