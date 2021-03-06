#### Current production tag : V07-04-09-02
#### Newest tag for testing : 
#### Note that the current head version need to be run with CMSSW_7_4_5

##### Caveat !
The current head version only works with CMSSW_7_4_9.

##### To work with CMSSW_7_4_9, you do:
cd CMSSW_7_4_9/src <br>
cmsenv <br>
git cms-merge-topic -u cms-met:METCorUnc74X <br>
git cms-merge-topic ikrav:egm_id_747_v2 <br>
git clone https://github.com/cms-jet/JetToolbox JMEAnalysis/JetToolbox <br>
git clone https://github.com/cmkuo/HiggsAnalysis.git <br>
git clone -b V07-04-09-02 https://github.com/cmkuo/ggAnalysis.git <br>
scram b -j 10 <br>

##### CRAB3 and V07-04-09-02
When you run jobs with CRAB3 and V07-04-09-02 <br>
you need to add the following line to your crab py file <br>
Data : config.JobType.inputFiles = ['Summer15_50nsV4_DATA.db'] <br>
MC : config.JobType.inputFiles = ['Summer15_50nsV4_MC.db'] <br>

##### To work with CMSSW_7_4_5, you do:
cd CMSSW_7_4_5/src <br>
cmsenv <br>
git cms-merge-topic ikrav:egm_id_74X_v2 <br>
git clone https://github.com/cmkuo/HiggsAnalysis.git <br>
git clone -b V07-04-05-05 https://github.com/cmkuo/ggAnalysis.git <br>
git clone https://github.com/cms-jet/JetToolbox JMEAnalysis/JetToolbox <br>
scram b -j 10 <br>

The above code stores the decision in 64 integer. Each bit represents a decision<br>
for ELECRON ID: 5 IDs (Veto, Loose, Medium, Tight and HEEP) so only 5 bits are imp for us (59 bits of this integer  we are not using so may be we can change that to 16 bit integer later)<br>
Representing that integer in 5 bits: b4 b3 b2 b1 b0<br>
b0: Veto; b1: Loose; b2: Medium; b3: Tight and b4: HEEP<br>
To access the decision for <br>
(a) veto: eleIDbit[]>>0&1 ---> gives 0 or 1. if 0--> this eID is failed. if 1--> this eID is passed<br>
(b) Loose: eleIDbit[]>>1&1<br>
(c) Medium: eleIDbit[]>>2&1<br>
(d) Tight: eleIDbit[]>>3&1<br>
(e) HEEP: eleIDbit[]>>4&1<br>

for photons it is done the same way: it has 3 IDs<br>
so 3 bits represent the decision<br>
Representing that integer in 3 bits:  b2 b1 b0<br>
b0: Loose; b1: Medium; b2: Tight<br>
To access the decision for <br>
(a) Loose: phoIDbit[]>>0&1 ---> gives 0 or 1. if 0--> this phoID is failed. if 1--> this phoID is passed<br>
(b) Medium: phoIDbit[]>>1&1<br>
(c) Tight: phoIDbit[]>>2&1<br>

to access the MC status flag with GEN particles <br>
(a) fromHardProcessFinalState : mcStatusFlag[]>>0&1 ---> gives 0 (no) or 1 (yes). <br>
(b) isPromptFinalState        : mcStatusFlag[]>>1&1 ---> gives 0 (no) or 1 (yes). <br>
(c) fromHardProcessBeforeFSR  : mcStatusFlag[]>>2&1 ---> gives 0 (no) or 1 (yes). <br>

##### To work with CMSSW_7_2_0 or 7_2_3, you do:

git cms-merge-topic ikrav:egm_id_phys14 # for photon ID recipe <br>
git cms-merge-topic HuguesBrun:trigElecIdInCommonIsoSelection720 # for electron ID recipe <br>
git clone https://github.com/cmkuo/HiggsAnalysis.git <br>
git clone -b V07-02-03-00 https://github.com/cmkuo/ggAnalysis.git <br>


