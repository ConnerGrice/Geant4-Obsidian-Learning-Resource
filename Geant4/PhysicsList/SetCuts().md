This method is used to set the range at which secondary particle production cannot occur is the particle has travelled below this range within a material. 

These ranges only need to be set for:
- Electrons
- Positrons
- Gamma photons
- Protons

An example of setting a constant cut value for all of these particle types is below:
```cpp
void ExamplePhysicsList::SetCuts(){
	defaultCutValue = 0.7*mm;
	SetCutValue(defaultCutValue,"e-");
	SetCutValue(defaultCutValue,"e+");
	SetCutValue(defaultCutValue,"gamma");
	SetCutValue(defaultCutValue,"proton");
}
```
This code means that secondary particle production cannot occur if the particles are less then 0.7mm into a material.