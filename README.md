# JupyterNotebooksDEGENaCPharm
Jupyter notebooks create figures for amplitude data (change in current and ratio) and selectivity data (realtive permeability) from TEVC data. There are two folders: 1) containing the figures for the [Fechner et al. 2021, JGP paper](https://rupress.org/jgp/article/153/4/e202012655/211847/DEG-ENaC-ASIC-channels-vary-in-their-sensitivity) and 2) figures to analyze data from N-terminal mutation study project. FOr the Dose response figures, data were analyzed with IgorPro, Individual dose-response curve fitted with the HIll equation and the fitted values for IC50 and EC50 entered into excel data shets. 

## Make Figures from TEVC data

### Clone matlab code to your computer
- [Link to wormsense Guthub repo](https://github.com/wormsenseLab/AnalysisFunction.git)

### Analyze data with TEVC Matlab code
- Follow the description to analyze [TEVC](https://github.com/wormsenseLab/AnalysisFunction) amplitude with TEVCAnalyzeLoopSTFX.m and selectivity with TEVCSelectivitySTFX.m 

### Figure creating with Jupyter notebook:
	
- Clone jupyter notebook to your computer:
	- https://github.com/wormsenseLab/JupyterNotebooksDEGENaCPharm.git
	- Contains analysis file for paper Fechner et al. 2021 and Nterm project
	- You have to make sure that the dabest package is installed for estimation plots
	- 
-	Navigate into folder on your computer via termina
-	Enter jupyter notebook in terminal 

Run RatioNterm.ipynb for amplitude measurement
-	Folder path are absolute (unfortunately), so, you need to adapt those
-	listofFiles = define the “frogs” you want to include in the analysis, e.g. STFX111, STFX112; just enter 111 and 112; STFZ will be combined automatically 
-	you also need to change the paths for saving the figures


Run Selectivity-Nterm-Data.ipynb for calculating the relative permeability

## Package requirement

* Python XX
* dabest
* 

####  Add heka_reader to PYTHONPATH
import sys
fpath = '/Users/Fechner/Dropbox/PythonImport/heka_reader' #MAC
sys.path.append(fpath)
import heka_reader

#### got the heka reader from here
[Heka Reader](https://github.com/campagnola/heka_reader)

- clone the repository to your computer (move to directory with terminal commands. Mine here is called PythonStuff at the moment: change name)
    - git clone https://github.com/campagnola/heka_reader.git
- the heka reader enables to read and access the .dat files (to work in jupyter notebook, you habe to append the heka_reader to the path where the heka reader is stored)
- browser.py enables to easily browse for recordings within a .dat comparable to Igor or other similar programs
- I changed the following in my local browser.py version, because the functions output was a tuple:
    - def load_clicked():
    - Display a file dialog to select a .dat file
    - file_name = pg.QtGui.QFileDialog.getOpenFileName()
    - if isinstance(file_name, tuple):   (ADDED THIS LINE)
        -    file_name = file_name[0]    (ADDED THIS LINE)
    - if file_name == '':
        -    return
    - load(file_name)

#### Brief example for heka_reader: we changed 

    *Load a .dat file
    bundle = Bundle(file_name)
    
    *Select a trace
    trace = bundle.pul[group_ind][series_ind][sweep_ind][trace_ind]
    
    *Print meta-data for this trace
    print(trace)
    
    *Load data for this trace
    data = bundle.data[group_id, series_id, sweep_ind, trace_ind]

