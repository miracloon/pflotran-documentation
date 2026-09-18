.. _polygon-theory:

Polygon
=======

A polygonal volume is the intersection of one, two, or three
polygons, each defined in a coordinate plane and extruded along the
unused axis. The corresponding input card is
:ref:`polygonal-region-card`.

Volume
------

Let :math:`P_{xy}`, :math:`P_{xz}`, and :math:`P_{yz}` be
(possibly undefined) polygonal regions in the :math:`xy`,
:math:`xz`, and :math:`yz` planes. The volume is

.. math::

   V = E_z(P_{xy}) \;\cap\; E_y(P_{xz}) \;\cap\; E_x(P_{yz}),

where :math:`E_z(P_{xy})` is the extrusion of :math:`P_{xy}` along
:math:`z` (all :math:`z`), and similarly for the other two. If a
polygon is not supplied, that extrusion is taken to be all of
:math:`\mathbb{R}^3`. Thus one polygon is an infinite prism; two
polygons are the intersection of two prisms; three polygons bound
a finite body aligned with the coordinate axes.

A two-vertex list in a given plane is interpreted as an
axis-aligned rectangle (the bounding box of the two points). More
than two vertices define a simple polygon; they must be ordered
clockwise or counter-clockwise and must not repeat the first
vertex. At most 100 vertices are stored per plane. The unused
coordinate on each vertex is required in the input and is ignored
in the in-plane test.

Point in polygon
----------------

Membership in a 2-D polygon is the even-odd ray test along
:math:`+x` in the in-plane coordinates :math:`(x',y')`:

- :math:`XY` uses :math:`(x,y)`
- :math:`XZ` uses :math:`(x,z)`
- :math:`YZ` uses :math:`(y,z)`

An edge from :math:`(x_i,y_i)` to :math:`(x_j,y_j)` contributes a
crossing when one endpoint is strictly below the query :math:`y'`
and the other is at or above it, and the intersection abscissa is
strictly less than the query :math:`x'`. Horizontal edges do not
contribute. The point is inside if the number of crossings is
odd.

A point :math:`\mathbf{x}=(x,y,z)` lies in :math:`V` if and only
if it lies in every *defined* 2-D polygon (equivalently, in every
defined extrusion).

Cell mapping
------------

``CELL_CENTERS_IN_VOLUME`` (default)
  A cell is in the region iff its center lies in :math:`V`. The cell
  body is not tested. Supported on structured, implicit
  unstructured, and explicit unstructured grids.

``BOUNDARY_FACES_IN_VOLUME``
  The same point-in-volume test is applied to the centroids of
  faces on the domain boundary. Implemented for implicit
  unstructured grids only.

Because each polygon is extruded along a coordinate axis, the
intersection of two or three filled polygons is a prismatic body
whose generators are axis-aligned. A dipping geologic surface is
not a thin sheet in this representation: its coordinate-plane
projections, once extruded and intersected, occupy a volume whose
thickness is set by the size of those projections, not by a
prescribed aperture.
