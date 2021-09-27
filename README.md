# Introduction

This repo contains a Python executable that parses YottaDB journal files

# Installation

      git clone https://github.com/RamSailopal/YottaDB-journproc.git
      cd YottaDB-journproc
      cp journproc /usr/local/bin
      export journpath="/root/.yottadb/r1.32_x86_64/g"

Make sure that ydb_dist is set as the path to mupip i.e. /opt/yottadb

Then run with:

     journproc

This will output YDB journal file entries to a flat text file /tmp/journalout.txt that then gets parsed for relevant data.

Execution with no options (as above) will output all entries from the yottadb.mjl file.
      
# Options available to refine data searches:

     --glob - Search for a specific global
     --type - The type of journal activity to search for i.e. SETS or KILLS.
     --start - The Date/Time to search from
     --end - The Date/Time to search to
     --file - An alternate journal file name i.e yottadb.mjl_2021250130325
     --commit - Commit any SETS and KILLS to a commit log located at /tmp/journcommit. This can later be amended as required and committed to YDB with:

     ydb < /tmp/journcommit


     Note that the use of --commit will ignore --type and focus only on activity type SET and type KILL
     
# Commit option example use case

A global gets set up with the following entry:

     Set ^YOTTATXT("hello")="world"

The global then gets inadvertedly deleted with:

     Kill ^YOTTATXT
     
The global can be recovered by doing the following:

     journproc --glob="YOTTATXT" --commit
  
     2021-09-27 14:45:25     SET     ^YOTTATXT("hello")="world"
     2021-09-27 14:45:25     KILL    ^YOTTATXT
 

     journal commit log has been saved to /tmp/journcommit

     Amend as required and then run:

     ydb < /tmp/journcommit
     
 The file **/tmp/journcommit** contains the following entries:
 
     Set ^YOTTATXT("hello")="world"
     Kill ^YOTTATXT
     
We need to remove the inadvertent Kill execution to recover the global by editting the file and once we have done this, we can commit the changes to the YDB database by running:

     ydb < /tmp/journcommit

     
    
     

     
