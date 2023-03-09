A run is the largest time scale in the Geant4 system, with an [[Event]] being the layer below. The object that represents a run is the [`G4Run`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/run/include/G4Run.hh) class. 

The run can be seen as a collection of events. A run begins at the same time as the first event (When the first primary particles are generated). Once a run has started, the detector geometry and physical processes are locked and unchangeable.

Some common data that is stored by the run object is:
- The list of [[Event]] objects - `GetEventVector()`
- Names of all [[Hit]] collections - `GetHCtable()`
- Names of all [[Digi]] collections - `GetDCtable()`

