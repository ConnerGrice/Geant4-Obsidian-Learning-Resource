In this method the values of the field at points within the simulation world are defined. This can either be done in the method itself or values can be pulled from external files.

There are 2 inputs taken by this method:
1. `points[4]` - This is an array with 4 values that represent coordinates in the simulation world.
	- `Point[0]` = x coordinate
	- `Point[1]` = y coordinate
	- `Point[2]` = z coordinate
	- `Point[3]` = time value
2. `Bfield` - This represents the vector of the field at each point in space.
	- `Bfield[0]` = x component
	- `Bfield[1]` = y component
	- `Bfield[2]` = z component

Below is an example of how a user would create their own `GetFieldValue()` method:
```cpp
void ExampleField::GetFieldValue(const G4double Point[4], G4double* Bfield) const{

	//Seperate coordinate values
	G4double x = Point[0];
	G4double y = Point[1];
	G4double z = Point[2];
	G4double t = Point[3];

	//Calcaulte components
	//NOTE: These methods are not defined anywhere and are for illustration purposes
	Bfield[0] = CalculateXComp(x,y,z,t);
	Bfield[1] = CalculateYComp(x,y,z,t);
	Bfield[2] = CalculateZComp(x,y,z,t);
}
```