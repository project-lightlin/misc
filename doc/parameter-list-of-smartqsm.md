# Supported architectural metrics

## Individual-scale: tree parameters
| No| Name | Unit | Computational method |
| - |------|------|----------------------|
| 1 |Location ($X$, $Y$, Altitude) | m | *Tree center* ($X$, $Y$) is taken from the starting point of the trunk path. Altitude is the lowest $z$ coordinate of the point cloud. |
| 2 |Number of branches | / | (including the trunk)  |
| 3 |Max branch order | / |  |
| 4 |Tree height | m | Height difference of the point cloud |
| 5 | DBH | cm | $\mathrm{DBH} \approx 2\left(r_u + \frac{(r_l-r_u)(h_u-1.3)}{h_u-h_l}\right)$, where $r_l$ ($r_u$) and $h_l$ ($h_u$) are the radius and aboveground height of the lower (upper) section of the trunk segment passing through $1.3 \, \mathrm{m}$ above ground |
| 6 | Girth | m | The radius obtained by fitting a cylinder to the point cloud within a breast height tolerance of $\pm 3 \, \mathrm{cm} $  (if failed, $\pm 20 \, \mathrm{cm}$ ), multiplied by $2\pi$ . ~~**Deprecated due to unstablility**:  The perimeter of horizontally projected 2D convex hull of point cloud extracted within $\pm 3\,\mathrm{cm}$ of breast height~~ |
| 7 | Ground diameter | cm | $\mathrm{GD} \approx 2\left(r_u + \frac{(r_l-r_u)(h_u-0.2)}{h_u-h_l}\right)$, where $r_l$ ($r_u$) and $h_l$ ($h_u$) are the radius and aboveground height of the lower (upper) section of the trunk segment passing through $0.2 \, \mathrm{m}$ above ground |
| 8 | Bole height | m | **Base height** of the first main branch |
| 9 | Diameter at bole height | cm | Twice the radius of the *bole top* (the highest node on the trunk path that is lower than the **bole height**) |
| 10| Bole length | m | Length of the trunk path until the *bole top* (*bole path*) |
| 11|Bole area | m² | Surface area of the mesh derived from the *bole path* |
| 12|Bole volume | L | Volume of the mesh derived from the *bole path* |
| 13|Trunk length | m | Length of the trunk path |
| 14|Trunk area | m² | Surface area of the mesh derived from the trunk path |
| 15|Trunk volume | L | Volume of the mesh derived from the trunk path |
| 16|Stem length | m | Sum of the path lengths of the trunk and all branches |
| 17|Stem area | m² | Surface area of the mesh derived from the paths of the trunk and all branches |
| 18|Stem volume | L | Volume of the mesh derived from the paths of the trunk and all branches |
| 19|Within-crown stem length | m | Sum of the path lengths of the stem starting from the *bole top* (*within-crown stem*) |
| 20|Within-crown stem area | m² | Surface area of the mesh derived from the *within-crown stem* |
| 21|Within-crown stem volume | L | Volume of the mesh derived from the *within-crown stem* |
| 22|Min crown radius | m | Minimum value of 36 *crown radii*. After horizontal projection of *crown points* above the **bole height** , they are divided into sub intervals every 10 degrees clockwise from the center of their bounding box (*crown center*) towards the north. The farthest projected *crown point* to the center (*ray*) within a subinterval is called the *crown radius*. |
| 23|Azimuth of min crown radius | ° | Azimuth of the *ray* that yields the **Min crown radius** |
| 24|Height at min crown radius | m | Relative height of the *crown point* that yields the **Min crown radius** |
| 25|Mean crown radius | m | Average value of 36 *crown radii* |
| 26|Max crown radius | m | Maximum value of 36 *crown radii* |
| 27|Azimuth of max crown radius | ° | Azimuth of the *ray* that yields the **Max crown radius** |
| 28|Height at max crown radius | m | Relative height of the *crown point* that yields the **Max crown radius** |
| 29|Min crown width | m | Minimum value of 180 *crown widths*. *Crown width* is the maximum difference between the projected *crown points* on a *straight line* passing through the *crown center* |
| 30|Azimuth of min crown width | ° | Azimuth of the *straight line* that yields the **Min crown width** |
| 31|Mean crown width | m | Average value of 180 *crown widths* |
| 32|Max crown width | m | Maximum value of 180 *crown widths* |
| 33|Azimuth of max crown width | ° | Azimuth of the *straight line* that yields the **Max crown width** |
| 34|East-west crown width | m | *Crown width* at azimuth of 90° |
| 35|North-south crown width | m | *Crown width* at azimuth of 0° |
| 36|Crown convex area | m² | Surface area of the crown convex hull |
| 37|Crown convex volume | L | Volume of the crown convex hull |
| 38|Active crown convex area | m² | Surface area of the convex hull of the *active crown*. *Active crown* refers to the mesh derived from the *within-crown stem* |
| 39|Active crown convex volume | L | Volume of the convex hull of the *active crown* |
| 40|Crown projection convex area | m² | Surface area of the crown projection convex hull |
| 41|Crown perimeter | m | Perimeter of the crown projection convex hull |
| 42|Canopy area | m² | Horizontally projected area of the *within-crown stem* |
| 43|Crown center offset | m | Horizontal distance between the *tree center* and the *crown center* |
| 44|Crown center azimuth | ° | Azimuth of the *crown center* relative to the *tree center* |
| 45|Min crown spread | m | Shortest distance from the *tree center* to the boundary of the crown projection convex hull |
| 46|Azimuth of min crown spread | ° | Azimuth of the line that yields the **Min crown spread** |
| 47|Max crown spread | m | Longest distance from the *tree center* to the boundary of the crown projection convex hull |
| 48|Azimuth of max crown spread | ° | Azimuth of the line that yields the **Max crown spread** |

## Organ-scale: branch attributes
※ The non-trunk branch path, starting from the first node outside its parent branch (*base center*) , is called the *active path*.

:star: Parameter contained in the trunk

| No| Name | Unit | Computational method |
| - |------|------|----------------------|
| 1|Order | / | Starting from order 0 (the trunk), recursively, when a branch junction is encountered, the branch segment originating from the thickest child node remains part of the original branch, and all other child nodes forms the start of new branches with order +1. |
| 2|Base height | m | $\mathrm{BH} \approx h_0 - \frac{\mathrm{BD}}{2}\sqrt{1-(\mathbf{v}\cdot \mathbf{n}_z)^2}$, where $\mathrm{BD}$ is the **base diameter**; $h_0$ is the aboveground height of the *base center*; $\mathbf{v}$ is the unit vector of the first *active path* segment; $\mathbf{n}_z$ is the unit vector of the $z$-axis |
| 3|Base diameter | cm | Twice the radius at the *base center* |
| 4|:star: Mid-length diameter | cm | $d_{\frac{1}{2}} \approx 2\left(r_f + \frac{(r_n-r_f)(L_f-0.5L)}{L_f-L_n}\right)$, where $r_n$ ($r_f$) and $L_n$ ($L_f$) are the radius and cumulative path length from the *base center* to the nearer (farther) end of the path segment passing through the midpoint of *active path* |
| 5|:star: Tip diameter | cm | Twice the radius at the endpoint of the *active path* |
| 6|Length | m | Length of the *active path* |
| 7|Area | m² | Surface area of the mesh derived from the *active path* |
| 8|Volume | L | Volume of the mesh derived from the *branch path* |
| 9|:star: Max spread | m | Maximum horizontal distance from the *base center* to the *active path* |
| 10|:star: Azimuth | ° | Clockwise angle between the horizontal projection of the *chord* direction and the north |
| 11|:star: Zenith | ° | Included angle between the *chord* direction and the positive $z$-axis |
| 12|:star: Chord length | m | Length of segment from the starting point to the end point of the active path (*chord*) |
| 13|:star: Arc height | m | Maximum distance from the active path to the *chord* |
| 14|:star: Height difference | m | Height difference of the mesh derived from the *branch path*. In the BH expression, the subtracted term is the vertical profile radius. Similarly here, the height difference can be replaced as the maximum difference between each node’s $z$-coordinate $\pm$ its respective vertical profile radius. |
| 15|Branching radius | m | Maximum perpendicular distance from the active path to the parent branch's local growth trend line |
| 16|Branching angle | ° | Included angle between the branch and its parent branch's local growth direction |
| 17|Tip deflection angle | ° | Included angle between the parent branch's local growth direction and the chord ray |
| 18|Vertical deflection angle | ° | Zenith of the branch's local growth direction relative to the positive $z$-axis |
| 19|:star: Tip-based DINC | m | **Tree height** minus the aboveground height of the upper edge of the endpoint of the **active path**. DINC is depth into crown |
| 20|:star: Apex-based DINC | m | **Tree height** minus the maximum aboveground height of the edge on the whole active path |
| 21|Growth length | m | Sum of the lengths of this branch and all derived branches |
| 22|Growth area | m² | Sum of the surface areas of this branch and all derived branches |
| 23|Growth volume | L | Sum of the volumes of this branch and all derived branches |
| 24|Base offset | m | Horizontal distance from the *tree center* to the *base center* |
| 25|Base azimuth | ° | Azimuth from the *tree center* to the *base center*|
| 26|Insertion distance | m | Cumulative length from the starting point of the trunk path to the *base center*. Only take the length of the active path of the branches that pass through |

## Plot-scale: stand's spatial structure indices
※ The number of neighbors $n$ below is set to 4.

| No| Name | Unit | Computational method |
| - |------|------|----------------------|
| 1|Uniform angle index | / | $W_i = \frac{1}{n}\sum_{j=1}^{n} z_{ij}$, where $z_{ij}$ is equal to $1$ if $\alpha_j < \alpha_0$, and $0$ otherwise; $\alpha_1,\cdots,\alpha_n$ are the angles formed by the rays from the central tree to $n$ neighboring trees that divide the circumference; standard angle $\alpha_0$ takes $72^\circ$ |
| 2|Hegyi's competition index | / | $\mathrm{CI}_i = \sum_{j=1}^{n}\frac{\mathrm{DBH}_j}{\mathrm{DBH}_i L_{ij}}$, where $\mathrm{DBH}_i$ and $\mathrm{DBH}_j$ are the DBH of the $i$th central tree and its $j$th neighboring tree; $L_{ij}$ is the horizontal distance between their tree centers |
| 3|Mingling | / | $M_i = \frac{1}{n}\sum_{j=1}^{n} v_{ij}$, where $v_{ij}$ is equal to $1$ if the $i$th central tree and its $j$th neighboring tree are the same species, and $0$ otherwise |
| 4|Tree species diversity mingling | / | $M_i = \sqrt{\frac{n_i}{n^2}\sum_{j=1}^{n} v_{ij}}$, where $n_i$ is the number of tree species in $n$ neighboring trees; $v_{ij}$ is the same as in Mingling |
| 5|Diameter dominance | / | $D_i = \frac{1}{n}\sum_{j=1}^{n} k_{ij}$, where $k_{ij}$ is equal to $1$ if $\mathrm{DBH}_i < \mathrm{DBH}_j$, and $0$ otherwise; $\mathrm{DBH}_i$ and $\mathrm{DBH}_j$ are the same as in Hegyi's competition index |
| 6|Crowdedness | / | $C_i = \frac{1}{n}\sum_{j=1}^{n} y_{ij}$, where $y_{ij}$ is equal to $1$ if $0.5(\mathrm{CW}_i+\mathrm{CW}_j) > L_{ij}$, and $0$ otherwise; $\mathrm{CW}_i$ and $\mathrm{CW}_j$ are the (mean) crown width of the $i$-th central tree and its $j$-th neighboring tree; $L_{ij}$ is the same as in Hegyi's competition index |
| 7|Openness | / | $O_i = \frac{1}{n}\sum_{j=1}^{n}\frac{L_{ij}}{H_j}$, where $H_j$ is the tree height of the $j$th neighboring tree of the $i$th central tree; $L_{ij}$ is the same as in Hegyi's competition index |
| 8|Within-unit species richness | / | The total number of tree species within a structural unit |