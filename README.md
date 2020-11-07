# Pyalmanac-Py2

**'End of Life' ANNOUNCEMENT**

Pyalmanac is nearing the end of its useful days. Almanacs generated after the next few 
years should not be used for navigational purposes. SFalmanac (or Skyalmanac with
some restrictions regarding the accuracy of sunset/twilight/sunrise and moonrise/moonset)
are the new norm as these are based on the more accurate algorithms currently employed
in the NASA JPL HORIZONS System (the same algorithms are implemented in Skyfield).

Pyalmanac is implemented using PyEphem, which in turn uses XEphem that is based on the
VSOP87D algorithms. XEphem is also 'end of life' as no further updates are planned,
however the major discrepancies are related to the projected speed of Earth's rotation.
The discrepancies in GHA between PyEphem and Skyfield 1.31 can be summarized thus:

* in 2020:&nbsp;&nbsp; 00.0 to 00.1 arcMINUTES GHA too high
* in 2030:&nbsp;&nbsp; 04.0 to 04.8 arcMINUTES GHA too high
* in 2050:&nbsp;&nbsp; 13.9 to 14.9 arcMINUTES GHA too high
* in 2100:&nbsp;&nbsp; 38.0 to 40.2 arcMINUTES GHA too high
* in 2200:&nbsp;&nbsp; 90.1 to 94.1 arcMINUTES GHA too high

The GHA discrepancy applies to the sun, moon, the First Point of Aries and all planets.

**Description**

Pyalmanac is a Python 2.7 script that creates the daily pages of the Nautical Almanac. These are tables that are needed for celestial navigation with a sextant. Although you are strongly advised to purchase the official Nautical Almanac, this program will reproduce the tables with no warranty or guarantee of accuracy.

Pyalmanac-Py2 was developed based on the original Pyalmanac by Enno Rodegerdts. Various improvements, enhancements and bugfixes (listed below) are implemented. Pyalmanac contains its own star database (similar to the database in PyEphem 3.7.6), however the accuracy was poor. It is updated with data from the Hipparcos Catalogue and the GHA/Dec data now matches a sample page from a Nautical Almanac exactly or at the most is within 0°0.1', which is very good.

NOTE: two scripts are included (both can be run): 'pyalmanac.py' and 'increments.py'  
NOTE: Pyalmanac contains its own star database - it does not use the version supplied with PyEphem, hence updating from 3.7.6 to 3.7.7 is harmless. Star names are chosen to comply with Nautical Almanacs.  
NOTE: a Python 3 script with identical functionality can be found at: https://github.com/aendie/Pyalmanac-Py3  
NOTE: a [Skyfield](https://rhodesmill.org/skyfield/) version of Pyalmanac is available here: https://github.com/aendie/SFalmanac-Py2

This fork of the original code, which can be found at https://github.com/rodegerdts/Pyalmanac, in general includes:

* **various bugfixes** (in accordance with USNO data), e.g. ...  
     - a declination of 20°60.0 now prints as 21°00.0;  
     - the same applies to times ('03:60' now prints as '04:00');  
     - incorrect date display in the **SHA and Mer.pass** section;  
     - some incorrect/missing dates for sunrise/sunset or moonrise/moonset;  
     - a few incorrect dates for Moon (upper) Transit or Antitransit (lower);  
     - incorrect times (by 1 minute) for Moon (upper) Transit or Antitransit (lower) due to truncation instead of rounding (506 such cases in 2019);  
     - a Mer. Pass. of '6:15:' now prints correctly as '06:15';  
     - an event occuring within 30 seconds before midnight now lists as 00:00 the next day.

* **enhanced functionality**, e.g. ...  
     - more accurate star database (based on the Hipparcos Catalogue);  
     - user input checks are performed when entering the requested data;  
     - a brief version of the tables can be created instead of the whole year;  
     - a '**modern**' table format in addition to the 'traditional' format layout;  
     - **three Moonrise/Moonset** events per day can be shown (e.g. on 7th July 2019 at 70°N);  
     - temporary files are deleted after running 'increments.py'.

* **cosmetic improvements**, e.g. ...  
     - Declinations/Latitudes are N/S instead of positive and negative;  
     - Declinations are always printed with two digits for degrees;  
     - line spacing (row padding) within the tables has been improved;  
     - minor table header improvements;  
     - addition of the minutes symbol on the Moon’s v, d and HP data rows.

* **a few typo corrections**

and the results have been crosschecked with USNO data to some extent.  
(Constructive feedback is always appreciated.)

**UPDATE: Aug 2019**

This includes a minor bugfix, improved and standardised output formatting, and cosmetic enhancements to the code. The idea is to have the same output formatting for both the PyEphem-based and Skyfield-based versions. If both are opened in a PDF reader, then simply by switching between tabs will highlight the data that has changed. Also one can now generate multiple years of almanacs with a single run. And output messages can be sent to the console or written to a log file if the log file has been opened.

**UPDATE: Nov 2019**

Declination formatting has been changed to the standard used in Nautical Almanacs. In each 6-hour block of declinations, the degrees value is only printed on the first line if it doesn't change. It is printed whenever the degrees value changes. The fourth line has two dots indicating "ditto". This applies to all planet declinations and for the sun's declination, but not to the moon's declination as this is continuously changing.

This also includes some very minor changes and an improved title page for the full almanac with a star chart that indicates the northern navigational stars.

**UPDATE: Jan 2020**

The Nautical Almanac tables now indicate if the sun never sets or never rises; similarly if the moon never sets or never rises. The constant "search_next_rising_sun" in **config.py** determines how the *SunNeverSets* or *SunNeverRises* state is calculated. The code also has cosmetic improvements.  
P.S. The *Overfull \hbox in paragraph...* messages can be ignored - the PDF is correctly generated.

**UPDATE: Feb 2020**

The main focus was on cleaning up the TeX code and eliminating the *Overfull/Underfull hbox/vbox* messages. Other minor improvements were included.

**UPDATE: Mar 2020**

A new parameter in *config.py* enables one to choose between A4 and Letter-sized pages. A [new approach](https://docs.python.org/3/whatsnew/3.0.html#pep-3101-a-new-approach-to-string-formatting) to string formatting has been implemented:
the [old](https://docs.python.org/2/library/stdtypes.html#string-formatting) style Python string formatting syntax has been replaced by the [new](https://docs.python.org/3/library/string.html#format-string-syntax) style string formatting syntax. 

**UPDATE: Jun 2020**

The Equation Of Time is shaded whenever EoT is negative indicating that apparent solar time is slow compared to mean solar time (mean solar time > apparent solar time).

## Requirements

&nbsp;&nbsp;&nbsp;&nbsp;Most of the computation is done by the free Pyephem library.  
&nbsp;&nbsp;&nbsp;&nbsp;Typesetting is done by MiKTeX or TeX Live so you first need to install:

* Python v2.x (2.6 or later)
* PyEphem
* TeX/LaTeX&nbsp;&nbsp;or&nbsp;&nbsp;MiKTeX&nbsp;&nbsp;or&nbsp;&nbsp;TeX Live

&nbsp;&nbsp;&nbsp;&nbsp;**DEPRECATION:** Python 2.7 will reach the end of its life on January 1st, 2020.  
&nbsp;&nbsp;&nbsp;&nbsp;Please upgrade your Python as Python 2.7 won't be maintained after that date.  
&nbsp;&nbsp;&nbsp;&nbsp;A future version of pip will drop support for Python 2.7.

## Files required in the execution folder:

* &ast;.py
* Ra.jpg
* A4chartNorth_P.pdf

### INSTALLATION GUIDELINES on Windows 10:

&nbsp;&nbsp;&nbsp;&nbsp;Install Python 2.7 and MiKTeX from https://miktex.org/  
&nbsp;&nbsp;&nbsp;&nbsp;When MiKTeX first runs it will require installation of additional packages.  
&nbsp;&nbsp;&nbsp;&nbsp;Run Command Prompt as Administrator, go to your Python Scripts folder and execute, e.g.:

&nbsp;&nbsp;&nbsp;&nbsp;**cd C:\\Python27\\Scripts**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pyephem**

&nbsp;&nbsp;&nbsp;&nbsp;NOTE: if Python 3 is already installed, you need to be in the Scripts folder - otherwise the Py3 version of pip will execute.

&nbsp;&nbsp;&nbsp;&nbsp;Put the Pyalmanac files in a new folder, run Command Prompt and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python.exe pyalmanac.py**

&nbsp;&nbsp;&nbsp;&nbsp;However, if Python 3 is also installed, start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**py -2 pyalmanac.py**


### INSTALLATION GUIDELINES on Ubuntu 18.04:

&nbsp;&nbsp;&nbsp;&nbsp;Ubuntu 18 and earlier come with Python 2 preinstalled,  
&nbsp;&nbsp;&nbsp;&nbsp;however pip may need to be installed:  
&nbsp;&nbsp;&nbsp;&nbsp;**sudo apt install python-pip**  
&nbsp;&nbsp;&nbsp;&nbsp;Note: Ubuntu 20.04 comes with Python 3 preinstalled, which is preferable to Python 2.

&nbsp;&nbsp;&nbsp;&nbsp;Install the following TeX Live package:  
&nbsp;&nbsp;&nbsp;&nbsp;**sudo apt install texlive-latex-extra**

&nbsp;&nbsp;&nbsp;&nbsp;Install the required astronomical library:  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pyephem**

&nbsp;&nbsp;&nbsp;&nbsp;Put the Pyalmanac files in a folder and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python pyalmanac.py**  


### INSTALLATION GUIDELINES on MAC:

&nbsp;&nbsp;&nbsp;&nbsp;Every Mac comes with python preinstalled.  
&nbsp;&nbsp;&nbsp;&nbsp;(Please choose the Python 3 version of Pyalmanac if Python 3.* is installed.)  
&nbsp;&nbsp;&nbsp;&nbsp;You need to install the PyEphem library to use Pyalmanac.  
&nbsp;&nbsp;&nbsp;&nbsp;Type the following commands at the commandline (terminal app):

&nbsp;&nbsp;&nbsp;&nbsp;**sudo easy_install pip**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pyephem**

&nbsp;&nbsp;&nbsp;&nbsp;If this command fails, your Mac asks you if you would like to install the header files.  
&nbsp;&nbsp;&nbsp;&nbsp;Do so - you do not need to install the full IDE - and try again.

&nbsp;&nbsp;&nbsp;&nbsp;Install TeX/LaTeX from http://www.tug.org/mactex/

&nbsp;&nbsp;&nbsp;&nbsp;Now you are almost ready. Put the Pyalmanac files in any directory and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python pyalmanac**  
&nbsp;&nbsp;&nbsp;&nbsp;or  
&nbsp;&nbsp;&nbsp;&nbsp;**./pyalmanac**
