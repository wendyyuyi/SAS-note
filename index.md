
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

## Use PROC CONTENTS to display the descriptor portion of a SAS data set.

proc contents data= text;
run;

## A blank represents a missing character value.
## A period(.) represents a missing numeric value.
