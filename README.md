# utl_crosstab_dataset_3_lines_of_code
Transpose and summarize row percents in three lines of code.  Minimal code for a crosstab.

    ```  SAS forum: Cross tab of percents in three lines of working code                                                                                                          ```
    ```                                                                                                                                                               ```
    ```    or a Cross tab in three lines of working code                                                                                                              ```
    ```                                                                                                                                                               ```
    ```    WORKING CODE (pretty much all of it)                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```         %utl_gather(have,id,var,id,havNrm,valFormat=$10.);                                                                                                    ```
    ```                                                                                                                                                               ```
    ```         ods output rowprofiles=xporow;                                                                                                                        ```
    ```         proc corresp data=havNrm all dimens=1 ;                                                                                                               ```
    ```           tables id, var;                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://goo.gl/TqbYau                                                                                                                                        ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/stack-statistics-of-multiple-variables-in-the-same-table/m-p/403375                                      ```
    ```                                                                                                                                                               ```
    ```  see Alea Iacta for the gather macro                                                                                                                          ```
    ```  https://github.com/clindocu/sas-macros-r-functions                                                                                                           ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  HAVE                                                                                                                                                         ```
    ```  ====                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  WORK.HAVE total obs=8                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  Obs    ID    Q1          Q2          Q3                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```   1     1     hard        veryhard    easy                                                                                                                    ```
    ```   2     2     veryhard    hard        hard                                                                                                                    ```
    ```   3     3     veryhard    easy        hard                                                                                                                    ```
    ```   4     4     hard        hard        veryhard                                                                                                                ```
    ```   5     1     easy        hard        veryhard                                                                                                                ```
    ```   6     2     hard        veryhard    hard                                                                                                                    ```
    ```   7     3     hard        veryhard    easy                                                                                                                    ```
    ```   8     4     hard        hard        veryhard                                                                                                                ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  WANT (SAS datset)                                                                                                                                            ```
    ```  =================                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```    WORK.WANT total obs=3                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```    Obs    LABEL     EASY     HARD    VERYHARD                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     1      Q1      0.125    0.625      0.250                                                                                                                  ```
    ```     2      Q2      0.125    0.500      0.375                                                                                                                  ```
    ```     3      Q3      0.250    0.375      0.375                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```  *                _              _       _                                                                                                                    ```
    ```   _ __ ___   __ _| | _____    __| | __ _| |_ __ _                                                                                                             ```
    ```  | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |                                                                                                            ```
    ```  | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |                                                                                                            ```
    ```  |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data have;                                                                                                                                                   ```
    ```  input (id q1 q2 q3) ($);                                                                                                                                     ```
    ```  cards4;                                                                                                                                                      ```
    ```  1 hard veryhard easy                                                                                                                                         ```
    ```  2 veryhard hard hard                                                                                                                                         ```
    ```  3 veryhard easy hard                                                                                                                                         ```
    ```  4 hard hard veryhard                                                                                                                                         ```
    ```  1 easy hard veryhard                                                                                                                                         ```
    ```  2 hard veryhard hard                                                                                                                                         ```
    ```  3 hard veryhard easy                                                                                                                                         ```
    ```  4 hard hard veryhard                                                                                                                                         ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %utl_gather(have,id,var,id,havNrm,valFormat=$10.);                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ods exclude all;                                                                                                                                             ```
    ```  ods output rowprofiles=want;                                                                                                                                 ```
    ```  proc corresp data=havNrm all dimens=1 ;                                                                                                                      ```
    ```    tables id, var;                                                                                                                                            ```
    ```  run;quit;                                                                                                                                                    ```
    ```  ods select all;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```  1425  ods exclude all;                                                                                                                                       ```
    ```  1426  ods output rowprofiles=want;                                                                                                                           ```
    ```  1427  proc corresp data=havNrm all dimens=1 ;                                                                                                                ```
    ```  1428    tables id, var;                                                                                                                                      ```
    ```  1429  run;                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  NOTE: The data set WORK.WANT has 3 observations and 4 variables.                                                                                             ```
    ```  NOTE: PROCEDURE CORRESP used (Total process time):                                                                                                           ```
    ```        real time           0.06 seconds                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```

