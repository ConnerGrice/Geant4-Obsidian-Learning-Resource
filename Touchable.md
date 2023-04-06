A touchable is the a class the stores the information about a volume. It is represented by [G4VTouchable](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/management/include/G4VTouchable.hh). This class allows the user to get the volumes [[SolidVolume]] or [[PhysicalVolume]], as well as the information about the volumes position and rotation.

- `G4VPhysicalVolume vol = touchable->GetVolume();`
- `G4VSolid solid = touchable->GetSolid();`

The touchable can be fetched via a few different methods:

- Via a [G4StepPoint](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/track/include/G4StepPoint.hh), which can be fetched from a [[Step]].
	- `touchable = aStep->GetPreStepPoint()->GetTouchable();`
- Via a [[Track]], which can also be fetched using a [[Step]].
	- `touchable = aStep->GetTrack()->GetTouchable();`

An extension to the touchable is the [G4TouchableHistory](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/volumes/include/G4TouchableHistory.hh). This represents an array of mother and grandmother volumes that are linked to the touchable in question.