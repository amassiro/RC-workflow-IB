# RC-workflow-IB

Example:

    https://github.com/cms-sw/cmssw/pull/31955/files
    

Where:

    /afs/cern.ch/user/a/amassiro/work/RC
    

Procedure:

    scramv1 list

get the latest release

    cmsrel CMSSW_11_2_0_pre10
    
    cd CMSSW_11_2_0_pre10/src/
    
    cmsenv
    
    git-cms-addpkg  Configuration/PyReleaseValidation/
    
 
modify file:

    Configuration/PyReleaseValidation/python/relval_standard.py
    
    ### LS2 - MWGR ###
    workflows[138.1] = ['',['RunCosmics2020GEM','RECOCOSDRUN3','ALCACOSDRUN3','HARVESTDCRUN3']]
    workflows[138.2] = ['',['RunCosmics2020','RECOCOSDEXPRUN3','ALCACOSDEXPRUN3','HARVESTDCEXPRUN3']]

    -->
    workflows[138.1] = ['',['RunCosmics2020','RECOCOSDRUN3','ALCACOSDRUN3','HARVESTDCRUN3']]

    
    Configuration/PyReleaseValidation/python/relval_steps.py
    
    steps['RunCosmics2020']
    
    New: 338714
    
    - [1] Run 338628   (CSC, DAQ, DCS, DQM, DT, ECAL, HCAL, RPC, TCDS, TRACKER, TRG)
    - [2] Run 338714   (CSC, DAQ, DCS, DQM, DT, ECAL, GEM, HCAL, RPC, TCDS, TRACKER, TRG)

    
    -->
    
    steps['RunCosmics2020']={'INPUT':InputInfo(dataSet='/ExpressCosmics/Commissioning2020-Express-v1/FEVT',label='2020GR5',run=[338714],events=100000,location='STD')}

    steps['RunCosmics2020']={'INPUT':InputInfo(dataSet='/ExpressCosmics/Commissioning2020-Express-v1/FEVT',label='2020GR5',ls={338714: [[1, 10000]]},events=100000,location='STD')}

    
Test:

    runTheMatrix.py -l 138.1 --command "-n 500"    -----> RECO
    runTheMatrix.py -l 138.2 --command "-n 500"    -----> Express


    dasgoclient --limit 0 --query 'file dataset=/ExpressCosmics/Commissioning2019-Express-v1/FEVT run=334393 site=T2_CH_CERN'
    dasgoclient --limit 0 --query 'file dataset=/ExpressCosmics/Commissioning2020-Express-v1/FEVT run=338714 site=T2_CH_CERN'
    
    (dasgoclient --limit 0 --query 'lumi,file dataset=/ExpressCosmics/Commissioning2020-Express-v1/FEVT run=338714' --format json | das-selected-lumis.py 1,10000 ) | sort -u > step1_dasquery.log  2>&1

     
    1 1 1 1 tests passed, 0 0 0 0 failed
    good
    
    
Create PR:

    git remote add origin git@github.com:amassiro/cmssw

    git fetch origin

    git checkout -b  addingMWGR5-from-2020-with-all-detectors-included
    
    
    git commit ...
    
    
    git push -u origin addingMWGR5-from-2020-with-all-detectors-included
    
Then on the web for the PR

    https://github.com/cms-sw/cmssw/compare/master...amassiro:addingMWGR5-from-2020-with-all-detectors-included?expand=1    
    
    https://github.com/cms-sw/cmssw/pull/32780
    
    
    
    
    
    
