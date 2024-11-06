# Navier Coding Challenge

#### Dataset basics.

#### Dataset_name
- **Type**: `<class 'list'>` containing elements of type `<class 'str'>`
- **Example Element**: `airFoil2D_SST_58.831_-3.563_2.815_4.916_10.078`
- **Length**: 504 elements
  - **NACA 4-digit count**: 239
  - **NACA 5-digit count**: 265
- **Inlet Velocity Range**: 46.84 to 77.95
- **Angle of Attack Range**: -4.93 to 14.79

#### Dataset_list
- **Type**: `<class 'list'>` containing elements of type `<class 'numpy.ndarray'>`
- **Length**: 504 elements
- **Shape of Each Element**: `(N, 12)`
  - **N**: Number of points in each simulation
  - **12**: Number of features
- **Number of Points in First Simulation (as reference)**: 170,180
  - *Note*: The number of points varies slightly across simulations.

#### Description of 12 Features (in order)
0. Position x
1. Position y
2. Inlet velocity (x)
3. Inlet velocity (y)
4. Distance to airfoil
5. Normals a
6. Normals b
7. Velocity x
8. Velocity y
9. Pressure/kin. mass
10. Kinematic viscosity
11. Boolean Flag*
   - *Evaluates to `True` if the point lies on the airfoil* to a `sim_id` and `row`.
