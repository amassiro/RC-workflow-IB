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

    
    
    Configuration/PyReleaseValidation/python/relval_steps.py
    
    steps['RunCosmics2020']
    
    338714
    
    - [1] Run 338628   (CSC, DAQ, DCS, DQM, DT, ECAL, HCAL, RPC, TCDS, TRACKER, TRG)
    - [2] Run 338714   (CSC, DAQ, DCS, DQM, DT, ECAL, GEM, HCAL, RPC, TCDS, TRACKER, TRG)

    
    