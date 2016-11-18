**The VM and its corresponding documentation are still under construction. Please come back to this page later.**

# CorrectByConstructionTC-JVLC16
This repository documents the resources of the SHARE VM that belongs to the paper "A Systematic Approach to Constructing Incremental Topology Control Algorithms Using Graph Transformation"
* Authors: Roland Kluge, Michael Stein, Gergely Varró, Andy Schürr, Matthias Hollick, Max Mühlhäuser
* DOI: http://dx.doi.org/10.1016/j.jvlc.2016.10.003 / URL: http://www.sciencedirect.com/science/article/pii/S1045926X15300483

# FAQs or What can I do with the VM?

## Where should I start?

1. Navigate to the Desktop
2. Open the folder *cbcTC*
3. Open Eclipse by double-clicking *eclipse.exe*
4. All material is contained in the workspace that opens up.

## Where is the metamodel? Where are the Topology Control rules?

1. In Eclipse, open the project *de.tudarmstadt.maki.tc.cbctc.specification*
2. Double-click the EAP file *de.tudarmstadt.maki.cbctc.specification.eap*
3. Enterprise Architect Lite opens up.
3. The metamodel can be found in the package *de.tudarmstadt.maki.tc.cbctc.model*. 
The Topology Control rules of kTC (and a number of other TC algorithms) can be found in the package *de.tudarmstadt.maki.tc.cbctc.algorithms*.

## How can I run a sample simulation?

1. In eclipse, open the project *simonstrator-simrunner*
2. Navigate to *config/rkluge/launch/"
3. Right-click *GUIRunner-with-EMF.launch* and select *Run as -> GUIRunner-with-EMF*
4. Type the following file name into the search bar: *jvlc_complete_evaluation.xml*
5. Press *Start Simulation*
6. Two windows should pop up
 * The *Topology Visualization* window shows the current output WiFi topology 
 * The *Simulation* window shows statistics about the progress of the simulation, simulation speed, etc.
7. Additionally, the log output in the *Console* view of Eclipse provides information about the progress of topology control.

## What do the log messages tell me?
The *Console* view of Eclipse reports on Topology-Control-specific metrics.
An example:
```
18-Nov-2016 10:09:11. INFO 	iter#001 CEs...
18-Nov-2016 10:09:11. INFO 	Adding node Node [id=1, properties={SiS-PHY_LOCATION=PositionVector [571.6007134974011, 360.78730807559845], SiS-LOCATION_X=571.6007134974011, SiS-LOCATION_Y=360.78730807559845}]
[...]
18-Nov-2016 10:09:12. INFO 	Adding node Node [id=100, properties={SiS-PHY_LOCATION=PositionVector [375.80031121334616, 375.88742237059733], SiS-LOCATION_X=375.80031121334616, SiS-LOCATION_Y=375.88742237059733}]
18-Nov-2016 10:09:12. INFO 	iter#001 CEs   Done (t=220ms, t_check=11ms, numCEs=[+n= 100, -n=   0, +e= 800, -e=   0, mod-d=   0, mod-w=   0, mod-p=   0])
18-Nov-2016 10:09:12. INFO 	iter#001 iTC...(algo=D_KTC(id=1), kTCParameterK=1.41)
18-Nov-2016 10:09:12. INFO 	iter#001 iTC   Done (t=138ms,  t_check=8ms,  violations=0, allLSMs=1401 [[total count: a= 469, i=622, u= 310, effective counts: a= 264, i=536, u=   0]], effLSMs=800)
18-Nov-2016 10:09:12. INFO 	iter#001 bTC...(algo=D_KTC(id=1), kTCParameterK=1.41)
18-Nov-2016 10:09:12. INFO 	iter#001 bTC   Done (t=13ms,  t_check=4ms, violations=0, allLSMs=800 [[total count: a= 264, i=536, u=   0, effective counts: a= 264, i=536, u=   0]], effLSMs=800)
18-Nov-2016 10:09:12. INFO 	iter#001 iTC vs. bTC (CE+TC) wrt. [time=27.54 / LSMs=1.00]
18-Nov-2016 10:09:12. INFO 	iter#001 Stat..
18-Nov-2016 10:09:12. INFO 	Total real duration: 0.01min
18-Nov-2016 10:09:12. INFO 	iter#001 Stat  Done (duration=32ms, n=100, m=800, avgBatPct=75.32, minBatPct=50.15, maxBatPct=98.88, numEmptyNodes=0, numSCCsInInput=2, numSCCsInOutput=2)
18-Nov-2016 10:09:12. INFO 	Simulated Realtime: 0:10:0:0 (H:m:s:ms)
```

**Explanation:**
* ```iter##001``` Denotes the first iteration of the Topology Control algorithm. In this setup, Topology Control is executed periodically every 10min of simulated time.
* ```iter#001 CEs... Adding node Node [...]``` Before running the algorithm, all pending context events are handled.
* ```iter#001 CEs   Done (t=220ms, t_check=11ms...```` At the end of context event handling, the required CPU time for the handling and for the constraint checking is printed.
* ```iter#001 iTC...(algo=D_KTC(id=1), kTCParameterK=1.41)``` Then, incremental the topology control algorithm is invoked (here: the traditional kTC with k=1.41). Afterwards, the required CPU time for the algorithm and the constraint checking are printed.
* ```iter#001 bTC...(algo=D_KTC(id=1), kTCParameterK=1.41)``` For comparison reasons, the batch counterpart of the current algorithm is executed on a copy of the topology and runtime statistics are printed.
* ```iter#001 iTC vs. bTC (CE+TC) wrt. [time=27.54 / LSMs=1.00]``` At the end of a Topology Control run, the costs of the incremental and batch algorithm are compared in terms of CPU time and link state modifications. In this case, the incremental algorithm needed 27.54 times longer compare to the batch algorithm. The link state modification count is identical in this iteration because the topology is processed for the first time.
