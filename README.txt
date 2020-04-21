This is loosely based on the prism_riblet_v1 system, but with an added 3D component.  We'll keep the general system
geometry the same as the prism_riblet_v1 one, but with extra patch definitions for the front and back faces.

There will also need to be some swapping around of boundary condition assignments as the inlet/outlets are now the front/back.

///////////////////////////////////////////////////////////////

Currently varying the biofilm thickness and the riblet separation. Current riblet separations are 23, 46 and 92 microns.

Biofilm thicknesses are:

thick = 60 microns
thin = 21 microns
level = 42 microns
//////////////////////////////////////////////
Gravity was still turned on, I've turned it off now, see if it changes anything.
