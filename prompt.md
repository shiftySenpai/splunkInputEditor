# Splunk Input Configuration Editor 
Create a 2 column webui that allows editing of 'input.conf files in Splunk by leveraging the spec file @[nputs.conf.spec] 
Go to Splunk.com and copy the color scheme from their website and use it for the webui. Use a separate CSS and js file for the webui for faster and easier development. 

## Left Column

### Splunk Installation Directory
The left column will allow the user to input the Splunk installation directory. Save that information in settings.json file after validating that it is a valid directory by checking if bin, etc/apps, etc/deployment-apps exist. If not, display an error message and do not allow the user to proceed. When loading settings.json, Put a green checkmark next to the directory if it is valid, red X if it is not valid. 

### splunk apps listing
In etc/apps and etc/deployment-apps only display the folders that include only 'inputs.conf' files in the 'default' or 'local' directories. Provide a tree visualization of the 'apps' folder and 'deployment-apps' folder. Color code 'apps' as pink and 'deployment-apps' as orange.  

### Deploy New App/Input
Add a "Deploy New App/Input" option.  When selected, display a list of all the folders in the 'app' folder and look for 'inputs.conf' in the 'default' and 'local' folders.  Only display the folder names that meet that condition.  Check the 'deployment-apps' folder for existing folders that match what is in 'apps' folder and append " (currently deployed)" after the folder name.  

Provide checkboxes for each folder that is not currently deployed.  Create a button "Migrate to Deployment Apps Folder" and COPY the selected folders to the 'deployment-apps' folder.  

### Edit Deployment Apps
For the 'deployment-apps' folder, provide a file system tree visualization within the "deployment-apps" folder  in the same left column for the user to select the folder as which they want to edit.   

Parse the 'local' folder and see if inputs.conf is present.  If not, then copy 'inputs.conf' from the 'default' folder to the 'local' folder.  If inputs.conf does not exist in the 'local' folder, display an error message and do not allow the user to proceed.  

### Backup and Restore
For the lower half of the left column, provide options to backup and restore the 'inputs.conf' file.  Provide a list of the last 10 backups and a "Restore" button for each backup.  When the user clicks the restore button, it should display a diff simliar to how github does it.   Create a new modal window that displays the diff.  The current configuration should be in the 1st column and the most recent backup should be in the 2nd column.  The diff should be color coded and show the changes in a side by side view.  Add a "Restore" button and provide a preview windows of the changes that will be restored.  Give the option "Okay" to restore and "Cancel" to cancel the restore.

Lastly, in the Left column options, at the bottom, provide the user with the option to list the number of backups they wish to keep.  The default is '1', but the user cannot enter a value less than 1.  Based on the number entered, use the following schema for creating backup files: inputs.conf.BACKUP-n-mm/dd/yyyy  where 'n' is the backup number and the 'mm/dd/yyy'

## Right Column

### index configuration
The right column will display the contents of the 'inputs.conf' file.

When loading any inputs.conf file, check if 'index=' exists for each stanza and list all the unique indexes at the very top of the right column, add an option to add, edit, delete a list of indexes and save that list separately, settings.json so that the user can go back and use that list again.  For the index creation, add a binary option for "Event-based" or "Metrics-based" indexes.  Color code the index names blue for "Event-based" and green for "Metrcis-based" indexes.  The color coding should appear at the top and within each of the stanzas so that the user can tell which one they are selecting and what has been selected. 

## general input configuration rules and guidelines
Add exception handling so that if the user enters an input that does not conform the the .spec file, it give a warning message and a hint as to why the input is wrong and suggestions to fix by using the .spec file as a reference.

### binary input options
For input options that are binary, true/false, 0/1 provide radio buttons. 

### index options
For each respective stanza add an entry for "index" if one does not exist.  If the index does not exist, provide a drop down menu of the list of indexes that were created or detected.

### schedule options
For inputs call "schedule", it uses cron job notation.  Provide a cron translator so that the user can see the translated interval in simple terms/English.  Additionally, create a reverse cron translator that allows the user to enter their own intervals with drop down menus.  When the user completes their changes, provide a "Save Schedule" for each "schedule" input, store the cron notation in the "schedule" input. For inputs that have "intervals" it currently uses 'seconds'.  similar to the cron job, translate the 'seconds' to minutes, hours, days.  Provide the user the ability to create a cron schedule just like the "schedule" option.  
Create an option for "Run continously" as '0' for the input.

Create an option to "Run once at startup" as '-1'

Create radio buttons for each option respectively.

### perfmon inputs
For the perfmon inputs, take the list of options and turn them into a grid 4 columns wide of check boxes, option to "Check All" and "Clear All", by default the check boxes should be unchecked.  Only collect the boxes that are checked.  

### input syntax color coding
Add color coding based on the input text syntax in div.card css class.  For example, monitor:// should be blue, powershell:// should be green, WinEventLog:// should be red, script:// should be yellow.  If the input stanza is not listed in the .spec file, create a new, unique color for it.

## UI/UX Design
Indicate if the file is modified and not saved at the top of the page and the working directory in main-header div.  Give a visual indicator of the file being modified and not saved such as the text font is in italics with an asterisk (*). Provide a global Save button at the top of the page that will save all changes to the .conf file. 

If a stanza does not have an index identified, do not allow the user to save the changes.  Provide a warning message and a hint as to why the input is wrong and suggestions to fix.  Create a flashing red border around the input stanza to draw attention to the issue for each stanza that does not have an index identified.  

Add a "Save" button for each input stanza.  When the user clicks the save button, it should save the changes to the .conf file and display a message to the user that the changes have been saved. 

Give the user a notification that the file has been saved successfully with the file name and path. 



--- 




