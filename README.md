PiScraper 
Version: 1.0.0, last updated 2018/07/18
README.txt, last updated 2018/07/18

Developed by Emilie Campbell, M.Sc.
Credit: Robert Campbell, M.S.



#-----
#-----
#-----



#-----WHAT IT IS:
PiScraper is a webscraper that checks for updates to prescribing information (PI) on manufacturer websites. When updated, a PDF of the new PI is either downloaded or created, and  put into a folder. The outdated copy is moved to an archival folder for continued access

PiScraper does not have access to red-line labels or any other labels that have not received FDA approval or have not yet been published online



#-----UPDATES:
The most recent version of PiScraper is hosted at: https://github.com/emmiemc/PiScraper

v1.0.0:
* updated file structure and naming
* added PI brand, URL pairs



#-----
#-----
#-----



#-----SYSTEM REQUIREMENTS:
	OSX
	bash 4.4
	pdftotxt
	wkhtmltopdf

POSSIBLY NOW REQUIRES EITHER GHOSTSCRIPT (brew install gs) OR PDFTK (https://www.pdflabs.com/tools/pdftk-server/)

All of the system requirements can be downloaded by following the instructions below. Current instructions use Homebrew to download these packages with minimal effort. If you wish to avoid using Homebrew, or want more information on any of the packages being used, please visit the websites listed below:

* Homebrew:	 https://brew.sh/
* bash 4.4:	 https://tiswww.case.edu/php/chet/bash/bashtop.html
* pdftotxt:	 https://poppler.freedesktop.org/
* wkhtmltopdf:	 https://wkhtmltopdf.org/



Instructions:

1. Open Terminal: /Macintosh HD/Applications/Utilities/Terminal.app

2. Type: /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

3. Hit enter and follow prompts to enter password

4. Type: brew install bash

5. Hit enter

6. Type: brew install poppler

7. Hit enter

8. Type: brew cask install wkhtmltopdf

9. Hit enter and follow prompts to enter password



#-----FILES:
The installation package for this should include a zipped folder with:

* README.txt
* LICENSE.txt
* /PiScraper
	* /_CODE
		* PiScraper.command

PDFs of PIs will be housed in the /PiScraper folder

Once you've run PiScraper at least once, two more folders: /_ARCHIVED (in /PiScraper) and /_LOGS (in /_CODE) will appear. Outdated PIs which have been replaced by new versions will be housed in the ARCHIVED folder, and run logs will be housed in the LOGS folder



#-----INSTALLATION:
If you are missing any of the system requirements listed above, please see the associated installation instructions on how to download them before running PiScraper

If you would like to set up PiScraper to run automatically via the crontab, please see the crontab installation instructions at the bottom of the file to add PiScraper to your crontab



Installation instructions:

1. Place the zipped PiScraper folder in the desired location. Unzip

2. Make folder named "_ARCHIVED" inside /PiScraper folder

3. Make folder named "_LOGS" inside /PiScraper/_CODE folder

2. Open Terminal: /Macintosh HD/Applications/Utilities/Terminal.app

3. Type: chmod +x and drag PiScraper.command (inside the _CODE folder) onto the cursor. The text line should look something like this: chmod +x /Users/ecampbell/Dropbox/PiScraper/_CODE/PiScraper.command

4. Hit enter

5. Exit Terminal
	


There are 3 instances in which PiScraper will e-mail you with its results: when the script is complete, when a new PI has been added to the folder, and when it has found an updated PI. In order to get these e-mails, you must input what e-mail you want to receive these notifications at



E-mail notification instructions:

1. Open PiScraper.command using a text editor (this can be done by right-clicking on the file and using "Open With")

2. Replace each instance of [YOUR E-MAIL] with the e-mail you want updates sent to

3. Save and close

NOTE: If you'd like to remove e-mail notifications, place a hashtag symbol at the beginning of each line (in front of "mail", i.e. "#mail -s...",  containing [YOUR E-MAIL]



In the event that a brand you would like to receive updates on is not included in PiScraper, new brands can be added. As of July 2018, the following formats are currently supported: 

* PIs following the Code of Federal Regulations (CFR), Title 21, §201.56, 201.57 and 201.80 (PIs post-2006)

NOTE: See Physician Labeling Rule (PLR) requirements for more information: https://www.fda.gov/drugs/guidancecomplianceregulatoryinformation/lawsactsandrules/ucm084159.htm

* PIs containing revision dates within the first 2 pages that are clearly labelled as such using the format: Revised: MM/YYYY or Revised: M/YYYY, Issued: MM/YYYY or Issued M/YYYY



Formatting for new entries is as follows:
ARRAY[*BRAND*]="*URL*", where *BRAND* is the name of the drug

Ex: ARRAY[HUMIRA]="http://www.rxabbvie.com/pdf/humira.pdf"

NOTE: each BRAND element needs to be unique, so that you don not wind up overwriting other files. This includes any different indications, doses or administration methods that have unique PIs, such as LUPRON-Urology versus LUPRON-Pediatric, CARDENE 0.1 mg/mL versus CARDENE 0.2 mg/mL, or EMEND-IV versus EMEND-PO

NOTE: URLs must be direct to a PDF, and must be static and cannot contain date modifiers, eg. http://www...HUMIRA-PI_2018-07.pdf. If the URL contains a date modifier, it will continuously check the same dated location for a new PI, resulting in false negatives when a new PI has been posted elsewhere



Update PI brands list instructions:

1. Open PiScraper.command using a text editor (this can be done by right-clicking on the file and using "Open With")

2. Underneath "#populate ARRAY with BRAND, URL pairs" (under "#-----CREATE ARRAY OF BRANDS & URLS-----"), insert your BRAND, URL pair according to the formatting listed above

NOTE: Brands are currently organized alphabetically

3. Save and close
	
		

#-----
#-----
#-----



#-----UNINSTALLATION:
There are two uninstallation processes: one which only removes PiScraper, and one which removes PiScraper, Homebrew, and and all Homebrew packages. I recommend using the former (listed first on this page), in the event you want to continue to use any of the Homebrew formulae installed for PiScraper, or any Homebrew formulae you may have otherwise installed

If you have set up PiScraper to run automatically via the crontab, please see the uninstallation instructions at the bottom of the page to remove it from your crontab as well



Instructions, removes PiScraper only:

Delete PiScraper folder and subfiles



Instructions, removes Homebrew and all formulae:

1. Open Terminal: /Macintosh HD/Applications/Utilities/Terminal.app

2. Type: ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"

NOTE: this assumes you want to remove the entire Homebrew package and all formulae. If you want to keep Homebrew for use with any other 

3. Hit enter



#-----
#-----
#-----



#-----AUTO-RUNNING:
I recommend running this every weekday at noon. This will require your computer to be on and have internet access at that time

To set it up to automatically run, you'll need to edit the crontab, a file that lists commands scheduled to run at regular intervals



Installation instructions:

1. Open Terminal: /Macintosh HD/Applications/Utilities/Terminal.app

2. Type: env EDITOR=nano -e crontab

3. Hit enter

4. Enter: 0 12 * * 1-5 ~path/PiScraper/_CODE/PiScraper.command 2>&1 | tee ~path/PiScraper/_CODE/_LOGS/LOG_`date +\%Y-\%m-\%d`.txt

NOTE: replace "~path" with the filepath to PiScraper file.
Ex: /Users/ecampbell/Dropbox/PiScraper/_CODE/PiScraper.command

NOTE: this will run every weekday at noon and export all output (StdERR and StdOUT) to a log file. To learn more about the crontab, go to: https://crontab.guru/

5. Hit control+x

6. Hit y

7. Hit enter

5. Exit Terminal



Uninstallation instructions:

1. Open Terminal: /Macintosh HD/Applications/Utilities/Terminal.app

2. Type: env EDITOR=nano -e crontab

3. Hit enter

4. Delete line with PiScraper information (see installation instructions above for what this should look like)

5. Hit control+x

6. Hit y

7. Hit enter

5. Exit Terminal
