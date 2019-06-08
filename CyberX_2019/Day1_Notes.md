# Day 1
- - - - -
### Splunk Overview

**Common Info Model Fields**
* user
* signature
* action 
* severity
* src
* dest
* dvc
* app 
  * e.g. ssh, web, ssl, win
* bytes 

**Data Sources**
* PF Sense Firewall
  * https://splunkbase.splunk.com/app/1527
* Splunk Essentials for ICS Security & Compliance
  * https://splunkbase.splunk.com/app/4150
* WINDOWS (Event Log/ Sysmon)
* Linux
* Active Directory
* NMAP
  * https://splunkbase.splunk.com/app/3056
  
- - - - -
### Downloading/Setting Up Splunk
(**NOTE:** if using splunk for an enterprise purpose **DO NOT** USE Windows)
1. Signup for a Splunk Account (Free)
2. Download Splunk software (Free)
   1. Windows (64/32)
   2. Linux (64bit, .rpm/.tgz/.deb)
   3. MacOS (OSX 10.10/11/12, .dmg/.tgz)
3. Verify Email for Splunk Account
4. Install Splunk Software
5. Install Splunk Add-On (You can find this by...)
   1. Going to your splunk page
   2. Manage Apps (Drop Down Option in Top Left)
   3. Browse More Apps
       1. Check the "Add-On" App Type Option
       2. Search for correct Add-On
           1. Linux/Unix/MacOS :: Search "Splunk Linux", choose Splunk Add-on for Unix and Linux
           2. Windows :: Search "Splunk Windows", choose Splunk Add-on for Microsoft Windows
       3. Install selected Add-On
   4. Navigate back to Manage Apps, on your Splunk web-page
   5. Click "Install from App" (Top Right)
       1. Browse for downloaded Add-on/App
       2. Upload
6. Set Splunk up on local machine
   1. **Linux/MacOS**
       1. Open up Terminal
       2. Navigate to `/Applications/Splunk/etc/apps/Splunk_TA_nix/default`
       3. `vi inputs.conf`
       4. set `Library/Logs` = 0 
            1. (i.e. False)
       5. exit vi 
            1. (`Press :`)
            2. (`Press q`)
       6. Navigate to `(Restart Path)`
            1. Restart Splunk
       7. Open up downloaded splunk app via GUI 
            1. (this will open browser)
       8. Navigate to the Search & Reporting App
       9. Search: `index=main`
       10. This is everything your local computer is logging, to find other items search other strings
   2. **Windows**
       1. Navigate to `/programfiles/splunk/etc/apps/splunk_TA_cisco-asa/default`
       2. open `inputs.conf`
       3. set `Library/Logs` = 0 
            1. (i.e. False)
       6. Navigate to `(Restart Path)`
            1. Restart Splunk
       7. Open up downloaded splunk app via GUI 
            1. (this will open browser)
       8. Navigate to the Search & Reporting App
       9. Search: `index=main`
       10. This is everything your local computer is logging, to find other items search other strings
- - - - -
# SPLUNK Use Cases
1. What Kind of Data do we have?
   1. tstats count where index=* groupby index, sourcetype
2. Correlate in Place.
   1. Gather a pool of data.
   2. use a table to form the data for easy numeric tests.
   3. Perform tests to make decisions.
3. why is my search slow
   1. Volume of data
      1. Limit the Time range
      2. Large and/or 
4. Search processing language
   1. Search & Filter | Munge | report | cleanup
      1. sourcetype=access*
      2. | eval KB=bytes/1024
      3. | stats sum(KB) dc(clientip)
      4. | rename sum(KB) AS "Total MB" dc(clientip) AS "Unique Customers"
5. Search Construction
   1. Be Specific
   2. Use Unique Terms
   3. Avoid NOTs use AND/OR
   4. Avoid Joins
      1. foo | stats count by unix | joing[search bar |stats count by qux]
      2. foo OR bar | stats count(eval(searchmatch....
- - - - -
## Additional Useful Add-Ons
* Python for Scientific Computing (for Mac)
* Pulse Connect Secure Add-on for Splunk

## Additional Useful Apps
* Monitoring Docker - Metrics and Log Forwarding
* Monitoring Kubernetes - Metrics and Log Forwarding
* Splunk Machine Learning Toolkit
* VersionControl For Splunk
* Splunk Security Essentials

- - - - -
## Additional Web Resources
* https://www.malwarearchaeology.com/
