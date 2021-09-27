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
     --start - The Date/Time for search from
     --end - The Date/Time to search to
     --file - An alternate journal file name i.e yottadb.mjl_2021250130325
     --commit - Commit any SETS and KILLS to a commit log located at /tmp/journcommit. This can later be amended as required and committed to YDB with:

     ydb < /tmp/journcommit


     Note that the use of --commit will ignore --type
