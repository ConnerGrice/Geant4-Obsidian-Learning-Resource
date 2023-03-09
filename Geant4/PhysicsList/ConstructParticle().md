This method is responsible for telling Geant4 what type of particles are allowed to be inside the simulation, this include particles that will be generated at the start of the run and particles that will be generated during the run. 

The types of particles that can be produced are:
1. Baryons
2. Mesons
3. Bosons
4. Short Lived (Transport bosons)
5. Ions

## Using Constructor
The basic method of allowing a certain particle is to, first define the particles constructor, then using the constructer to create the generate the particle. This example will construct mesons:
```cpp
//Defines constructor
G4MesonConstructor mConstructor;
//Creates particles
mConstructor.ConstructParticle();
```

## Using Definition
These constructors simplify the process by defining multiple types of particles at the same time. If the user wants to have complete control over the particles they want to generate they can use this other method. This will show how only electrons are defined:
```cpp
G4Electron::ElectronDefinition();
```

Below is an example of this method that allows all types of particles to be generated:
```cpp
void ExamplePhysicsList::ConstructParticle(){

G4BaryonConstructor bConstructor;
bConstructor.ConstructParticle(); 

G4LeptonConstructor lConstructor;
lConstructor.ConstructParticle();

G4MesonConstructor mConstructor;
mConstructor.ConstructParticle();

G4BosonConstructor bsConstructor;
bsConstructor.ConstructParticle();

G4ShortLivedConstructor slConstructor;
slConstructor.ConstructParticle();

G4IonConstructor iConstructor;
iConstructor.ConstructParticle();

}
```

