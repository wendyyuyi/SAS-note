
### DATA steps typically create SAS data sets.
data text;
  infile ".csv" dlm="";
  input first$ second$ ;
run;

### PROC steps typically process SAS data sets to generate reports and graphs, and to manage data.
proc print data=text;
run;
  
proc means data= text;


data  ;
  length firstname $ 12;
  infile ".csv" dlm=",";
  input firstname $ ;
run;

### Use PROC CONTENTS to display the descriptor portion of a SAS data set.


proc contents data= text;
run;

### A blank represents a missing character value.
### A period(.) represents a missing numeric value.

### Work is a temporary library where you can store and access SAS data sets for the duration of the SAS session. It is the default library.
When a data set is in the temporary Work library, you can use a one-level name (for example, newsalesemps).

### Sashelp is a permanent library that contains sample SAS data sets you can access during your SAS session.

data work.donations;
	infile "&path\donation.dat";
	input Employee_ID Qtr1 Qtr2 Qtr3 Qtr4;
	Total=mean(Qtr1,Qtr2,Qtr3,Qtr4); 
run;
proc contents data=work.donations;
run;
proc print data=work.donations; 
run;

### The VAR statement selects variables to include in the report and specifies their order.
proc print data=orion.sales;
  var last_name first_name Salary;
  where Salary<25000 AND Job_Title contains 'rep' or Job_Title ? 'rep';
run;

![image]
(https://github.com/wendyyuyi/SAS-note/blob/master/sas.png)

###  A percent sign (%) specifies that any number of characters can occupy that position.
###  An underscore (_) specifies that exactly one character must occupy that position.

### The ID statement specifies the variable or variables to print at the beginning of each row instead of an observation number.
	
ID variables;
	
	
### Sort procedure
proc sort data=orion.sales
	  out= work.sales;
     by Salary;
run;

### Displaying Titles and Footnotes
title1 'I'm title!';
footnote1 'hello';



title;
footnote;

![title & footnode]
(https://github.com/wendyyuyi/SAS-note/blob/master/title.png)

### Use a LABEL statement and the LABEL option to display descriptive column headings instead of variable names.

### The FORMAT statement associates a format with a variable.
proc print data=orion.sales noobs;
	format Salary dollar8. Hire_Date mmddyy10.;
	var Last_Name First_Name Job_Title Salary Hire_Date;
run;

##################################################

proc format;
	value tiers 0-49999='tier 1' 50000-99999='tier 2' 100000-250000='tier 3';
run;
data work.salaries;
	input Name $ salary;
	datalines;
Abi 50000
Mike 65000
Jose 50000.00
Joe 37000.50
Ursula 142000
;

proc print data=work.salaries;
	format salary tiers.;
run;

##################################################

proc format;
%% Character formats must have a dollar sign
as the first character and a letter or underscore as the second character.	
   value $gender 'F'='Female'
                 'M'='Male'
               other='Invalid code';

   value salrange .='Missing salary'
      20000-<100000='Below $100,000'
      100000-500000='$100,000 or more'
              other='Invalid salary';
run;
