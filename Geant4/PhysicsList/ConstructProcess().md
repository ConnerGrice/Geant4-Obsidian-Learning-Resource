This method is used to define the interactions that can occur between particles during the simulation. This include electromagnetic forces, nuclear forces, decay reactions, or collision reactions. 

There are multiple different ways to define these forces. First, the user must define `AddTransportation()`, this allows for the particles to move at all. The user can specify each of the types of interactions that they wish to consider. This is done using the [`G4PhysicsListHelper`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/run/include/G4PhysicsListHelper.hh) and different processes using [processes](https://gitlab.cern.ch/geant4/geant4/-/tree/master/source/processes) defined by Geant4. One of the simple ways to specify multiple different types of interactions is to use the [physics constructors](https://gitlab.cern.ch/geant4/geant4/-/tree/master/source/physics_lists/constructors).

## Using G4PhysicsListHelper
This is an example of using the `G4PhysicsListHelper` to define gamma conversion as well as decay reactions:
```cpp
void ExamplePhysicsList::ConstructProcess(){
	//Define the list helper
	G4PhyicsListHelper* ph = G4PhysicsListHelper::GetPhysicsListHelper();

	//Get object that will loop through all particles
	auto particleIterator = GetParticleIterator();
	particleIterator->reset();

	//Define the decay reaction process
	G4Decay* decayProcess = new G4Decay();

	//Loop through all particles
	while ((*particleIterator)()){
		
		G4ParticleDefinition* particle = particleIterator->value();
		
		//Check if gamma conversion is applicable
		if (particle == G4Gamma::Gamma()){
			//Apply interactor to given particle
			ph->RegisterProcess(new G4GammaConversion(),particle);
		}
		//Checks if decay process is allowed to occur on given particle
		if (decayProcess->IsApplicable(*particle)){
			ph->RegisterProcess(decayProcess,particle);
		}		
	}
}
```

## Using Pre-packaged Physics Lists
The physics constructors are pre-packaged lists of interaction types. This is an example that allows for standard electromagnetic forces to be taken into account:
```cpp
void ExamplePhysicsList::ConstructProcess(){
	//Allows particles to move
	AddTransportation();

	//Allows em interactions to take place
	G4VPhysicsConstructor* emPhys = new G4EmStandardPhysics();
	emPhys->ConstructProcess();
}
```