Back to :ref:`card-index`

Back to :ref:`region-card`

.. _planar-patch-region-card:

PLANAR_PATCH
============

Define a finite-thickness elliptical or rectangular patch in an
arbitrary plane. A cell is assigned to the region if the cell
**intersects** the patch (not merely if the cell center lies inside
it). See :ref:`planar-patch-theory` in the Theory Guide.

Required Cards:
---------------

PLANAR_PATCH
  Opens the PLANAR_PATCH block within a REGION block.

CENTROID <float float float>
  Coordinates of the patch center :math:`\mathbf{c}`.

  ::

    CENTROID x y z

RADII <float float>
  In-plane semi-axes :math:`a` and :math:`b` (metres). The first radius
  lies along :math:`\hat{\mathbf{e}}_1` (the XY-trace for ``ANGLES``,
  or the projected ``AXIS`` for ``NORMAL``). Both values must be
  positive.

  ::

    RADII a b

HALF_THICKNESS <float>
  Half-aperture :math:`h` (metres) measured along the plane normal.
  Must be greater than zero. The patch occupies
  :math:`|\mathbf{n}\cdot(\mathbf{x}-\mathbf{c})| \le h`.

Exactly one of:

  ANGLES <float float>
    Trace angles in degrees. The first is the map-view (XY) trace from
    :math:`+X` toward :math:`+Y`. The second is the XZ-section trace from
    :math:`+X` toward :math:`+Z`. These angles define the plane of the
    patch.

    ::

      ANGLES theta_xy theta_xz

  NORMAL <float float float>
    Plane normal (normalized internally). Requires ``AXIS``.

    ::

      NORMAL nx ny nz

    AXIS <float float float>
      In-plane direction for the first radius. Projected onto the plane
      (must not be parallel to ``NORMAL``).

      ::

        AXIS ax ay az

Optional Cards:
---------------

SHAPE <string>
  ``ELLIPSE`` (default) or ``RECTANGLE``.

Examples
--------
 ::

  REGION fault
    PLANAR_PATCH
      CENTROID 22.75 375. 150.
      ANGLES 45. 45.
      SHAPE ELLIPSE
      RADII 80. 50.
      HALF_THICKNESS 0.5
    /
  END

  REGION cap
    PLANAR_PATCH
      CENTROID 10.5 10.5 10.5
      NORMAL 0.d0 0.d0 1.d0
      AXIS 1.d0 0.d0 0.d0
      SHAPE ELLIPSE
      RADII 5.d0 3.d0
      HALF_THICKNESS 0.6d0
    /
  END

  REGION panel
    PLANAR_PATCH
      CENTROID 0. 0. 0.
      NORMAL 1. -1. -1.
      AXIS 0.707106781 0.707106781 0.
      SHAPE RECTANGLE
      RADII 20. 10.
      HALF_THICKNESS 1.
    /
  END
