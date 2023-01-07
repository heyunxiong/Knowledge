Java 使用 POI 操作 Excel
https://juejin.im/post/5c09e559e51d451da152df9c

在 POI 中，Workbook代表着一个 Excel 文件（工作簿），Sheet代表着 Workbook 中的一个表格，Row 代表 Sheet 中的一行，而 Cell 代表着一个单元格。 

HSSFWorkbook对应的就是一个 .xls 文件，兼容 Office97-2003 版本。 

XSSFWorkbook对应的是一个 .xlsx 文件，兼容 Office2007 及以上版本。

在 HSSFWorkbook 中，Sheet接口 的实现类为 HSSFSheet，Row接口 的实现类为HSSFRow，Cell 接口的实现类为 HSSFCell。 

XSSFWorkbook 中实现类的命名方式类似，在 Sheet、Row、Cell 前加 XSSF 前缀即可。（XSSFSheet、XSSFRow、XSSFCell）