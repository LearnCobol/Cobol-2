# Cobol
A simple application developed in Cobol.

Hello,

I’ve been learning Cobol as part of my career development plan at work and thought I would share with you a simple, but user-friendly, application that I wrote to demonstrate my skills. 
The work that I have carried out centres round a simple Text User Interface (TUI) that interacts with an indexed file (clnt.dat). I advise anyone learning Cobol to follow this course on the University of Limerick website first.
I’ve adopted the usual three-tier architecture for developing the software.

Data tier
There are two indexed files:
-	Clnt.dat, which stores client information - client number, surname, dob and balance.
-	Cont.dat, which stores the next client number – this, in my opinion, is the best way to automatically generate the next client number when you want to add another client.

Logic tier
There are two programs that are responsible to handling the interactions between the presentation layer and data layer:
-	Clntio: this is a linkage file that accepts an operation character (such as “Q” for querying the clnt file) and client information from the presentation tier. The clntio program then performs the necessary operation and returns four parameters: the client record, a navigation status (used by the Presentation tier to control navigation) and a message (used by the presentation layer to inform users of why certain actions cannot be carried out – e.g. pressing ‘Next’ on the last record should display an ‘End of file’ message)
-	Contio: this is responsible for retrieving the next client number (stored on cont.dat) and then returning it to clntio where it will be used for the new client. The program then increments the next client number by one.
	
Presentation Layer
There are two distinctive screens that the user interacts with
-	Clntgui: this is a TUI that displays all the details for one client record. The user can navigate through the records (‘Next’ and ‘Prev’), query records by client number, and also add, update and delete records. Input is limited to the surname and date of birth, but there is extensive validation on these fields.
-	Clntbrws: this is called when you select the ‘Browse’ option clntgui screen. This screen displays a list of ten clients per page and provides the user with a quicker method of browsing through clients. Users can use navigate through the pages and also select a record by moving the screen cursor up and down the page and pressing F9. Selecting the record will reload the clntgui screen with the values for the selected client.

Additional Functions
Some readers will notice that there are additional programs on this project.
-	Dates: one way to make your lives much easier as a software developer is to store dates in a numeric format that represents the number of days since a particular date. In the context of OpenCobol (now known as GNU Cobol) all numeric dates are calculated from 1st January 1601. Why use this? Well, it is much easier to perform calculations when using dates stored as numerics. I have validation that prevents the user from entering a date of birth prior to 1st January 1900 or after ‘today’. The dates.cob program converts dates between the numeric figure and the format that is more recognisable to us: yyyymmdd.
-	Dropclnts: as I have been developing the software I wanted a quick way to delete all the records in the clnt file and reset the next client number back to 1. Just by executing the ‘open output ClientFile’ and ‘open output ContinueFile’ statements the clnt.dat and cont.dat files are overwritten with a blank file. I then perform a quick function to set the next client number to 1.
-	Enrol: I wanted to make a quick program that will populate the clnt.dat file with records from a csv file. Be warned: there are no validation checks. My intentions were to automate a process that I would have otherwise found tedious – entering the records manually in clntgui. I decided to publish this as it could be helpful for those learning Cobol.

The software was developed using OpenCobol 1.1 which was packaged with Slackware Linux 16. It is advised to execute this program on a basic terminal application, such as Konsole, as you will need full use of Function keys F1 to F12. Some advanced terminals reserve the Function keys for their intended purposes, which results in my application malfunctioning.

The program can be compiled using the compile.sh shell script and run via the command: cobcrun clntgui.

Thank you for reading and showing an interest in this project. I hope you can find some use for it.

Kind regards,

Andy 
