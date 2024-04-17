# Types of Grid Description Files


- **Exodus file**: ex. "ne4.g".   This is a netcdf file following Exodus conventions.  It gives the corner locations of all elements on the sphere and their connectivity.  It is independent of the polynomial order used inside the element ("np").  This file is used by TempestRemap (TR) to generate mapping files.  The polynomial order is a command line option and the GLL nodes are internally generated by TR.  

- **SCRIP file**:  ex. "ne4pg2.scrip.nc".   This file contains a description of the atmosphere physics grid in the format used by the original incremental remap tool SCRIP.  It is used for most output and also used to generate mapping files between components and for post-processing of most output.

Less common “GLL” metadata files needed for specialized purposes:

- **"dual grid" SCRIP file**:  ex. "ne4np4_scrip.nc".   This file contains a SCRIP format description of the GLL grid.  It includes the locations of the GLL nodes and artificial bounding polygons around those nodes.   Ideally the spherical area of each polygon will match the GLL weight ("exact GLL areas"), but not all tools can achieve exact areas.  Inexact areas does not impact the accuracy of the resulting mapping algorithm, it just means that mass will not be exactly conserved by the mapping algorithm. These files are often problematic to generate, so it is advised to avoid using workflows that require this. This was previously needed in E3SMv2 configurations by the cube_to_target topography dataset generation tool, but effort has been made to eliminate this requirement. It was also historically used in E3SMv1 to create ocean/atm mapping files (exact GLL areas was important here to conserve fluxes).

- **latlon file**: ex. "ne4np4_latlon.nc".   This file contains a list of all the GLL nodes in the mesh (in latitude/longitude coordinates).   The list of GLL nodes must be in the the internal HOMME global id ordering, matching the ordering used in EAM GLL grid output.   It also contains the connectivity of the GLL subcell grid. This file is no longer needed for any E3SM workflow.