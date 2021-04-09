# JupyterNotebooksDEGENaCPharm

Selectivity Study:

DAY 0: harvest:
-	harvest oocytes
-	prepare injection mix and keep at -80C
o	my data are in folder /Users/Fechner/Box Sync/Fechner/TEVC-GoodmanlabBOX/Project-STFX/InjectionMixesSTFX
o	examples excel sheets in github Folder
o	adjust comments to prepare for how many recordings and which conditions to do

DAY 1: inject oocytes
-	inject oocytes and keep at 18C in L-15 + 300 uM Amilroide

DAY 4 to 7: recordings
-	for selectivity measurements I always use the following sequencs
-	monitor the cell with ContRamp1550 until it’s stable
-	use pgf 10ContStep, which is a combination of 10x ContRamp1550 and 3x STEPSens
-	monitor the cell with ContRamp1550, switch solutions and monitor until it’s stable in new solutions
-	use pgf 10ContStep 
-	and the end: use ContRamp1550, switch back to NaGluSel solution, switch to 300 uM amiloride, and wash with NaGluSel solution

The last use of the protocol ContRamp1550 (or sometimes used at the beginning) with the switch to amiloride is used to measure the amplitude of the current at -85 mV and to determine the quality of the recording.  

Analysis of Selectivity Data:

Enter Meta Data

-	Amplitude analysis amiloride sensitive current: Enter ContRamp1550 of amiloride block data into excel spreadsheet (only works 1 file per cell). They are located in the Box Folder: /Users/Fechner/Box Sync/Fechner/TEVC-GoodmanlabBOX/Project-STFX/MetaDataSTFX/MetaDelta and are called TEVCMetaSTFX111.xlsx – replace STFX111 with the current frog number.
-	Enter series for replicate of 3 in TEVCMetaSTFX112-Selectivity.xlsx (replace STFX112 with current frog number) Meta data sheet found here: /Users/Fechner/Box Sync/Fechner/TEVC-GoodmanlabBOX/Project-STFX/MetaDataSTFX


RUN MATLAB Code:

-	Clone matlab code to your computer
o	https://github.com/wormsenseLab/AnalysisFunction.git
-	Prerequisite: follow the instruction of sigtool installation for the import .dat files (see Sammy’s script as well)
-	Describe here: HOT TO INSTALL SIGTOOL
-	Open Matlab
-	Type SigTOOL in command window, click continue, if a window appears (mostly grey), just close it.
-	Before starting the analysis, navigate to the folder where you want to save the Ratio-analysis files. In my case: /Users/Fechner/Box Sync/Fechner/TEVC-GoodmanlabBOX/Project-STFX/RatioSTFX

-	Run TEVCAnalyzeLoopSTFX.m for analysis of amplitude
o	First section (%%  load dat.files), which is a script from Sammy (I copied those files in a folder locally and not using the one from Github, but Github would be fine).
	Navigate to the folder where the dat files are stored, in my case: /Users/Fechner/Box Sync/Fechner/TEVC-GoodmanlabBOX/Project-STFX/datFilesSTFX
	Loads a file ephysData (explore data, contains)
o	Second section (Load Meta Data TEVC)
	Load Meta Data for amiloride sensitive amplitude measurements
	/Users/Fechner/Box Sync/Fechner/TEVC-GoodmanlabBOX/Project-STFX/MetaDataSTFX/MetaDelta
	E.g. the file: TEVCMetaSTFX112.xlsx
o	Third section (Analysis Individual Recording)
	Enter “2” behind the variable a1 (2 is the first recording)
	In the first round, enter 2 as well behind the variable a2
	After running the code ones, you can use the variable LastFile behind a2, but it doesn’t exist in the first round yet 
	i gives the column row corresponding to the MetaData + the name o fthe recording
	if there is an error, the following error message appears
•	there were an error; This file will be skipped for analysis.
•	Debugging: type "name" in the command window below to figure our the file name.
•	typical error: 1) check if the file exist in the data structure ephysData on the right in Workspace.
•	2) Verify that the name in MetaData Sheet is correct.
•	Check if you entered the correct series
	You can create a plot for each recording by changing the variable makePlots from 0 to 1
	The code creates a “single” (!) file called RatioDeltaTEVC-STFX112.txt where STFX112 is taken from the MetaData sheet entry.

-	Run TEVCSelectivitySTFX.m for analysis of selectivity
o	First section
	Identical to amplitude section
o	Second section (Load Meta Data TEVC)
	Similar, but different MetaData sheet: /Users/Fechner/Box Sync/Fechner/TEVC-GoodmanlabBOX/Project-STFX/MetaDataSTFX
	e.g. the file TEVCMetaSTFX112-Selectivity.xlsx
o	Third Section:
	Same procedure as script above
	Enter “2” behind the variable a1 (2 is the first recording)
	In the first round, enter 2 as well behind the variable a2
	After running the code ones, you can use the variable LastFile behind a2, but it doesn’t exist in the first round yet 
	It generates an individual files for each recording, e.g.: Selectivity-TEVC-STFX112023.txt


Figure creating with Jupyter notebook:
	
-	Clone jupyter notebook to your computer:
o	https://github.com/wormsenseLab/JupyterNotebooksDEGENaCPharm.git
o	Contains analysis file for paper Fechner et al. 2021 and Nterm project
o	You have to make sure that the dabest package is installed
-	Navigate into folder on your computer via termina
-	Enter jupyter notebook in terminal 

Run RatioNterm.ipynb for amplitude measurement
-	Folder path are absolute (unfortunately), so, you need to adapt those
-	listofFiles = define the “frogs” you want to include in the analysis, e.g. STFX111, STFX112; just enter 111 and 112; STFZ will be combined automatically 
-	you also need to change the paths for saving the figures


Run Selectivity-Nterm-Data.ipynb for calculating the relative permeability






