# HotelDSRConverter

## Overview

The HotelDSRConverter program processes `.txt` and `.csv` files related to hotel daily sales reports (DSR). It extracts data, merges and decodes it, performs various calculations, and uploads the processed data to the Intacct system.

## Features

- Automatically detects and processes `.txt` and `.csv` files.
- Merges hotel data and ledger data.
- Decodes transactions.
- Performs data cleaning, including removing duplicates and direct bill checks.
- Formats data for CSV export and uploads to Intacct.

## Project Structure

### Main Class: `HotelDSRConverter`

- **Purpose**: Entry point for the program, processes files, and manages the flow of data.
- **Key Methods**:
  - `main(String[] args)`: Initiates file processing.
  - `processFile(File file, StringBuilder processedFilesSummary)`: Determines file type and processes accordingly.
  - `processCsvFile(File file, String filePath)`: Processes `.csv` files.
  - `processTxtFile(File file, String filePath)`: Processes `.txt` files.

### Supporting Classes and Methods

#### `CSVProcessor`
- **Purpose**: Handles specific processing of CSV files.
- **Key Methods**:
  - `csvFileProcessor(String filePath)`: Processes CSV files, merges data, and prepares it for upload.
  - `removeLessComprehensiveDirectBillRows(ArrayList<ArrayList<String>> transactions)`: Removes less comprehensive direct bill rows.
  - `removeDuplicates(ArrayList<ArrayList<String>> dataList)`: Removes duplicate rows from the data.
  - `arrayListToCSV(ArrayList<ArrayList<String>> updatedData, String date)`: Converts an ArrayList to a CSV file.
  - `dataToCSV(ArrayList<ArrayList<String>> decodedData, String date)`: Prepares data for CSV export.
  - `generalLedger(ArrayList<ArrayList<String>> decodedData)`: Summarizes data into general ledger entries.
  - `formatDate(String inputDate)`: Formats date strings.
  - `findMatchingFile(String directoryPath, String date, String fileType)`: Finds matching files based on the date and type.
  - `elxFilesMatch(String hotelFilePath, String ledgerFilePath)`: Checks if two files match based on their dates.
  - `extractDateFromFilename(String fileName)`: Extracts date from the filename.
  - `readCSV(String filePath)`: Reads CSV data from a file.
  - `print2DArrayList(ArrayList<ArrayList<String>> data)`: Prints a 2D ArrayList to the console.
  - `mergeData(ArrayList<ArrayList<String>> hotelData, ArrayList<ArrayList<String>> ledgerData)`: Merges hotel data and ledger data.
  - `splitRows(ArrayList<ArrayList<String>> rows)`: Splits rows with both debit and credit values.
  - `decodeTransaction(ArrayList<ArrayList<String>> mergedData)`: Decodes transactions into a human-readable format.
  - `getGLNumber(String transactionCode)`: Retrieves GL number for a given transaction code.
  - `getItemNum(String transactionCode)`: Retrieves item number for a given transaction code.

#### `ROC`
- **Purpose**: Handles specific processing of ROC (Return on Cost) files.
- **Key Methods**:
  - `rocProcessor(String filepath)`: Processes ROC files, sorts and prepares data for upload.
  - `isAllStrings(ArrayList<ArrayList<String>> list2D)`: Checks if all elements in a 2D list are strings.
  - `csvToArray(String filepath)`: Converts CSV data to a 2D ArrayList.
  - `sortData(ArrayList<ArrayList<String>> csvData)`: Sorts and processes CSV data.
  - `csvReady(ArrayList<ArrayList<String>> sortedData, String date)`: Prepares sorted data for CSV export.
  - `getItemNo(String memo)`: Retrieves item number based on memo.
  - `getAccountNo(String memo)`: Retrieves account number based on memo.
  - `rowTotals(ArrayList<ArrayList<String>> csvData, String rowTitle, String newTitle, int debitOrCredit)`: Computes totals for a specific row.
  - `getRows(ArrayList<ArrayList<String>> csvData, String rowTitle, String newTitle, int debitOrCredit)`: Retrieves specific rows based on title.
  - `processRowRange(ArrayList<ArrayList<String>> csvData, String startRow, String endRow, int debitOrCredit)`: Processes a range of rows.
  - `nameChange(ArrayList<ArrayList<String>> csvData, String rowTitle, String newName)`: Changes row names.
  - `guestLedger(ArrayList<ArrayList<String>> sortedData)`: Computes guest ledger entries.
  - `getDate(String filepath)`: Extracts date from the file path.
  - `exportToCsv(ArrayList<ArrayList<String>> csvData, String filepath)`: Exports data to a CSV file.
  - `checkFilesBeforeProcessing(String filepath)`: Checks if files exist before processing.

#### `SHIprocessor`
- **Purpose**: Handles specific processing of SHI files.
- **Key Methods**:
  - `shiProcessor(String filepath)`: Processes SHI files, sorts and prepares data for upload.
  - `dataToCSV(ArrayList<ArrayList<String>> sortedData)`: Prepares sorted data for CSV export.
  - `convertToCSV(ArrayList<ArrayList<String>> csvData, String filepath)`: Converts data to CSV and saves to a file.
  - `getItemNo(String memo)`: Retrieves item number based on memo.
  - `getAccountNo(String memo)`: Retrieves account number based on memo.
  - `formatDate(String dateStr)`: Formats date strings.
  - `sortData(ArrayList<ArrayList<String>> shiData)`: Sorts and processes SHI data.
  - `directBill(ArrayList<ArrayList<String>> shiData)`: Retrieves direct bill information.
  - `txtToArray(String filename)`: Converts text file data to a 2D ArrayList.
  - `printArray(ArrayList<ArrayList<String>> data)`: Prints a 2D ArrayList to the console.
  - `mergeData(ArrayList<ArrayList<String>> sortedData, ArrayList<ArrayList<String>> GLandAD)`: Merges sorted data with GL and AD data.
  - `switchSign(ArrayList<ArrayList<String>> sortedData, String titleName)`: Switches the sign of amounts for specified titles.
  - `dataHelper(ArrayList<ArrayList<String>> sortedData)`: Cleans and processes sorted data.
  - `balanceCheck(ArrayList<ArrayList<String>> sortedData)`: Checks and balances debit and credit totals.
  - `checkFilesBeforeProcessing(String filepath)`: Checks if files exist before processing.

## Usage

1. Place your `.txt` and `.csv` files in the same directory as the program.
2. Run the program.
3. Processed files will be detected, merged, decoded, and prepared for upload to Intacct.
4. A summary of processed files will be displayed in a popup.

## Notes

- Ensure the file names follow the expected patterns for proper date extraction and matching.
- The program skips files that don't match the expected types or patterns.

## Dependencies

- Java Development Kit (JDK)
- Apache PDFBox
- Intacct API

## Author

- Alex Martinez Jr.
