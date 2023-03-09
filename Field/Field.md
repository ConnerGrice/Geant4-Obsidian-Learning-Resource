These are classes the define different types of fields that can be present in the simulation world. The base class for all fields is the [`G4Field`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/magneticfield/include/G4Field.hh). However, there are some child classes already created that can be used to define other fields:
1. [`G4ElectricField`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/magneticfield/include/G4ElectricField.hh)
2. [`G4MagneticField`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/magneticfield/include/G4MagneticField.hh)
3. [`G4ElectromagneticField`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/magneticfield/include/G4ElectroMagneticField.hh)

## Non-uniform Fields
The main method used by the `G4Field` class as well as all the other premade classes is [[GetFieldValue()]].

Another method in this base class is `DoesFieldChangeEnergy()`. If the user is using one of the 3 already concrete classes, this method is not needed since this method just returns a bool depending on the type of field. For instance: `G4ElectricField` will return `true`, while `G4MagneticField` will return `false`.

An example for a custom magnetic field header file is below:
```cpp
class ExampleField: public G4MagneticField{
public:
	ExampleField();
	~ExampleField();

public:
	//point -> Global coordinate system, x,y,z,t
	//Bfield -> Output field vector
	void GetFieldValue(const G4double Point[4], G4double* Bfield);
};
```

## Uniform Fields
If the user wants to define a uniform field, there are pre-made concrete classes that can already handle this:
- `G4UniformMagField(const G4ThreeVector& FieldVector)`
- `G4UniformGravField(const G4ThreeVector& FieldVector)`
- `G4UniformElectricField(const G4ThreeVector& FieldVector)`
These are used by invoking them into the [[ConstructSDandField()]] method.
