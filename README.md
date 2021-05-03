# forceporousZones
To output the porous forces saperately for a given porous cellZone ID. 
Compatible with OF version : 8.0
Instructions to install :  
download the files to the use directory of openFoam. 
run in terminal wmake with openfoam variables in the source.

add the following function part to the system/controlDict

functions
{
   forcesA
   {	
	 type 		forcePorousZones;
	 libs		("libforcePorousZones.so");
	 porosity 	true;
	 cellZones	(0 1);  // newly added term which needs the cellZoneID's not names (normally start from 0 to number of cellzones in the case) 
	 patches 	(); //(".*all.*");
	 rho 		rhoInf;
	 rhoInf 	1000;
	 CofR 		(0 0 0);
	 writeControl   timeStep;
	 writeInterval  1;
	 log 		true;
   }
}

The above function object will give the combined porous forces of cellZoneID's 0 and 1. 
If you need them saperately, just create another function object for example forcesB with only the ID of the cellZone which is requiered.

TODO: give the cellZOne names insted of ID's. 
porosity class doesnt have member function returning cellZoneID for a given cellZOne name.
