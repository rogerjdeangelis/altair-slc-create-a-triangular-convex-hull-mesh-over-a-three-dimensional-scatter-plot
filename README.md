# altair-slc-create-a-triangular-convex-hull-mesh-over-a-three-dimensional-scatter-plot
Encase a scatter plot of a point sphere in a convex hull surface using a 92 face polyhedron composed of 92 triangles
    %let pgm=altair-slc-create-a-triangular-convex-hull-mesh-over-a-three-dimensional-scatter-plot;

    %stop_submission;

    Encase a scatter plot of a point sphere in a convex hull surface using a 92 face polyhedron composed of 92 triangles

    Too long to post, wee github
    https://github.com/rogerjdeangelis/altair-slc-create-a-triangular-convex-hull-mesh-over-a-three-dimensional-scatter-plot

    3d View of mesh and internal points
    https://github.com/rogerjdeangelis/altair-slc-create-a-triangular-convex-hull-mesh-over-a-three-dimensional-scatter-plot/blob/main/convex_hull_3d.png

    Depiction of the 3d poylhedron surcase triangles encasing the point sphere

    /***************************************************************************/
    /*  WORKX.THREE_TRIANGLES total obs=9                                      */
    /*                                                                         */
    /*   IDX     TRIANGLEID    VERTEXID     X      Y      Z     CZ             */
    /*                                                                         */
    /*  741          8            1       0.0    0.4    0.8    8               */
    /*  813          8            2       0.0    0.8    0.4    4               */
    /*  94           8            3       0.2    0.6    0.6    6               */
    /*                                                                         */
    /*  120          9            1       0.6    0.2    0.6    6               */
    /*  742          9            2       0.0    0.4    0.8    8               */
    /*  941          9            3       0.2    0.6    0.6    6               */
    /*                                                                         */
    /*  1201        10            1       0.6    0.2    0.6    6               */
    /*  743         10            2       0.0    0.4    0.8    8               */
    /*  104         10            3       0.4    0.0    0.8    8               */
    /*                                                                         */
    /*  +-----------------------------------------------------------------+    */
    /*  |  Triangles Pojected on xy Plane (recreation not to sale)        |    */
    /*  |                          ACTUAL DATA                            |    */
    /*  |        * 8-2             TRIANGLE VERTEX    X      Y      Z     |    */
    /*  |        | \                                                      |    */
    /*  |        |  \                  8       1    0.0    0.4    0.8     |    */
    /*  |        |   \                 8       2    0.0    0.8    0.4     |    */
    /*  |        |    \                8       3    0.2    0.6    0.6     |    */
    /*  |        |     \                                                  |    */
    /*  |        |      \              9       1    0.6    0.2    0.6     |    */
    /*  |        |       \             9       2    0.0    0.4    0.8     |    */
    /*  |        |        \            9       3    0.2    0.6    0.6     |    */
    /*  |        |         \                                              |    */
    /*  |        |          \         10       1    0.6    0.2    0.6     |    */
    /*  |        |           \ 8-3    10       2    0.0    0.4    0.8     |    */
    /*  |        |Triangle 8 * 9-3    10       3    0.4    0.0    0.8     |    */
    /*  |        |           /\                                           |    */
    /*  |        |          /  \                                          |    */
    /*  |        |         /    \                                         |    */
    /*  |        |        /      \                                        |    */
    /*  |        |       /        \                                       |    */
    /*  |        |      /          \                                      |    */
    /*  |        |     /            \                                     |    */
    /*  |        |    /              \                                    |    */
    /*  |        |   /  Triangle 9    \                                   |    */
    /*  |        |  /                  \                                  |    */
    /*  |    8-1 | /                    \   9-1                           |    */
    /*  |    9-2 *-----------------------* 10-1                           |    */
    /*  |   10-2  \                     /                                 |    */
    /*  |          \                   /                                  |    */
    /*  |           \  Triangle 10    /                                   |    */
    /*  |            \               /                                    |    */
    /*  |             \             /                                     |    */
    /*  |              \           /                                      |    */
    /*  |               \         /                                       |    */
    /*  |                \       /                                        |    */
    /*  |                 \     /                                         |    */
    /*  |                  \   /                                          |    */
    /*  |                   \ /                                           |    */
    /*  |                    *  10-3                                      |    */
    /*  |                                                                 |    */
    /*  +-----------------------------------------------------------------+    */
    /*                                                                         */
    /***************************************************************************/


    /*   _                   _
    / | (_)_ __  _ __  _   _| |_
    | | | | `_ \| `_ \| | | | __|
    | | | | | | | |_) | |_| | |_
    |_| |_|_| |_| .__/ \__,_|\__|
                |_|
    */

    proc datasets library=workx kill;
    run;

    data workx.sphere;
      input x y z @@;
    cards4;
    -0.8 -0.4 -0.0 -0.8 -0.2 -0.2 -0.8 -0.2 -0.0 -0.8 -0.2 +0.2 -0.8 -0.0 -0.4 -0.8 -0.0 -0.2
    -0.8 -0.0 -0.0 -0.8 -0.0 +0.2 -0.8 -0.0 +0.4 -0.8 +0.2 -0.2 -0.8 +0.2 -0.0 -0.8 +0.2 +0.2
    -0.8 +0.4 -0.0 -0.6 -0.6 -0.2 -0.6 -0.6 -0.0 -0.6 -0.6 +0.2 -0.6 -0.4 -0.4 -0.6 -0.4 +0.4
    -0.6 -0.2 -0.6 -0.6 -0.2 +0.6 -0.6 -0.0 -0.6 -0.6 -0.0 +0.6 -0.6 +0.2 -0.6 -0.6 +0.2 +0.6
    -0.6 +0.4 -0.4 -0.6 +0.4 +0.4 -0.6 +0.6 -0.2 -0.6 +0.6 -0.0 -0.6 +0.6 +0.2 -0.4 -0.8 -0.0
    -0.4 -0.6 -0.4 -0.4 -0.6 +0.4 -0.4 -0.4 -0.6 -0.4 -0.4 +0.6 -0.4 -0.0 -0.8 -0.4 -0.0 +0.8
    -0.4 +0.4 -0.6 -0.4 +0.4 +0.6 -0.4 +0.6 -0.4 -0.4 +0.6 +0.4 -0.4 +0.8 -0.0 -0.2 -0.8 -0.2
    -0.2 -0.8 -0.0 -0.2 -0.8 +0.2 -0.2 -0.6 -0.6 -0.2 -0.6 +0.6 -0.2 -0.2 -0.8 -0.2 -0.2 +0.8
    -0.2 -0.0 -0.8 -0.2 -0.0 +0.8 -0.2 +0.2 -0.8 -0.2 +0.2 +0.8 -0.2 +0.6 -0.6 -0.2 +0.6 +0.6
    -0.2 +0.8 -0.2 -0.2 +0.8 -0.0 -0.2 +0.8 +0.2 -0.0 -0.8 -0.4 -0.0 -0.8 -0.2 -0.0 -0.8 -0.0
    -0.0 -0.8 +0.2 -0.0 -0.8 +0.4 -0.0 -0.6 -0.6 -0.0 -0.6 +0.6 -0.0 -0.4 -0.8 -0.0 -0.4 +0.8
    -0.0 -0.2 -0.8 -0.0 -0.2 +0.8 -0.0 -0.0 -0.8 -0.0 -0.0 +0.8 -0.0 +0.2 -0.8 -0.0 +0.2 +0.8
    -0.0 +0.4 -0.8 -0.0 +0.4 +0.8 -0.0 +0.6 -0.6 -0.0 +0.6 +0.6 -0.0 +0.8 -0.4 -0.0 +0.8 -0.2
    -0.0 +0.8 -0.0 -0.0 +0.8 +0.2 -0.0 +0.8 +0.4 +0.2 -0.8 -0.2 +0.2 -0.8 -0.0 +0.2 -0.8 +0.2
    +0.2 -0.6 -0.6 +0.2 -0.6 +0.6 +0.2 -0.2 -0.8 +0.2 -0.2 +0.8 +0.2 -0.0 -0.8 +0.2 -0.0 +0.8
    +0.2 +0.2 -0.8 +0.2 +0.2 +0.8 +0.2 +0.6 -0.6 +0.2 +0.6 +0.6 +0.2 +0.8 -0.2 +0.2 +0.8 -0.0
    +0.2 +0.8 +0.2 +0.4 -0.8 -0.0 +0.4 -0.6 -0.4 +0.4 -0.6 +0.4 +0.4 -0.4 -0.6 +0.4 -0.4 +0.6
    +0.4 -0.0 -0.8 +0.4 -0.0 +0.8 +0.4 +0.4 -0.6 +0.4 +0.4 +0.6 +0.4 +0.6 -0.4 +0.4 +0.6 +0.4
    +0.4 +0.8 -0.0 +0.6 -0.6 -0.2 +0.6 -0.6 -0.0 +0.6 -0.6 +0.2 +0.6 -0.4 -0.4 +0.6 -0.4 +0.4
    +0.6 -0.2 -0.6 +0.6 -0.2 +0.6 +0.6 -0.0 -0.6 +0.6 -0.0 +0.6 +0.6 +0.2 -0.6 +0.6 +0.2 +0.6
    +0.6 +0.4 -0.4 +0.6 +0.4 +0.4 +0.6 +0.6 -0.2 +0.6 +0.6 -0.0 +0.6 +0.6 +0.2 +0.8 -0.4 -0.0
    +0.8 -0.2 -0.2 +0.8 -0.2 -0.0 +0.8 -0.2 +0.2 +0.8 -0.0 -0.4 +0.8 -0.0 -0.2 +0.8 -0.0 -0.0
    +0.8 -0.0 +0.2 +0.8 -0.0 +0.4 +0.8 +0.2 -0.2 +0.8 +0.2 -0.0 +0.8 +0.2 +0.2 +0.8 +0.4 -0.0
    ;;;;
    run;


    /**************************************************************************************************************************/
    /*   WORKX.SPHERE total obs=138 29JUN2026:15:40:00                                                                        */
    /*  Obs       X       Y       Z                                                                                           */
    /*                                                                                                                        */
    /*    1    -0.8    -0.4    -0.0                                                                                           */
    /*    2    -0.8    -0.2    -0.2                                                                                           */
    /*    3    -0.8    -0.2    -0.0                                                                                           */
    /*    4    -0.8    -0.2     0.2                                                                                           */
    /*    5    -0.8    -0.0    -0.4                                                                                           */
    /*  ...                                                                                                                   */
    /*  134     0.8    -0.0     0.4                                                                                           */
    /*  135     0.8     0.2    -0.2                                                                                           */
    /*  136     0.8     0.2    -0.0                                                                                           */
    /*  137     0.8     0.2     0.2                                                                                           */
    /*  138     0.8     0.4    -0.0                                                                                           */
    /**************************************************************************************************************************/

    1                                          Altair SLC          10:33 Tuesday, June 30, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx


    NOTE: AUTOEXEC processing completed

    1          data workx.sphere;
    2           input x y z @@;
    3         cards4;

    NOTE: A new line was read when INPUT statement read past the end of a line
    NOTE: Data set "WORKX.sphere" has 138 observation(s) and 3 variable(s)
    NOTE: The data step took :
          real time : 0.016
          cpu time  : 0.015


    4         -0.8 -0.4 -0.0 -0.8 -0.2 -0.2 -0.8 -0.2 -0.0 -0.8 -0.2 +0.2 -0.8 -0.0 -0.4 -0.8 -0.0 -0.2
    5         -0.8 -0.0 -0.0 -0.8 -0.0 +0.2 -0.8 -0.0 +0.4 -0.8 +0.2 -0.2 -0.8 +0.2 -0.0 -0.8 +0.2 +0.2
    6         -0.8 +0.4 -0.0 -0.6 -0.6 -0.2 -0.6 -0.6 -0.0 -0.6 -0.6 +0.2 -0.6 -0.4 -0.4 -0.6 -0.4 +0.4
    7         -0.6 -0.2 -0.6 -0.6 -0.2 +0.6 -0.6 -0.0 -0.6 -0.6 -0.0 +0.6 -0.6 +0.2 -0.6 -0.6 +0.2 +0.6
    8         -0.6 +0.4 -0.4 -0.6 +0.4 +0.4 -0.6 +0.6 -0.2 -0.6 +0.6 -0.0 -0.6 +0.6 +0.2 -0.4 -0.8 -0.0
    9         -0.4 -0.6 -0.4 -0.4 -0.6 +0.4 -0.4 -0.4 -0.6 -0.4 -0.4 +0.6 -0.4 -0.0 -0.8 -0.4 -0.0 +0.8
    10        -0.4 +0.4 -0.6 -0.4 +0.4 +0.6 -0.4 +0.6 -0.4 -0.4 +0.6 +0.4 -0.4 +0.8 -0.0 -0.2 -0.8 -0.2
    11        -0.2 -0.8 -0.0 -0.2 -0.8 +0.2 -0.2 -0.6 -0.6 -0.2 -0.6 +0.6 -0.2 -0.2 -0.8 -0.2 -0.2 +0.8
    12        -0.2 -0.0 -0.8 -0.2 -0.0 +0.8 -0.2 +0.2 -0.8 -0.2 +0.2 +0.8 -0.2 +0.6 -0.6 -0.2 +0.6 +0.6
    13        -0.2 +0.8 -0.2 -0.2 +0.8 -0.0 -0.2 +0.8 +0.2 -0.0 -0.8 -0.4 -0.0 -0.8 -0.2 -0.0 -0.8 -0.0
    14        -0.0 -0.8 +0.2 -0.0 -0.8 +0.4 -0.0 -0.6 -0.6 -0.0 -0.6 +0.6 -0.0 -0.4 -0.8 -0.0 -0.4 +0.8
    15        -0.0 -0.2 -0.8 -0.0 -0.2 +0.8 -0.0 -0.0 -0.8 -0.0 -0.0 +0.8 -0.0 +0.2 -0.8 -0.0 +0.2 +0.8
    16        -0.0 +0.4 -0.8 -0.0 +0.4 +0.8 -0.0 +0.6 -0.6 -0.0 +0.6 +0.6 -0.0 +0.8 -0.4 -0.0 +0.8 -0.2
    17        -0.0 +0.8 -0.0 -0.0 +0.8 +0.2 -0.0 +0.8 +0.4 +0.2 -0.8 -0.2 +0.2 -0.8 -0.0 +0.2 -0.8 +0.2
    18        +0.2 -0.6 -0.6 +0.2 -0.6 +0.6 +0.2 -0.2 -0.8 +0.2 -0.2 +0.8 +0.2 -0.0 -0.8 +0.2 -0.0 +0.8
    19        +0.2 +0.2 -0.8 +0.2 +0.2 +0.8 +0.2 +0.6 -0.6 +0.2 +0.6 +0.6 +0.2 +0.8 -0.2 +0.2 +0.8 -0.0
    20        +0.2 +0.8 +0.2 +0.4 -0.8 -0.0 +0.4 -0.6 -0.4 +0.4 -0.6 +0.4 +0.4 -0.4 -0.6 +0.4 -0.4 +0.6
    21        +0.4 -0.0 -0.8 +0.4 -0.0 +0.8 +0.4 +0.4 -0.6 +0.4 +0.4 +0.6 +0.4 +0.6 -0.4 +0.4 +0.6 +0.4
    22        +0.4 +0.8 -0.0 +0.6 -0.6 -0.2 +0.6 -0.6 -0.0 +0.6 -0.6 +0.2 +0.6 -0.4 -0.4 +0.6 -0.4 +0.4
    23        +0.6 -0.2 -0.6 +0.6 -0.2 +0.6 +0.6 -0.0 -0.6 +0.6 -0.0 +0.6 +0.6 +0.2 -0.6 +0.6 +0.2 +0.6
    24        +0.6 +0.4 -0.4 +0.6 +0.4 +0.4 +0.6 +0.6 -0.2 +0.6 +0.6 -0.0 +0.6 +0.6 +0.2 +0.8 -0.4 -0.0
    25        +0.8 -0.2 -0.2 +0.8 -0.2 -0.0 +0.8 -0.2 +0.2 +0.8 -0.0 -0.4 +0.8 -0.0 -0.2 +0.8 -0.0 -0.0
    26        +0.8 -0.0 +0.2 +0.8 -0.0 +0.4 +0.8 +0.2 -0.2 +0.8 +0.2 -0.0 +0.8 +0.2 +0.2 +0.8 +0.4 -0.0
    27        ;;;;
    28        run;

    NOTE: Submitted statements took :
          real time : 0.127
          cpu time  : 0.093

    /*___                _   _                                                  _           _ _
    |___ \   _ __  _   _| |_| |__   ___  _ __     ___ ___  _ ____   _______  __| |__  _   _| | |
      __) | | `_ \| | | | __| `_ \ / _ \| `_ \   / __/ _ \| `_ \ \ / / _ \ \/ /| `_ \| | | | | |
     / __/  | |_) | |_| | |_| | | | (_) | | | | | (_| (_) | | | \ V /  __/>  < | | | | |_| | | |
    |_____| | .__/ \__, |\__|_| |_|\___/|_| |_|  \___\___/|_| |_|\_/ \___/_/\_\|_| |_|\__,_|_|_|
            |_|    |___/
    */

    %utlfkil(d:/png/convex_hull_3d.png);

    proc datasets lib=workx;
     delete
       vertex
       triangles
       triangle_coords;
    run;quit;

    options validvarname=upcase;
    options set=RHOME "C:\Progra~1\R\R-4.5.2\bin\r";

    proc r;
    export data=workx.sphere r=df;
    submit;
    # Load required libraries
    library(geometry)
    library(scatterplot3d)

    # Create output directory
    output_dir <- "d:/png"
    if (!dir.exists(output_dir)) {
      dir.create(output_dir, recursive = TRUE)
    }

    # Compute hull
    coords <- df
    hull <- convhulln(coords, options = "FA")

    # Get hull vertices (unique points)
    hull_vertices <- unique(as.vector(hull$hull))
    hull_coords <- coords[hull_vertices, ]
    colnames(hull_coords) <- c("X", "Y", "Z")

    vertex   <- data.frame(
      IDX = hull_vertices,           # Original row indices from coords
      X = hull_coords[, "X"],        # X coordinates
      Y = hull_coords[, "Y"],        # Y coordinates
      Z = hull_coords[, "Z"]         # Z coordinates
    )

    # GET TRIANGLE INFORMATION
    triangles <- hull$hull  # Matrix of triangle indices
    n_triangles <- nrow(triangles)

    # Print triangle information
    cat("\n============================================================\n")
    cat("TRIANGLE INFORMATION\n")
    cat("============================================================\n")
    cat("Number of unique vertices:", length(hull_vertices), "\n")
    cat("Number of triangles:", n_triangles, "\n")
    cat("\nFirst 10 triangles (vertex indices):\n")
    print(head(triangles, 10))

    str(triangles)

    # Create a data frame with triangle coordinates for SAS export
    # Each triangle becomes 3 rows (one per vertex)
    triangle_coords <- data.frame()
    for (i in 1:min(n_triangles, 50)) {  # Limit to first 50 triangles
      tri_indices <- triangles[i, ]
      tri_points <- coords[tri_indices, ]
      triangle_coords <- rbind(triangle_coords,
                               cbind(TriangleID = i,
                                     VertexID = 1:3,
                                     tri_points))
    }
    colnames(triangle_coords) <- c("TriangleID", "VertexID", "X", "Y", "Z")

    # Extract edges for plotting
    edge_pairs <- list()
    for (i in 1:nrow(hull$hull)) {
      tri <- hull$hull[i, ]
      edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[1], tri[2]))
      edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[2], tri[3]))
      edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[3], tri[1]))
    }
    edge_pairs <- unique(edge_pairs)

    # Create PNG
    cat("\nCreating PNG...\n")
    png_file <- file.path(output_dir, "convex_hull_3d.png")
    png(png_file, width = 4, height = 4, units = "in", res = 300)

    s3d <- scatterplot3d(
      coords,
      color = "blue",
      pch = 16,
      cex.symbols = .5,  # Larger blue points (increased from 1.0)
      xlab = "X",
      ylab = "Y",
      zlab = "Z",
      angle = 30,
      cex.lab = 0.4
    )

    # Add hull vertices - DECREASE cex for smaller red points
    s3d$points3d(hull_coords, col = "red", pch = 16, cex = 0.6)  # Smaller red points

    # Add edges - DECREASE lwd for thinner lines
    for (e in edge_pairs) {
      edge_coords <- coords[e, ]
      s3d$points3d(edge_coords, type = "l", col = "darkred", lwd = 1)  # Thinner lines
    }

    # Close the PNG device
    dev.off()
    cat("PNG saved to:", png_file, "\n")


    # Return multiple objects to SAS
    # 1. hull_coords - unique vertices
    # 2. triangles - triangle indices
    # 3. triangle_coords - triangle coordinates


    # Convert row names to a column named IDX using base R
    triangle_coords <- cbind(
      IDX = rownames(triangle_coords),
      triangle_coords
    )

    # Reset row names to numeric sequence (optional)
    rownames(triangle_coords) <- NULL

    # Display the result
    print(triangle_coords)

    endsubmit;

    * Import the hull vertices back to SAS;
    import r=vertex          data=workx.vertex;
    import r=triangles       data=workx.triangles;
    import r=triangle_coords data=workx.triangle_coords;
    run;


    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /* PYTHON                                                  SLC                                                            */
    /*                                                                                                                        */
    /* Altair SLC                                              WORKX.VERTEX total obs=48                                      */
    /*                                                                                                                        */
    /* Creating PNG using scatterplot3d...                     Obs    IDX       X       Y       Z                             */
    /*                                                                                                                        */
    /* PNG saved to: d:/png/convex_hull_3d.png                   1     24    -0.6     0.2     0.6                             */
    /*                                                           2     53    -0.2     0.6    -0.6                             */
    /* ========================================                  3     20    -0.6    -0.2     0.6                             */
    /* CONVEX HULL SUMMARY                                       4    115     0.6    -0.2    -0.6                             */
    /* ========================================                  5     81     0.0     0.8     0.4                             */
    /*                                                         ...                                                            */
    /* Number of hull vertices: 48                              44     35    -0.4     0.0    -0.8                             */
    /* Number of hull faces: 92                                 45      1    -0.8    -0.4     0.0                             */
    /*                                                          46     58     0.0    -0.8    -0.4                             */
    /* First 10 hull vertices:                                  47    103     0.4     0.0    -0.8                             */
    /*        X    Y    Z                                       48     93     0.2     0.6    -0.6                             */
    /* 24  -0.6  0.2  0.6                                                                                                     */
    /* 53  -0.2  0.6 -0.6                                                                                                     */
    /* 20  -0.6 -0.2  0.6                                                                                                     */
    /* 115  0.6 -0.2 -0.6                                                                                                     */
    /* 81   0.0  0.8  0.4                                                                                                     */
    /* 74   0.0  0.4  0.8                                                                                                     */
    /* 120  0.6  0.2  0.6                                                                                                     */
    /* 134  0.8  0.0  0.4                                                                                                     */
    /* 19  -0.6 -0.2 -0.6                                                                                                     */
    /* 14  -0.6 -0.6 -0.2                                                                                                     */
    /*                                                                                                                        */
    /*========================================================================================================================*/
    /*                                                                                                                        */
    /* $triangles 92 faces index=53 is (-0.2, 0.6,-0.6)        WORKX.TRIANGLES total obs=92                                   */
    /*                                                                                                                        */
    /*       [,1] [,2] [,3]                                    Obs     V1     V2     V3                                       */
    /*  [1,]   53   27   23                                                                                                   */
    /*  [2,]  110  115   85                                      1     53     27     23                                       */
    /*  [3,]  120  125   94                                      2    110    115     85                                       */
    /*  [4,]  116   86  112                                      3    120    125     94                                       */
    /*  [5,]   81   74   54                                      4    116     86    112                                       */
    /*                                                           5     81     74     54                                       */
    /*  [88,]  116  120  134                                    ...                                                           */
    /*  [89,]  116  134  126                                    88    116    120    134                                       */
    /*  [90,]  116  112  126                                    89    116    134    126                                       */
    /*  [91,]  116   66  104                                    90    116    112    126                                       */
    /*  [92,]  116   86   66                                    91    116     66    104                                       */
    /*                                                          92    116     86     66                                       */
    /*========================================================================================================================*/
    /*                                                                                                                        */
    /* $triangle_coords                                                                                                       */
    /*                                                                                                                        */
    /*    TriangleID VertexID     X     Y     Z                WORKX.TRIANGLE_COORDS total obs=150                            */
    /*                                                                                                                        */
    /* 53          1        1   -.2    .6   -.6                Obs    IDX TRIANGLEID VERTEXID       X       Y       Z         */
    /* 27          1        2   -.6    .6   -.2                                                                               */
    /* 23          1        3   -.6    .2   -.6                  1    24       1         1       -0.6     0.2     0.6         */
    /* 110         2        1    .6   -.6   -.2                  2    29       1         2       -0.6     0.6     0.2         */
    /* 115         2        2    .6   -.2   -.6                  3    54       1         3       -0.2     0.6     0.6         */
    /* 85          2        3    .2   -.6   -.6                  4    53       2         1       -0.2     0.6    -0.6         */
    /* 120         3        1    .6    .2    .6                  5    27       2         2       -0.6     0.6    -0.2         */
    /* 125         3        2    .6    .6    .2                                                                               */
    /* 94          3        3    .2    .6    .6                 46   273      49         2       -0.6     0.6    -0.2         */
    /*                                                          47   413      49         3       -0.4     0.8     0.0         */
    /*                                                          48   771      50         1        0.0     0.8    -0.4         */
    /*                                                          49   532      50         2       -0.2     0.6    -0.6         */
    /*                                                          50   274      50         3       -0.6     0.6    -0.2         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC          12:51 Tuesday, June 30, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    NOTE: Library slchelp assigned as follows:
          Engine:        WPD
          Physical Name: C:\Progra~1\Altair\SLC\2026\sashelp


    LOG:  12:51:29
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.025
          cpu time  : 0.000


    NOTE: Format num2mis output
    NOTE: Format $chr2mis output
    NOTE: Procedure format step took :
          real time : 0.015
          cpu time  : 0.015


    NOTE: AUTOEXEC processing completed

    1
    2         %utlfkil(d:/png/convex_hull_3d.png);

    Altair SLC

    The DATASETS Procedure

             Directory

    Libref           WORKX
    Engine           SAS7BDAT
    Physical Name    d:\wpswrkx

                                       Members

                                   Member
      Number    Member Name        Type         File Size      Date Last Modified

    -----------------------------------------------------------------------------

           1    SPHERE             DATA            131072      30JUN2026:12:50:40
           2    TRIANGLE_COORDS    DATA              5120      30JUN2026:12:47:52
    3
    4         proc datasets lib=workx;
    5          delete
    6            vertex
    7            triangles
    8            triangle_coords;
    9         run;quit;
    NOTE: Deleting "WORKX.TRIANGLE_COORDS" (memtype="DATA")
    NOTE: WORKX.VERTEX (memtype="DATA") was not found, and has not been deleted
    NOTE: WORKX.TRIANGLES (memtype="DATA") was not found, and has not been deleted
    NOTE: Procedure datasets step took :
          real time : 0.037
          cpu time  : 0.000


    10
    11        options validvarname=upcase;
    12        options set=RHOME "C:\Progra~1\R\R-4.5.2\bin\r";
    13
    14        proc r;
    NOTE: Using R version 4.5.2 (2025-10-31 ucrt) from C:\Program Files\R\R-4.5.2
    15        export data=workx.sphere r=df;
    NOTE: Creating R data frame 'df' from data set 'WORKX.sphere'

    16        submit;
    17        # Load required libraries
    18        library(geometry)
    19        library(scatterplot3d)
    20
    21        # Create output directory
    22        output_dir <- "d:/png"
    23        if (!dir.exists(output_dir)) {
    24          dir.create(output_dir, recursive = TRUE)
    25        }
    26
    27        # Compute hull
    28        coords <- df
    29        hull <- convhulln(coords, options = "FA")
    30
    31        # Get hull vertices (unique points)
    32        hull_vertices <- unique(as.vector(hull$hull))
    33        hull_coords <- coords[hull_vertices, ]
    34        colnames(hull_coords) <- c("X", "Y", "Z")
    35
    36        vertex   <- data.frame(
    37          IDX = hull_vertices,           # Original row indices from coords
    38          X = hull_coords[, "X"],        # X coordinates
    39          Y = hull_coords[, "Y"],        # Y coordinates
    40          Z = hull_coords[, "Z"]         # Z coordinates
    41        )
    42
    43        # GET TRIANGLE INFORMATION
    44        triangles <- hull$hull  # Matrix of triangle indices
    45        n_triangles <- nrow(triangles)
    46
    47        # Print triangle information
    48        cat("\n============================================================\n")
    49        cat("TRIANGLE INFORMATION\n")
    50        cat("============================================================\n")
    51        cat("Number of unique vertices:", length(hull_vertices), "\n")
    52        cat("Number of triangles:", n_triangles, "\n")
    53        cat("\nFirst 10 triangles (vertex indices):\n")
    54        print(head(triangles, 10))
    55
    56        str(triangles)
    57
    58        # Create a data frame with triangle coordinates for SAS export
    59        # Each triangle becomes 3 rows (one per vertex)
    60        triangle_coords <- data.frame()
    61        for (i in 1:min(n_triangles, 50)) {  # Limit to first 50 triangles
    62          tri_indices <- triangles[i, ]
    63          tri_points <- coords[tri_indices, ]
    64          triangle_coords <- rbind(triangle_coords,
    65                                   cbind(TriangleID = i,
    66                                         VertexID = 1:3,
    67                                         tri_points))
    68        }
    69        colnames(triangle_coords) <- c("TriangleID", "VertexID", "X", "Y", "Z")
    70
    71        # Extract edges for plotting
    72        edge_pairs <- list()
    73        for (i in 1:nrow(hull$hull)) {
    74          tri <- hull$hull[i, ]
    75          edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[1], tri[2]))
    76          edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[2], tri[3]))
    77          edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[3], tri[1]))
    78        }
    79        edge_pairs <- unique(edge_pairs)
    80
    81        # Create PNG
    82        cat("\nCreating PNG...\n")
    83        png_file <- file.path(output_dir, "convex_hull_3d.png")
    84        png(png_file, width = 4, height = 4, units = "in", res = 300)
    85
    86        s3d <- scatterplot3d(
    87          coords,
    88          color = "blue",
    89          pch = 16,
    90          cex.symbols = .5,  # Larger blue points (increased from 1.0)
    91          xlab = "X",
    92          ylab = "Y",
    93          zlab = "Z",
    94          angle = 30,
    95          cex.lab = 0.4
    96        )
    97
    98        # Add hull vertices - DECREASE cex for smaller red points
    99        s3d$points3d(hull_coords, col = "red", pch = 16, cex = 0.6)  # Smaller red points
    100
    101       # Add edges - DECREASE lwd for thinner lines
    102       for (e in edge_pairs) {
    103         edge_coords <- coords[e, ]
    104         s3d$points3d(edge_coords, type = "l", col = "darkred", lwd = 1)  # Thinner lines
    105       }
    106
    107       # Close the PNG device
    108       dev.off()
    109       cat("PNG saved to:", png_file, "\n")
    110
    111
    112       # Return multiple objects to SAS
    113       # 1. hull_coords - unique vertices
    114       # 2. triangles - triangle indices
    115       # 3. triangle_coords - triangle coordinates
    116
    117
    118       # Convert row names to a column named IDX using base R
    119       triangle_coords <- cbind(
    120         IDX = rownames(triangle_coords),
    121         triangle_coords
    122       )
    123
    124       # Reset row names to numeric sequence (optional)
    125       rownames(triangle_coords) <- NULL
    126
    127       # Display the result
    128       print(triangle_coords)
    129
    130       endsubmit;

    NOTE: Submitting statements to R:

    > # Load required libraries
    > library(geometry)
    Warning message:
    package 'geometry' was built under R version 4.5.3
    > library(scatterplot3d)
    >
    > # Create output directory
    > output_dir <- "d:/png"
    > if (!dir.exists(output_dir)) {
    +   dir.create(output_dir, recursive = TRUE)
    + }
    >
    > # Compute hull
    > coords <- df
    > hull <- convhulln(coords, options = "FA")
    >
    > # Get hull vertices (unique points)
    > hull_vertices <- unique(as.vector(hull$hull))
    > hull_coords <- coords[hull_vertices, ]
    > colnames(hull_coords) <- c("X", "Y", "Z")
    >
    > vertex   <- data.frame(
    +   IDX = hull_vertices,           # Original row indices from coords
    +   X = hull_coords[, "X"],        # X coordinates
    +   Y = hull_coords[, "Y"],        # Y coordinates
    +   Z = hull_coords[, "Z"]         # Z coordinates
    + )
    >
    > # GET TRIANGLE INFORMATION
    > triangles <- hull$hull  # Matrix of triangle indices
    > n_triangles <- nrow(triangles)
    >
    > # Print triangle information
    > cat("\n============================================================\n")
    > cat("TRIANGLE INFORMATION\n")
    > cat("============================================================\n")
    > cat("Number of unique vertices:", length(hull_vertices), "\n")
    > cat("Number of triangles:", n_triangles, "\n")
    > cat("\nFirst 10 triangles (vertex indices):\n")
    > print(head(triangles, 10))
    >
    > str(triangles)
    >
    > # Create a data frame with triangle coordinates for SAS export
    > # Each triangle becomes 3 rows (one per vertex)
    > triangle_coords <- data.frame()
    > for (i in 1:min(n_triangles, 50)) {  # Limit to first 50 triangles
    +   tri_indices <- triangles[i, ]
    +   tri_points <- coords[tri_indices, ]
    +   triangle_coords <- rbind(triangle_coords,
    +                            cbind(TriangleID = i,
    +                                  VertexID = 1:3,
    +                                  tri_points))
    + }
    > colnames(triangle_coords) <- c("TriangleID", "VertexID", "X", "Y", "Z")
    >
    > # Extract edges for plotting
    > edge_pairs <- list()
    > for (i in 1:nrow(hull$hull)) {
    +   tri <- hull$hull[i, ]
    +   edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[1], tri[2]))
    +   edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[2], tri[3]))
    +   edge_pairs[[length(edge_pairs) + 1]] <- sort(c(tri[3], tri[1]))
    + }
    > edge_pairs <- unique(edge_pairs)
    >
    > # Create PNG
    > cat("\nCreating PNG...\n")
    > png_file <- file.path(output_dir, "convex_hull_3d.png")
    > png(png_file, width = 4, height = 4, units = "in", res = 300)
    >
    > s3d <- scatterplot3d(
    +   coords,
    +   color = "blue",
    +   pch = 16,
    +   cex.symbols = .5,  # Larger blue points (increased from 1.0)
    +   xlab = "X",
    +   ylab = "Y",
    +   zlab = "Z",
    +   angle = 30,
    +   cex.lab = 0.4
    + )
    >
    > # Add hull vertices - DECREASE cex for smaller red points
    > s3d$points3d(hull_coords, col = "red", pch = 16, cex = 0.6)  # Smaller red points
    >
    > # Add edges - DECREASE lwd for thinner lines
    > for (e in edge_pairs) {
    +   edge_coords <- coords[e, ]
    +   s3d$points3d(edge_coords, type = "l", col = "darkred", lwd = 1)  # Thinner lines
    + }
    >
    > # Close the PNG device
    > dev.off()
    > cat("PNG saved to:", png_file, "\n")
    >
    >
    > # Return multiple objects to SAS
    > # 1. hull_coords - unique vertices
    > # 2. triangles - triangle indices
    > # 3. triangle_coords - triangle coordinates
    >
    >
    > # Convert row names to a column named IDX using base R
    > triangle_coords <- cbind(
    +   IDX = rownames(triangle_coords),
    +   triangle_coords
    + )
    >
    > # Reset row names to numeric sequence (optional)
    > rownames(triangle_coords) <- NULL
    >
    > # Display the result
    > print(triangle_coords)
    >

    NOTE: Processing of R statements complete

    131
    132       * Import the hull vertices back to SAS;
    133       import r=vertex          data=workx.vertex;
    NOTE: Creating data set 'WORKX.vertex' from R data frame 'vertex'
    NOTE: Data set "WORKX.vertex" has 48 observation(s) and 4 variable(s)

    134       import r=triangles       data=workx.triangles;
    NOTE: Creating data set 'WORKX.triangles' from R data frame 'triangles'
    NOTE: Data set "WORKX.triangles" has 92 observation(s) and 3 variable(s)

    135       import r=triangle_coords data=workx.triangle_coords;
    NOTE: Creating data set 'WORKX.triangle_coords' from R data frame 'triangle_coords'
    NOTE: Column names modified during import of 'triangle_coords'
    NOTE: Data set "WORKX.triangle_coords" has 150 observation(s) and 6 variable(s)

    136       run;
    NOTE: Procedure r step took :
          real time : 0.874
          cpu time  : 0.046


    137

    NOTE: Submitted statements took :
          real time : 1.048
          cpu time  : 0.156

    /*____       _        _____     _         _       _
    |___ /   ___| | ___  |___ /  __| |  _ __ | | ___ | |_ ___
      |_ \  / __| |/ __|   |_ \ / _` | | `_ \| |/ _ \| __/ __|
     ___) | \__ \ | (__   ___) | (_| | | |_) | | (_) | |_\__ \
    |____/  |___/_|\___| |____/ \__,_| | .__/|_|\___/ \__|___/
                                       |_|
    */

    /*--- UPPER AND LOWER PROJECTION ON XY PLANE ---*/

    data workx.upper_hemisphere;
      set workx.vertex(where=(z>=0));
        cz=scan(put(z,3.1),2,'.');
    run;

    options ls=64 ps=32;
    proc plot data=workx.upper_hemisphere;
      plot x*y=' '  $ cz /
             box
             haxis=-1 to +1 by .2
             vaxis=-1 to +1 by .2 ;
    run;quit;
    options ls=255 ps =255;


    data workx.upper_hemisphere;
      set workx.vertex(where=(z<=0));
        cz=scan(put(z,3.1),2,'.');
    run;

    /*--- EDIT THE MINUS SIGNS ---*/

    options ls=64 ps=32;
    proc plot data=workx.upper_hemisphere;
      plot x*y=' '  $ cz /
             box
             haxis=-1 to +1 by .2
             vaxis=-1 to +1 by .2 ;
    run;quit;
    options ls=255 ps =255;

    /**************************************************************************************************************************/
    /*              Upper Hemisphere Surface Triangle Vertices                                                                */
    /*                     XY Plane Points is Z corrdinate                                                                    */
    /*                      Quite a bit of editing                                                                            */
    /*                                   X                                                                                    */
    /*        -1.0 -0.8 -0.6 -0.4 -0.2  0.0  0.2  0.4  0.6  0.8  1.0                                                          */
    /*       ---+----+----+----+----+----+----+----+----+----+----+---                                                        */
    /*       | Projection of the upper hemisphere on xy plane e      |                                                        */
    /*       | on the x*y plane.                                     |                                                        */
    /*       | The numbers are the z coordinate time 10.             |                                                        */
    /*     Y |                                                       |  Y                                                     */
    /*   1.0 +                                                       +  1.0                                                   */
    /*       |                                                       |                                                        */
    /*   0.8 +                 0         4         0                 +  0.8                                                   */
    /*       |                                                       |                                                        */
    /*   0.6 +            2         6         6         2            +  0.6                                                   */
    /*       |                                                       |                                                        */
    /*   0.4 +      0                    8                   0       +  0.4                                                   */
    /*       |                                                       |                                                        */
    /*   0.2 +            6                             6            +  0.2                                                   */
    /*       |                                                       |                                                        */
    /*   0.0 +       4         8   Z VALUES        8         4       +  0.0                                                   */
    /*       |                                                       |                                                        */
    /*  -0.2 +            6                             6            + -0.2                                                   */
    /*       |                                                       |                                                        */
    /*  -0.4 +       0                   8                   0       + -0.4                                                   */
    /*       |                                                       |                                                        */
    /*  -0.6 +            2         6         6         2            + -0.6                                                   */
    /*       |                                                       |                                                        */
    /*  -0.8 +                 0         4         0                 + -0.8                                                   */
    /*       |                                                       |                                                        */
    /*  -1.0 +                                                       + -1.0                                                   */
    /*       |                                                       |                                                        */
    /*       ---+----+----+----+----+----+----+----+----+----+----+---                                                        */
    /*        -1.0 -0.8 -0.6 -0.4 -0.2  0.0  0.2  0.4  0.6  0.8  1.0                                                          */
    /*                                   X                                                                                    */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*             Lower Hemisphere Surface Triangle Vertices                                                                 */
    /*                     XY Plane Points is Z corrdinate                                                                    */
    /*                                                                                                                        */
    /*                                   X                                                                                    */
    /*        -1.0 -0.8 -0.6 -0.4 -0.2  0.0  0.2  0.4  0.6  0.8  1.0                                                          */
    /*       ---+----+----+----+----+----+----+----+----+----+----+---                                                        */
    /*       | Projection of the upper hemisphere on xy plane e      |                                                        */
    /*       | on the x*y plane.                                     |                                                        */
    /*       | The numbers are the z coordinate time 10.             |                                                        */
    /*     Y |                                                       |  Y                                                     */
    /*   1.0 +                                                       +  1.0                                                   */
    /*       |                                                       |                                                        */
    /*   0.8 +                 0        -4        0                  +  0.8                                                   */
    /*       |                                                       |                                                        */
    /*   0.6 +           -2        -6        -6        -2            +  0.6                                                   */
    /*       |                                                       |                                                        */
    /*   0.4 +       0                  -8                   0       +  0.4                                                   */
    /*       |                                                       |                                                        */
    /*   0.2 +           -6                            -6            +  0.2                                                   */
    /*       |                                                       |                                                        */
    /*   0.0 +      -4        -8    Z VALUES      -8        -4       +  0.0                                                   */
    /*       |                                                       |                                                        */
    /*  -0.2 +           -6                            -6            + -0.2                                                   */
    /*       |                                                       |                                                        */
    /*  -0.4 +       0                  -8                   0       + -0.4                                                   */
    /*       |                                                       |                                                        */
    /*  -0.6 +           -2        -6        -6        -2            + -0.6                                                   */
    /*       |                                                       |                                                        */
    /*  -0.8 +                0         -4        0                  + -0.8                                                   */
    /*       |                                                       |                                                        */
    /*  -1.0 +                                                       + -1.0                                                   */
    /*       |                                                       |                                                        */
    /*       ---+----+----+----+----+----+----+----+----+----+----+---                                                        */
    /*        -1.0 -0.8 -0.6 -0.4 -0.2  0.0  0.2  0.4  0.6  0.8  1.0                                                          */
    /*                                   X                                                                                    */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC        09:48 Wednesday, July  1, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    NOTE: Library slchelp assigned as follows:
          Engine:        WPD
          Physical Name: C:\Progra~1\Altair\SLC\2026\sashelp


    LOG:  9:48:46
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.032
          cpu time  : 0.000


    NOTE: Format num2mis output
    NOTE: Format $chr2mis output
    NOTE: Procedure format step took :
          real time : 0.015
          cpu time  : 0.000


    NOTE: AUTOEXEC processing completed

    1         data workx.upper_hemisphere;
    2           set workx.vertex(where=(z>0));
    3             cz=scan(put(z,3.1),2,'.');
    4         run;

    NOTE: 20 observations were read from "WORKX.vertex"
    NOTE: Data set "WORKX.upper_hemisphere" has 20 observation(s) and 5 variable(s)
    NOTE: The data step took :
          real time : 0.031
          cpu time  : 0.015


    5
    6         options ls=64 ps=32;
    7         proc plot data=workx.upper_hemisphere;
    8           plot x*y=' '  $ cz /
    9                  box
    10                 haxis=-1 to +1 by .2
    11                 vaxis=-1 to +1 by .2 ;
    12        run;quit;
    NOTE: Procedure plot step took :
          real time : 0.016
          cpu time  : 0.000


    13        options ls=255 ps =255;
    14

    NOTE: Submitted statements took :
          real time : 0.175
          cpu time  : 0.093

    /*  _         _        _        _                   _             _       _
    | || |    ___| | ___  | |_ _ __(_) __ _ _ __   __ _| | ___  _ __ | | ___ | |_ ___
    | || |_  / __| |/ __| | __| `__| |/ _` | `_ \ / _` | |/ _ \| `_ \| |/ _ \| __/ __|
    |__   _| \__ \ | (__  | |_| |  | | (_| | | | | (_| | |  __/| |_) | | (_) | |_\__ \
       |_|   |___/_|\___|  \__|_|  |_|\__,_|_| |_|\__, |_|\___|| .__/|_|\___/ \__|___/
                                                  |___/        |_|
    */

    data workx.three_triangles;
      set WORKX.TRIANGLE_COORDS(where=(8<=triangleid<=10));
      cz=scan(put(z,3.1),2,'.');
      id=cats(TRIANGLEID,'-',VERTEXID);
    run;quit;

    options ls=72 ps=32;
    proc plot data=workx.three_triangles;
       plot y*x='*' $ id/box
         haxis = -.1 to .7 by .1
         vaxis  = -.1 to .9 by .1;
    run;quit;


    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */


    /**************************************************************************************************************************/
    /*  WORKX.THREE_TRIANGLES total obs=9                                                                                     */
    /*                                                                                                                        */
    /*   IDX     TRIANGLEID    VERTEXID     X      Y      Z     CZ                                                            */
    /*                                                                                                                        */
    /*  741          8            1       0.0    0.4    0.8    8                                                              */
    /*  813          8            2       0.0    0.8    0.4    4                                                              */
    /*  94           8            3       0.2    0.6    0.6    6                                                              */
    /*                                                                                                                        */
    /*  120          9            1       0.6    0.2    0.6    6                                                              */
    /*  742          9            2       0.0    0.4    0.8    8                                                              */
    /*  941          9            3       0.2    0.6    0.6    6                                                              */
    /*                                                                                                                        */
    /*  1201        10            1       0.6    0.2    0.6    6                                                              */
    /*  743         10            2       0.0    0.4    0.8    8                                                              */
    /*  104         10            3       0.4    0.0    0.8    8                                                              */
    /*                                                                                                                        */
    /*  +-----------------------------------------------------------------+                                                   */
    /*  |  Triangles Pojected on xy Plane (recreation not to sale)        |                                                   */
    /*  |                                                                 |                                                   */
    /*  |        * 8-2             TRIANGLE VERTEX    X      Y      Z     |                                                   */
    /*  |        | \                                                      |                                                   */
    /*  |        |  \                  8       1    0.0    0.4    0.8     |                                                   */
    /*  |        |   \                 8       2    0.0    0.8    0.4     |                                                   */
    /*  |        |    \                8       3    0.2    0.6    0.6     |                                                   */
    /*  |        |     \                                                  |                                                   */
    /*  |        |      \              9       1    0.6    0.2    0.6     |                                                   */
    /*  |        |       \             9       2    0.0    0.4    0.8     |                                                   */
    /*  |        |        \            9       3    0.2    0.6    0.6     |                                                   */
    /*  |        |         \                                              |                                                   */
    /*  |        |          \         10       1    0.6    0.2    0.6     |                                                   */
    /*  |        |           \ 8-3    10       2    0.0    0.4    0.8     |                                                   */
    /*  |        |Triangle 8 * 9-3    10       3    0.4    0.0    0.8     |                                                   */
    /*  |        |           /\                                           |                                                   */
    /*  |        |          /  \                                          |                                                   */
    /*  |        |         /    \                                         |                                                   */
    /*  |        |        /      \                                        |                                                   */
    /*  |        |       /        \                                       |                                                   */
    /*  |        |      /          \                                      |                                                   */
    /*  |        |     /            \                                     |                                                   */
    /*  |        |    /              \                                    |                                                   */
    /*  |        |   /  Triangle 9    \                                   |                                                   */
    /*  |        |  /                  \                                  |                                                   */
    /*  |    8-1 | /                    \   9-1                           |                                                   */
    /*  |    9-2 *-----------------------* 10-1                           |                                                   */
    /*  |   10-2  \                     /                                 |                                                   */
    /*  |          \                   /                                  |                                                   */
    /*  |           \  Triangle 10    /                                   |                                                   */
    /*  |            \               /                                    |                                                   */
    /*  |             \             /                                     |                                                   */
    /*  |              \           /                                      |                                                   */
    /*  |               \         /                                       |                                                   */
    /*  |                \       /                                        |                                                   */
    /*  |                 \     /                                         |                                                   */
    /*  |                  \   /                                          |                                                   */
    /*  |                   \ /                                           |                                                   */
    /*  |                    *  10-3                                      |                                                   */
    /*  |                                                                 |                                                   */
    /*  +-----------------------------------------------------------------+                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC        10:14 Wednesday, July  1, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    NOTE: Library slchelp assigned as follows:
          Engine:        WPD
          Physical Name: C:\Progra~1\Altair\SLC\2026\sashelp


    LOG:  10:14:50
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.015
          cpu time  : 0.015


    NOTE: Format num2mis output
    NOTE: Format $chr2mis output
    NOTE: Procedure format step took :
          real time : 0.015
          cpu time  : 0.015


    NOTE: AUTOEXEC processing completed

    1
    2         options ls=72 ps=32;
    3         proc plot data=workx.three_triangles;
    4            plot y*x='*' $ id/box
    5              haxis = -.1 to .7 by .1
    6              vaxis  = -.1 to .9 by .1;
    7         run;quit;
    NOTE: Procedure plot step took :
          real time : 0.015
          cpu time  : 0.015


    8

    NOTE: Submitted statements took :
          real time : 0.110
          cpu time  : 0.109
    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
