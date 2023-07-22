# Overview

This spreadsheet and Jupyter notebook form an automation system to input timecards into the Themis system via a script which processes a spreadsheet instead of interacting with Themis manually. The script can still typically take one to four hours to run for a standard full week of work, but will save a lot of time where you don't need to be present.

# Setup

The system uses docker to get you set up.

1. Install docker (see https://docs.docker.com/engine/install/ for details) - you should use Linux containers.
2. Pull image gradyfitz/umelbtoolbase using `docker pull gradyfitz/umelbtoolbase`.
3. Start the image, the easiest way to do this is using Docker Compose by running `docker-compose -d up` in the repository folder. This connects the folder you're in to the /data directory relative to the initial working directory.
4. You can then get the link to open using `docker exec worktools jupyter notebook list`, this will give you an address containing `0.0.0.0:8888`, you need to swap that component of the address with `localhost:8897` (or whichever port you've set in `docker-compose.yml`). You can then access this in a web browser.

# Timecards Entry

`timecard_calculator.xlsx` is a spreadsheet which performs the following work:

- Allows you to record details about each piece of work you do by its start and end time, the subject and activity, as well as comments explaining what work was done.
- Automatically provides checks for minimum engagement (a feature currently missing from Themis).
- Automatically provides checks for appropriate breaks (both that they're being taken for sufficient duration and sufficiently often)
- Provides more detailed view to diagnose overlapping entries.

The steps to fill timecards this way are:

1. Add activities to the "Activities" sheet, if in doubt, you can get all the information from the template which should have been added with the commencement of your contract. The tab provides the ability to split activities into what's known as a "split-rate" where you are engaged for work differing in nature. Examples of this are shown with the Casual Contract Reference and Approval ID removed. If you're not sure what kind of activities you'll need, you may like to just set "Total Components" as 1 and "Component #" as 1 for all activities and use the rows in the Themis template. You'll probably only have to do this once in the semester.
2. Add rows to the "Weekly Timesheet". Week should be either 1 or 2 depending on which week of the time period you're entering the details for and the Activity should be the name of the activity. The time should be 24-hour.
3. In the "Timecard Config" sheet, set the "Fortnight Start".
4. Once all that is entered, you should see Fortnight Starts Check, Minimum Engagement, Breaks Check and Maximum Block Duration Check all change to "OK".
5. If you like, you can check the "Time Entry Sorted" tab to check there are no overlapping end and start times. If you record your weekly timesheet in the first tab, overlaps will usually be fairly obvious.
6. Once you're ready to enter the timecard, open the "Timecard Export" tab and save the tab as a .csv (`Timecard Export.csv` is usually a good option to preserve the naming convention)
 
# Automated Entry

The final step is to actually enter the timecard. Open `themis-enter.ipynb` in the Jupyter webpage. Run each cell one by one, checking with the viewer to see when it's time to run the next cell. A number of commands are provided with limited explanation to get you out of trouble if you make mistakes (e.g. putting the wrong hours type will open a separate window, locking you out from entering anything extra in the timecard and giving a runtime exception). Not entering your username and password correctly in the sections where that needs to be entered will also require a bit of rescue. The cells hopefully give enough of a hint on how to achieve this. If you get stuck on anything, ask on the CIS Tutor Network Discord.

The final step after the script finishes is to log in to Themis and check the timecards are entered correctly and then submit them! The system doesn't check for OHS compliant daily hours so you'll need to check this yourself.

# Maintenance

This script may get updates from time to time while Themis is still in use. Supposedly the university is moving to Workday at some point, which will hopefully resolve many issues this system works around, but until then, this script will be kept up to date. =)
