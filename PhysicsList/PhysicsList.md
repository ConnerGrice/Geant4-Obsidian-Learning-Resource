This class is responsible for telling Geant4 what particles will be allowed to generate, as well as the physical forces that can influence particles within the simulation.

This must be a child class of the [`G4VUserPhysicsList`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/run/include/G4VUserPhysicsList.hh) base class. It must contain 2 different abstract methods from this base class:

1. [[ConstructParticle()]] - Used to define the particles
2. [[ConstructProcess()]] - Used to define the physical forces
3. [[SetCuts()]] - Used to set ranges for secondary particle production

A basic header file for the physics list is below:
```cpp
class ExamplePhysicsList: public G4VUserPhysicsList{
public:
	ExamplePhysicsList();
	~ExamplePhysicsList();
protected:
	void ConstructParticle();
	void ConstructProcess();
	void SetCuts();
};
```