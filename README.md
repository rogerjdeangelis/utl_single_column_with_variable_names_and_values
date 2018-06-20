# utl_single_column_with_variable_names_and_values
Single column with variable names and values.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Single column with variable names and values

    Same result in WPS and SAS

    github
    https://tinyurl.com/y8flmv99
    https://github.com/rogerjdeangelis/utl_single_column_with_variable_names_and_values

    see
    https://communities.sas.com/t5/Base-SAS-Programming/Need-to-Convert/m-p/470760


    INPUT
    =====

     WORK.HAVE total obs=3          |  RULES (Stack names and values when not missing)
                                    |
      ID    VAR1    VAR2     VAR3   |  ID    NEWVAR
                                    |
      1     Age             Gender  |   1     VAR1
                                    |   1     Age
                                    |   1     VAR3
                                    |   1     Gender
                                    |
      2              No             |
      3     Age      No             |

    EXAMPLE OUTPUT

    WORK.WANT total obs=10

       ID    NEWVAR

       1     VAR1
       1     Age
       1     VAR3
       1     Gender
       2     VAR2
       2     No
       3     VAR1
       3     Age
       3     VAR2
       3     No


    PROCESS
    =======

    data want;
      set have;
      array vars[*] v:;
      do i=1 to dim(vars);
         if not missing(vars[i]) then do;
            newvar=vname(vars[i]);output;
            newvar=vars[i]       ;output;
         end;
      end;
      keep id newvar;
    run;quit;


    OUTPUT
    ======

    WORK.WANT total obs=10

       ID    NEWVAR

       1     VAR1
       1     Age
       1     VAR3
       1     Gender
       2     VAR2
       2     No
       3     VAR1
       3     Age
       3     VAR2
       3     No

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;
    data have;
      informat ID Var1 Var2 Var3 $6.;
      input ID Var1 Var2 Var3 ;
    cards4;
    1 Age . Gender
    2 . No .
    3 Age No .
    ;;;;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utl_submit_wps64('
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    data want;
      set wrk.have;
      array vars[*] v:;
      do i=1 to dim(vars);
         if not missing(vars[i]) then do;
            newvar=vname(vars[i]);output;
            newvar=vars[i]       ;output;
         end;
      end;
      keep id newvar;
    run;quit;
    proc print;
    run;quit;
    ');

