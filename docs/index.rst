=====================
Python C3D Processing
=====================

This package provides a single Python module for reading and writing binary
motion-capture files in the `C3D file format`_.

.. _C3D file format: https://www.c3d.org/HTML/default.htm

Examples
========

Reading
-------

To read the frames of a C3D file, use a :class:`Reader <c3d.Reader>` instance::

  import c3d

  reader = c3d.Reader(open('my-motion.c3d', 'rb'))
  for i, points, analog in reader.read_frames():
      print('frame {}: point {}, analog {}'.format(
          i, points.shape, analog.shape)

The :func:`read_frames <c3d.Reader.read_frames>` method generates tuples
containing the frame index, a ``numpy`` array of point data, and a ``numpy``
array of analog data.

Writing
-------

To write data frames to a C3D file, use a :class:`Writer <c3d.Writer>`
instance::

  import c3d
  import numpy as np

  writer = c3d.Writer()
  for _ in range(100):
      writer.add_frame(np.random.randn(30, 5))
  with open('random-points.c3d', 'wb') as h:
      writer.write(h)

The :func:`add_frame <c3d.Writer.add_frame>` method takes a ``numpy`` array of
point data---and, optionally, a ``numpy`` array of analog data---and adds it to
an internal data buffer. The :func:`write <c3d.Writer.write>` method serializes
all of the frame data to a C3D binary file.

Command-Line Scripts
====================

The ``c3d`` package also contains several command-line scripts.

Two of these scripts convert C3D binary data to other formats:
- ``c3d2csv``: Converts C3D data to comma-separated values.
- ``c3d2npz``: Converts C3D data to serialized ``numpy`` arrays.

The ``c3d-metadata`` script simply prints out the metadata from a C3D file.

Finally, the ``c3d-viewer`` script provides a basic OpenGL viewer for C3D data.
This script depends on ``pyglet``.

.. toctree::
   :maxdepth: 2

   reference
