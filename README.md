# Crypto-Currency-Calculator
A crypto currency logging tool using Google Scripts for Google Sheets made to assist with tax reporting

**SET-UP**
1. Open up Google Chrome and make a new Google Sheet. Name it anything you want.
2. At the top, go to Extensions -> Apps Script
3. For each of the txt files, you will need to copy and paste the script into a file in the file section to the left. The process is as follow:
	- Name the file by hovering the file name, clicking on the 3 vertical dots, and selecting rename. It is required to name it what the txtfile name is excluding the numbers.
	- Copy and and paste the script for each txt file
	- Click on the + next to Files AZ and select Script to add a new file.
	- Repeat until all txts files are imported
4. Once complete, the files should look like this:
	- autoOpen.gs
   	- autoEdit.gs
	- addingYears.gs
	- fixFormat.gs
	- sortTransactions.gs
	- verification.gs
	- bigDecimal.gs
	- analyzeTransactions.gs
	- create8949.gs
5. Click the save disk icon under the project icon to save the project.
6. A couple of the scripts require triggers to function properly. To do this, follow the following steps:
   	- Click on the alarm clock icon to the left (Triggers)
	- On the bottom right, click Add Trigger
	- For autoEdit:
		- Choose which function to run: autoEdit
		- Select event type: On Edit
		- Failure notifications setting: Notify me weekly
		- Leave the rest as is and click save
	- For autoOpen:
	  	- Choose which function to run: autoOpen
		- Failure notifications setting: Notify me weekly
		- Leave the rest as is and click save
	- This will need to be synced to your Google sheet to function. Follow the steps to allow this process. 
7. Upon completion of the above steps, return to the spreadsheet and refresh the page. The scripts will build the Google Sheet.

**FEATURES**

The tool is fairly rich for a prototype. To understand some of the basic
features, see below.

_GAS FEES:_ Gas is a tax documentation nightmare with no consensus on how to 
properly manage. The IRS has no documentation on how to report them, however,
the generally accepted 'safe' methods are default on newly a built sheet. The user
has control of how the fees are incorporated in the capital gains/loss for each 
type of transaction.

_CVS IMPORT:_ Since it would be impossible for a single person to be able 
to create an import function for every single API of every single coin from every 
single exchange, the solution was to copy the CVS files into the IMPORT CSV sheet, 
make modifications based on column drop downs,and import the changes into the 
TRANSACTIONS sheet. 

_PROCESSING OPTIONS:_ Google Sheets is pretty slow. Scripts time out after 
six minutes of calculations. This section allows the user to select an algorithm
to calculate within a specific year in order to minimize the failure of a script.
In order for proper calculations, the sheet must be sorted chronologically. 
PROCESS TRANSACTIONS then goes through the defined year (this is automatically 
populated based on dates within TRANSACTIONS once refreshed) to calculate 
capital gains/loss based on settings in TRANSACTIONS. If no year is selected, it 
defaults to the start of TRANSACTIONS. Finally, once PROCESS TRANSACTIONS has 
been completed, OUTPUT TAX DOCUMENT will output a TAX document similar to the
IRS 8949 on a separate sheet with the year. If no sheet has been created, a new
one will be made, otherwise that current year will be overwritten. WASH SALES
are not necessary to be calculated at this time, but may become tax law in the 
future. For now, leave it checked as IGNORED. Clicking CALCULATE initiates
any of the selected algorithms.

_REPAIR FORMATTING:_ Does what it says. You break it, it fixes it. However, data
lost is data lost. 

_YOUR WALLET:_ Calculates total coin across all exchanges of each type of coin
once PROCESS TRANSACTIONS is complete.

**TRANSACTIONS**

There's a lot to pack in with this sheet. Most of it requires some bit of knowledge on crypto trading to understand, but some key points are the following:
	
_TRANSACTION TYPE:_ Upon select, will guide the user in which columns to fill out depending on the transaction type. BUY handles acquiring coin of any kind in any way. SELL handles disposing of a coin in any way. TRADE moves a coin of one type into another type of coin as a taxable event, while SWAP is the same but as a non-taxable event. TRANSFERS are for moving coin betwen wallets and exchanges (non-taxable) while GIFT and DONATE are exceptions to SELL that are separated to output separately in the tax document. These are handleded differently based various laws.

_DATES:_ All dates must be formatted the same or the sheet breaks. This would normally be handled by having IMPORT CSV working, but alas. To follow the correct formatting, hover over the column name. 

_METHOD:_ The IRS does not specify in what order you sell your coin. As a result, you can sell any coin you purchased at anytime, but there are generally only three options that make sense. FIFO is first in first out, which simply sells the first coin of that type while LIFO is last in first out which sells the most recent. HIFO is high in first out which sells the highest valued one first. For concistency, it his higly recommended to simply keep this FIFO as that is the standard for stock trading. Using the others can reduce capital gain/capital loss, however, could possibly result in the sold coin being a short term trade which generally results in higher taxes. 

**IMPORT CSV**

WIP

**TAX DOCUMENTS**

Once one of these is exported, it will look very much like an 8949 that you would report to the IRS. If wash sales are selected, codes and adjustments are output. It is also possible to filter out by exchange as this may be useful in the future.
