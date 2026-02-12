# Are We XDMF Yet

A collection of [XDMF](https://www.xdmf.org/index.html) files demonstrating some bugs related to [ParaView](https://www.paraview.org/)'s handling of the format.

## Reproducing

Open up the `XDMF` files with `paraview`, and select one of the readers. The `XDMF2` reader is the most stable and feature-complete one, but different readers have different bugs. Open the `XDMF` file with a text editor and read the comments that explain what to look for.

So far, I tested these examples on the following `paraview` versions:
- `6.0.1`

## Bug categories

Bugs are listed by category for both `XDMF2` and `XDMF3` readers. Check the comments in the `XDMF` files to see which bug is produced by what reader.

### Attribute size inconsistency

- `vector_attributes.xdmf` demonstrates inconsistencies with vector attributes that don't exactly have 3 components (X Y Z).
    - 1-component vector attribute segfaults.
    - 2-component vector attribute is padded to become a 3-component vector.
    - Vector attributes with more than 3 components are treated as 3-component vectors.

- `matrix_attributes.xdmf` demonstrates inconsistencies with matrix attributes.
    - Rows after the first one of any matrix attribute of rank 2 are ignored.
    - Any matrix attribute of size 6 in its last dimension is interpreted as a symmetric 3x3 matrix.
    - Rows and columns of rank 3 matrices are ignored.
    - Any dimension other than the last one of a matrix with high rank (more than 2) is ignored.

### Broken `Coordinates` type for `DataItem`s

- `coordinate.xdmf` demonstrates that even the simplest use case of the `Coordinates` type of `DataItem` (select a subset of scalars) is broken.

### Broken `Hyperslab` type for `DataItem`s

- todo
