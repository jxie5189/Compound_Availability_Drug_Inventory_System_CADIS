# Compound_Availability_Drug_Inventory_System_CADIS
This project was done for class project in 6 week's worth of time. 

Read Me:


CADIS (Compound Availability and Drug Inventory System)

Summary:

	CADIS tracks the real-time availability of compounded intravenous drugs across multiple pharmacies.
It utilizes concurrent programming to ensure efficient inventory management, cost reduction, and waste reduction by
repurposing drugs for different patients. Patients benefit from accessing drugs from alternative sources, even
out-of-network non-institutional pharmacies. The system effectively handles high volumes and improves inventory
management for better patient outcomes and satisfaction.

How to run:

    ****
    Before running, modify 'ABC Pharmacy Drug Inputs' and 'Koch Pharmacy Drug Inputs' drug dates to the date
         that you will run to demonstrate time thread, the program contains a stimulated fast-foward time

    New Implmentation:
        Database Access:
        Before running the program, you must change the path of both database loction (Drug_Stability_DB and TransferLog_DB).
        You would have to change the String url in the getConn method for both database.

        The url in Drug_Stability_DB's getConn method should be the path to Drug_Stability_DB.db,
        while the url in TransferLog_DB's getConn method should be the path to TransferLog_DB.db.
        There will be 3 tables and 2 different Database for the program to fun and the jdbc used is SQLite.

        CADIS uses Drug_Stability_DB.db, which contains tables Drug_Stability_DB and Ideal_Storage_Condition.
        CADIS uses Backup_TransferLog_DB.db, which contains table All_TransferLog.

    ****

    Run the whole program by running Main. Main will prompt the user to enter 'ok' to enter, any other input will result
in invalid entry and cannot proceed forward. Once the user has enter 'ok' to enter the program, Main will initially read
'Pharmacies.txt', 'ABC Pharmacy Drug Inputs', and 'Koch Pharmacy Drug Inputs' files. It will display 'Pharmacy file have
been read' and 'All Drug Inputs file have been read'.

    Pharmacies.txt contains 5 pharmacies, but more can be added. A valid pharmacy can be added by entering the name of
the pharmacy and their address, separated by a ',' in the Pharmacies.txt file on a new line. Drug files can also be
added, but each pharmacy will one drug file. Drug files will specifically be named as Pharmacy_name and ' Drug Inputs'.
Each line of a drug file will be an individual drug. Each drug will have name, strength, date/time when it was made
in the format of MM/DD/YY HH:MM, stability in number of hours, either "IV" or "SC" as administration route, either "NS",
or "D5W" as dilute used, if a pharmacist have verified yet, and "Room temp" or "Fridge" as storage requirement. All these
fields will be separated by ','. The program will automatically create individual Pharmacy objects for each pharmacy as
well as individual drugs and be added to their respective inventory.

    The initial main menu will display the current date and time on the top and there will be 6 options to choose from:
1-Show all available Pharmacy, 2-Show all available drugs, 3-show each Pharmacy's Inventory, 4-Initiate transfers,
5-Access TransferLogs, and 0-exit application.

    When the user selects 1, a selection of all the Pharmacies will display. The user can get back to the previous menu
by enter 9. By entering 2, a sub menu is displayed and categorizes all the drugs into either Intravenous, Subcutaneous,
or All available drugs. Accessing any of the 3 option will display a list of respective drug type (Intravenous,
Subcutaneous, or both). Each drug will also be accompanied by their BeyondUseDate(BUD), which is calculated by adding
their stability to their CompoundDate in the format of MM/DD/YY HH:MM. Revert back to the main menu by enter 9. If the
user enters 3, then a list of all the pharmacies will display along with their respective inventory. If a pharmacy does
not carry any drug in their inventory, then a 'Inventory does not contain any drug' will display.

    To initiate a transfer between pharmacies, the user enters 4 into the main menu prompt. The program will ask the user
to enter their own current pharmacy's (or where the drug is being transferred to). Next, the program will only list
pharmacies that currently have at least 1 drug in their inventory. The user enters the pharmacy ID number to transfer
from. The program will display all the available drugs that is allowed to be transferred, and asks the user to enter the
number that corresponds to the drug. Once the target drug is selected/entered, a message of 'Transfer have been initiated'
will display, and a transfer will be created. The program will display 'Transfer wrote to <Pharmacy_Name> transfer_log.dat'
if the written was successful. The Transfer object contains the drug entity, the destination pharmacy, and the source
pharmacy information. Each successful transfer object will be added to each pharmacy's transfer log and a file containing
an ArrayList of transfer object will be written out. A 'Transfer Completed' completes the transfer, and display the newly
updated inventory of each pharmacy (destination pharmacy and source pharmacy) and the user is back to the main menu.

    User should enter 5 (Access TransferLogs) only after initiating at least one transfers and thus there exist a
'<Pharmacy_name> transfer_log.dat' file. After entering 5, there will be a display of available pharmacy logs. Enter the
number that corresponds to the transfer log to display the entry number, the drug's name and strength, the name of the
source pharmacy transferred from, and the destination pharmacy transferred to.

    The program currently have a stimulated advance time to demonstrate its auto drug disposal. After entering 'ok' to
obtain the first main menu, noticed the current date/time in the top field. The forwarded stimulated time thread start
when the user enters their first selection. Then for every 2 seconds, the current date/time will advance 1 hour. After
incrementing the time, the program will scan each pharmayc's inventory for drugs with an BUD of 6 hours from current time,
i.e, if a drug's BUD is at 20:00, and the current time is 15:00, then that drug will be removed, because 6 hours from
20:00 is 14:00 and 15:00 is already pass 14:00. A Notification will display stating which drug was removed. The time
thread stops when the program exist.

    The Program is now fitted with access to database in SQLite. When Main is invoked, the menu now contains
"Access Drug/Transfer Database" as option 6. By selecting 6, the user gets to a submenu of "1 - Drug Stability Database"
or "2 - TransferLog Database". If the user selects 1, then CADIS will access Drug_Stability_DB database. Drug_Stability_DB
has 2 tables, Drug_Stability_DB table and Ideal_Storage_Condition table. CADIS combines both table via a JOIN call and
display all the drug names, drug route, stability in hours, and storage condition on to the terminal. If the user selects
option 2 for TransferLog Database, then CADIS will access Backup_TransferLog_DB.db. There is only 1 table in this
database. CADIS uses a count call and sums up the number of transfers each pharmacy has made within each month and display
the information onto the terminal.








