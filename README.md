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
   - *Evaluates to `True` if the point lies on the airfoil*


#### Notes on design.

#### Challenges:
1. **Memory Usage**
   - `af.dataset.load` pulls all data into RAM, little left to play with.

2. **Data Structure**
   - Indexing is a bit complex because our dataset is a list of ndarray simulations.
   - For example, to find the 500,000th data point, we need to find the index of the simulation it belongs to first.
   - This is challenging, because each simulation has a different number of data points.

#### Approach:
- **First idea**: Create a dataset to hold target features (position, sdf, v_pos) and simply run the ML model on that.
   - **Pros**: Straightforward, readable code; still a viable option.
   - **Cons**: Requires copying data, which quickly exceeded Google Colab memory limits. (No $$.)
   - **Next steps**: Consider chunking the data, possibly loading only parts at a time to avoid RAM overload.

#### Solution:
- **Avoid making any copies and directly reference data in RAM.**
   - **Pros**: Keeps RAM usage low! No need to spend money.
   - **Cons**: Less readable code. (I sorry <3)
   - **Details**: Solved the indexing problem without data copies by mapping a given index to a `sim_id` and `row`.
      - Stored valid index ranges of each simulation (e.g., sim 0: [0, 170180], sim 1: [170181, 320912], ...) in an array,
      - and used binary search to find `sim_id`.
   - **Next steps**: Do sanity check with teammates who understand physics part of it. Test the current code and explore how
     Geometric Deep Learning libraries can help!
