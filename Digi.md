Digi stands for **Digit** and it represents something similar to a [[Hit]], however, instead of giving exact values, they will output currents and voltages in order to simulate the output of a real detector more closely. This class is a child class of the [`G4VDigi`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/digits_hits/digits/include/G4VDigi.hh) base class. 

Just like hits, you can define an array of digits into a digi collection that can be used for further processing. In order to utilise digits, the user must define a [[DigitizerModule]] concrete class. 

The basic header file for a digit is very similar to the [[Hit]] as it is just a container for data. Therefore, it will contain a number of `getxxx()` and `setxxx()` methods. This example will continue from the example its [[Hit]] and will record the position of the particle.
```cpp
class ExampleDigi: public G4VDigi {
public:
	ExampleDigi();
	~ExampleDigi();
	
	inline void SetPosition(G4ThreeVector pos) {fpos = pos;};
	inline G4ThreeVector GetPosition() {return fpos;};

private:
	G4ThreeVector fpos;

};

typedef G4TDigiCollection<ExampleDigi> ExampleDigitsCollection;
}
```
In reality, the position would be represented by some copy numbers given to the [[SensitiveDetector]] that was hit by the particle, therefore, digitizing the output e.g. if you had a grid of sensitive detectors, if a particle hits the detector at (1,2), the hit would record these copy numbers, which is what the digit would extract. 
