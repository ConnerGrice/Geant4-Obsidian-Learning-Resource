This is a special physical volume that optimises a users ability to create a repeated volume along a single axis similar to [[PVDivision]]. This could either be segments around a cylinder or sections of a rectangle. This physical volume is represented by the [G4PVReplica](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/volumes/include/G4PVReplica.hh) class.

There are some constraints when placing a replica:
1. The mother volume **MUST** be completely filled by the replicas. (This is where the replica differs from the division).
2. The replicas must be the same width and shape.
3. Replication can only occur along a single axis.
4. Replicas can be inside of other replicas.
5. [[Placement Volumes]] can be placed inside replicas if there is no overlap with the replica mother volume.
6. No volumes can be placed inside of a radial replica.
7. [[PVParameterised]] volumes cannot be placed in a replica.

The basic constructor for a replica:
```cpp
G4PVReplica(const G4String& pName,
	G4LogicalVolume* pLogical,
	G4LogicalVolume* pMother,
	const EAxis pAxis,
	const G4int nReplicas,
	const G4double width,
	const G4double offset = 0.);
```

- `pName` - The name of the replica volume.
- `pLogical` - The logical volume of a single replica.
- `pMother` - The logical volume of the shape that the replicas will take up.
- `pAxis` - The axis that the volumes will be replicated.
	- `kXaxis`,`kYaxis`,`kZaxis` - Cartesian - _slabs_
	- `kRaxis` - Radial axis - _rings_
	- `kPhi` - About centre axis - _segments_
- `nReplicas` - The number of replications
- `width` - The width of replications
- `offset` - The offset from the centre (only for circular shapes)

When defining a replica, the user must first define a logical mother volume, and the logical segment volume that will be used to fill that mother volume. Once this is done, the user defines the `G4PVReplica` object that takes the logical segment and the logical mother. The final replica is then placed by creating a physical mother volume.

An example using a `G4Box` and replicating down the Z axis:
```cpp
//Full mother dimensions
G4double motherWidth = ...
G4double motherHeight = ...
G4double motherLength = ...

//Number of replicas
G4int reps = ...

//Define the mother volume
G4Box* motherS = new G4Box("MotherS",hMotherWidth/2,hMotherHeight/2,hMotherLength/2);
G4LogicalVolume* motherL = new G4LogicalVolume(motherS,motherMat,"MotherL");

//The length of a replica since it is replicated down the Z axis
G4double replicaLength = motherLength/reps;

//Width and height are the same since all the replicas must completely fill the mother volume
G4Box* replicaS = new G4Box("ReplicaS",motherWidth/2,motherHeight/2,replicaLength/2);
G4LogicalVolume* replicaL = new G4LogicalVolume(replicaS,replicaMat,"ReplicaL");

//Physical replica must be linked to the mother logical volume
G4VPhysicalVolume* replicaP = new G4PVReplica("ReplicaP",replicaL,motherL,kZaxis,reps,replicaLength);

//The mother volume must then be placed in the world volume for it to appear in simulation
G4VPhysicalVolume* motherP = G4PVPlacement(0,0,motherL,"MotherP",worldL,false,0);

```





	
