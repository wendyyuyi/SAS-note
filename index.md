
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
  var last_name first_name;
run;
