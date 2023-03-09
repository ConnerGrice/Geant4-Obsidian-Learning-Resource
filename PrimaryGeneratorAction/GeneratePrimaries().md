This method is part of the [[PrimaryGeneratorAction]] class and will contain the information about how particles are generated at the start of each run. In order for this method to generate particles, it must use a concrete class that uses the [`G4VPrimaryGenerator`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4VPrimaryGenerator.hh) as a base class. Then the `GeneratePrimaryVertex()` method is used. An example of one of these classes is the [`G4ParticleGun`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4ParticleGun.hh). Which is used in the header file for the [[PrimaryGeneratorAction]].

In the example below, the simulation will generate a proton with a given momentum and a given direction of travel and will originate from slightly off centre of the world volume:
```cpp
void ExamplePrimaryGeneratorAction::GeneratePrimaries(G4Event* anEvent){
	//Sets the particle to be shot to be a proton
	particleGun->SetParticleDefinition(G4Proton::Definition());

	//Sets particle properties
	particleGun->SetParticlePosition(G4ThreeVector(0,1,0));
	particleGun->SetParticleEnergy(G4double 10*Mev);
	particleGun->SetParticleMomentumDirection(G4ThreeVector(1,1,1));

	//Shoots the particle at the start of an event
	particleGun->GeneratePraimryVertex(anEvent);
}
```