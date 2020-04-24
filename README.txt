This is loosely based on the prism_riblet_v1 system, but with an added 3D component.  We'll keep the general system
geometry the same as the prism_riblet_v1 one, but with extra patch definitions for the front and back faces.

ALSO NEED TO CHANGE THE DYNAMIC MESHING STUFF AS THE ONE IN prism_riblet_v1 IS FOR 2D!!!!!!!!!!!!!!!!

There will also need to be some swapping around of boundary condition assignments as the inlet/outlets are now the front/back.

It turns out that boundary conditions need to be defined for any named patches before the system can be visualised in paraview.

Boundary condition modifications are:
alpha.biofilm.orig - added in frontWall and backWall with the same inletOutlet conditions as the non-riblet boundaries
p - all boundaries are now zeroGradient except backWall which is uniform 0, as it's now the outlet
U - changed leftWall and rightWall to slip, frontWall has type zeroGradient, backWall is now inletOutlet, upperWall now has U_z instead of U_x.

Also added in some modifications in the parameters file and in the setfieldsdict file.  Care will need to be taken when changing the width of the system etc.

Here is a rudimentary way to visualise in 3D:
use the threshold filter on alpha.biofilm and set the limits to 0.5 and 1.5, this will only plot biofilm
then add another threshold filter to the main case file, but don't change the limit and instead reduce the opacity.
this will show the biofilm in the internal system with a translucent box around it.
we can figure out a more aesthetic way for this later on.

For the dynamic meshing, we used the dynamicmeshdict from the dambreak with obstacle case. the dynamicMeshDict for the 2D case is still saved in the constant folder
for now.
///////////////////////////////////////////////////////////////

Currently varying the biofilm thickness and the riblet separation. Current riblet separations are 23, 46 and 92 microns.

Biofilm thicknesses are:

thick = 60 microns
thin = 21 microns
level = 42 microns
//////////////////////////////////////////////

Due to the large clocktimes and high number of cores required to run these 3D simulations, it seems that the best course of action is to submit these jobs
to the 24 hour queue and then manually continue them once the 24 hours has elapsed.  This appears reasonably straightforward to do.  The steps are as follows:

1. Change the startFrom keyword in system/controlDict as startTime -> latestTime.  This can be done via: sed -i 's/startTime/latestTime/g' system/controlDict
2. Just in case the job was stopped in the middle of filewriting, run this command to delete the latest time directories: foamListTimes -processor -latestTime -rm
3. Then run the solver as usual.  No need to reconstructPar anything.
