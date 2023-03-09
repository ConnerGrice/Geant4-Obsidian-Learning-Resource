A step is the smallest piece of information provided by Geant4. It is the data about a particle for each timestep. A step object is given by [`G4Step`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/track/include/G4Step.hh).

A step will contain a collection of information about particles for each timestep:
- Step point info at the start of the timestep - `GetPreStepPoint()`
- Step point info at the end of the timestep - `GetPostStepPoint()`
	- These methods will output an [`G4StepPoint`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/track/include/G4StepPoint.hh) object. These step points allows the user to extract more information, such as the volume the particle is inside of.
-  "delta" information (difference between each step point)
	- delta position - `GetDeltaPosition()`
	- delta momentum - `GetDeltaMomentum()`
	- delta energy - `GetTotalEnergyDeposit()`

To make use at the steps within a simulation, the user must define a [[SteppingAction]] class to specify what exactly will happen at each step.