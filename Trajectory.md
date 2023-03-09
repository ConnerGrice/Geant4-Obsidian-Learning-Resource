A trajectory is a collection of points particles take during an event.

The structure of a trajectory is that it contains a vector of [`G4VTrajectoryPoint`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4VTrajectoryPoint.hh) objects which are be seen as very similar to [[Step]]s, which represents the particles at each point along the trajectory.  Geant4 also provide a default concrete class that already contains common information that is used, the [`G4TrajectoryPoint`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4TrajectoryPoint.hh). 

The trajectory base class is the [`G4VTrajectory`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4VTrajectory.hh), however, Geant4 also have a default trajectory class containing common information, [`G4Trajectory`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4Trajectory.hh). 

The user can create their own trajectory class if they want additional information or change the drawing style in the visualiser.

```ad-warning
If a custom trajectory class is used, **DO NOT** use `G4Trajectory`, or `G4TrajectoryPoint` as the base classes.
```
