Back to :ref:`card-index`

Back to :ref:`region-card`

.. _polygonal-region-card:

POLYGON
=======

Define a volume as the intersection of one, two, or three polygons
in the coordinate planes. Each polygon is extruded along the unused
axis (``XY`` along :math:`z`, ``XZ`` along :math:`y`, ``YZ`` along
:math:`x`).
A coordinate plane that is omitted is treated as infinite.

By default a cell is included if its **center** lies in every
defined extrusion. See :ref:`polygon-theory` in the Theory Guide.

Required Cards:
---------------

POLYGON
  Opens the POLYGON block within a REGION block.

Within the POLYGON block, one or more of:

 XY
  Vertices of a polygon in the XY plane. Two points define an
  axis-aligned rectangle. :math:`N > 2` points define a simple polygon
  and must be listed clockwise or counter-clockwise without
  repeating the first vertex. The unused coordinate (:math:`z`) is
  required on each line and is ignored. At most 100 vertices.

   ::

    XY
      x0 y0 z0
      x1 y1 z1
      x2 y2 z2
      ...
      xN yN zN
    /

 XZ
  Same as XY, but in the XZ plane (unused coordinate is :math:`y`).

 YZ
  Same as XY, but in the YZ plane (unused coordinate is :math:`x`).

Optional Cards:
---------------

TYPE <string>
  How the volume is mapped onto the grid.

  CELL_CENTERS_IN_VOLUME
    Default. Include a cell if its center lies in every defined
    extrusion. Cell-body intersection is not tested. All grid types.

  BOUNDARY_FACES_IN_VOLUME
    Include boundary faces whose centroids lie in the volume.
    Implicit unstructured grids only.

Examples
--------
 ::

  REGION polyvol_xy
    POLYGON
      XY
        1. 1. 0.
        1. 2. 0.
        2. 2. 0.
        2. 4. 0.
        3. 4. 0.
        3. 2. 0.
        4. 2. 0.
        4. 1. 0.
      /
      XZ
        0. 0. 3.
        5. 5. 4.
      /
    /
  END


  REGION pond
    POLYGON
      TYPE BOUNDARY_FACES_IN_VOLUME
      XY
        1081.09 512.609 0.
        1008.38 536.404 0.
        957.98 554.706 0.
        904.05 562.406 0.
        817.357 580.904 0.
        734.512 585.373 0.
        683.75 579.356 0.
        605.18 536.218 0.
        585.15 490. 0.
        638.527 440.49 0.
        704.511 387.615 0.
        775.457 384.037 0.
        860.4 401.267 0.
        950.316 432.744 0.
        1015.65 472.986 0.
      /
      XZ
        0. 0. 1.
        1126. 0. -22.
      /
    /
  END
