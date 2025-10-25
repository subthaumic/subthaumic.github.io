---
layout: "page"
title: "GUDHI Tutorial"
permalink: "/projects/ep-math-data/gudhi-tutorial/"
archived: true
archive_source: "STRUCTURES Wiki"
archive_captured: "Oct 2025"
primary_editor: "Dspitz"
primary_edit_count: "18"
total_edits: "18"
first_editor: "Dspitz"
first_edit: "2019-05-05T19:06:57Z"
last_editor: "Dspitz"
last_edit: "2019-05-22T10:12:35Z"
---
> This article was originally written by Daniel Spitz for the STRUCTURES Wiki (captured October 2025).


In this tutorial we will learn how to employ the C++ library GUDHI (Geometric understanding in higher dimensions) in order to compute the Delaunay complex and alpha shapes of given point cloud data. For a more complete picture of GUDHI we refer to the project homepage and recommend reading the tutorials provided there: http://gudhi.gforge.inria.fr/.

A selection of promising starting points for individual applications beyond alpha shapes is given by means of links to GUDHI example codes. Additionally, on the GUDHI webpage dozens of useful code example are provided, numerically implementing a multitude of computational topology methods, http://gudhi.gforge.inria.fr/doc/latest/examples.html.

This tutorial describes the numerics leading to results as in [What is Topological Data Analysis? - A Primer](https://wiki.structures.mathi.uni-heidelberg.de/index.php?title=What_is_Topological_Data_Analysis%3F_-_A_Primer).

## Installation
To be able to compile code against the GUDHI library and in particular to run the following example, some prerequisites need to be fulfilled. The free third-party C++ libraries CGAL and Eigen3 need to be installed to create alpha shapes. To make use of the interesting multi-field persistent homology algorithm, additionally, the arbitrary-precision arithmetic library GMP needs to be installed.

CGAL can be obtained from https://www.cgal.org/. 

Eigen3 can be obtained from http://eigen.tuxfamily.org/index.php?title=Main_Page.

GMP can be obtained from https://gmplib.org/.

For useful and up-to-date information on how to install GUDHI and these third-party libraries we refer to its installation manual, http://gudhi.gforge.inria.fr/doc/latest/installation.html.

## Creating the example point cloud
The basis of any topological data analysis routine is a point cloud of data. For instance, the following lines of code generate npoints lying on a circle of radius r  with Gaussian noise of width sigma  added on top:

   Vector_of_points pts;
   std::random_device rd;          // obtain a seed for the random number engine
   std::mt19937 gen(rd());         // mersenne_twister_engine seeded with rd()
   std::uniform_real_distribution<> dist_uniform(0.,2.*M_PI);
   std::normal_distribution dist_normal(0.,sigma);
   double phase, x, y;
   for (long i=0; i
GUDHI uses the Computational Geometry Algorithms Library, [CGAL](https://wiki.structures.mathi.uni-heidelberg.de/index.php?title=List_of_Software#CGAL), to compute e.g. the Delaunay complex and alpha shapes of a given point cloud. As such, point clouds need to be provided as CGAL data type objects. In the two dimensional case of interest in this tutorial the data type of pts reads std::vector >::Point_d>. 

## Generating alpha shapes
Using the GUDHI library, the following lines of code compute all alpha shapes of the point cloud pts at once. For details on the data type of pts we refer to the end of the previous subsection. 

 // Set maximum alpha radius to infinity, restoring the Delaunay complex in the limiting case
 double alpha_square_max_value {std::numeric_limits::infinity()};
 
 // Initialize the alpha complex of the point cloud
 Gudhi::alpha_complex::Alpha_complex alpha_complex_from_points(pts);
   
 // Initialize the corresponding simplex tree to store the complex
 Simplex_tree simplex_tree;
 
 // Create the complex
 alpha_complex_from_points.create_complex(simplex_tree, alpha_square_max_value)

A simplex tree is a particularly efficient and memory-saving data format to store abstract simplicial complexes, providing cheap algorithms to compute for example faces and cofaces of a given simplex. For more details we refer to the original publication by Boissonat and Maria 2012.

## Computing persistent homology
Given the alpha shapes of an input point cloud, stored in the object simplex_tree, we can finally compute the persistent homology of the filtration of alpha shapes. The following lines of code first initialize the alpha shape filtration. Then the coefficient field of interest, \mathbb{Z}/2\mathbb{Z}, is set and the persistent homology structure, called pcoh, is initialized. The last line then actually does the persistent homology computation, using an efficient persistent cohomology algorithm as mentioned in Maria et al 2014.

 // Sort simplices in filtration order
 simplex_tree.initialize_filtration();
 
 // Compute the persistence diagram of the complex
 int coeff_field_characteristic = 2;
 Gudhi::persistent_cohomology::Persistent_cohomology pcoh(simplex_tree);
 Filtration_value min_persistence = 0.;
 pcoh.init_coefficients(coeff_field_characteristic);
 pcoh.compute_persistent_cohomology(min_persistence);

As the nomenclature in this example code already suggests, GUDHI is capable of computing persistent homology with coefficients in different fields of interest. Actually, the GUDHI persistent cohomology algorithm is capable of computing persistent homology classes of different fields simultaneously, providing effective means to unveil torsional features in point clouds. Again, for details we refer to .

## Further example routines
In this section a selection of GUDHI example codes is linked and described in brevity. A multitude of further example codes can be found here: http://gudhi.gforge.inria.fr/doc/latest/examples.html.

#### Vietoris-Rips complex
GUDHI is capable of computing the Vietoris-Rips complex to a given point cloud as described in detail in the following example: http://gudhi.gforge.inria.fr/doc/latest/_rips_complex_2example_one_skeleton_rips_from_points_8cpp-example.html.

#### Witness complex and persistence
The following example describes how to compute the witness complex of a given input file containing the point cloud of interest, randomly picking landmark points and finally computing persistent homology classes: http://gudhi.gforge.inria.fr/doc/latest/_witness_complex_2weak_witness_persistence_8cpp-example.html.

#### A custom simplex tree
Simplex trees, i.e., the efficient data format that GUDHI employs for storing simplicial complexes, can also be build by hand: http://gudhi.gforge.inria.fr/doc/latest/_simplex_tree_2simple_simplex_tree_8cpp-example.html.

#### Multifield persistence
GUDHI is capable of computing persistent homology of different ground fields simultaneously. The following example describes code details of this: http://gudhi.gforge.inria.fr/doc/latest/_persistent_cohomology_2rips_multifield_persistence_8cpp-example.html.

#### Persistence representations: Persistence landscapes
GUDHI has routines implemented to compute various derived quantities from persistence diagrams. A particularly useful such quantity with regard to statistical applications of persistent homology is the persistence landscape. The following routine describes the way GUDHI computes these landscapes: http://gudhi.gforge.inria.fr/doc/latest/_persistence_representations_2persistence_landscape_8cpp-example.html.

#### Bottleneck distance
Metrics exist that make the space of persistence diagrams a metric space, such as for example the bottleneck distance. Given two persistence diagrams, their bottleneck distance can be computed via GUDHI as described here: http://gudhi.gforge.inria.fr/doc/latest/_bottleneck_distance_2bottleneck_distance_8cpp-example.html.

## The entire C++ script
The following code is the entire script described in the previous subsections. Output generation lines of code have been added here.

 /* This script computes via GUDHI alpha shapes and persistent homology of points sampled from a circle with noise added
 Arguments to this program are:
 (1)    Radius of the circle
 (2)    Number of points to sample
 (3)    Sigma of Gaussian noise
 
 For further information on the alpha shape construction functions employed, cf. e.g.
 http://gudhi.gforge.inria.fr/doc/latest/_alpha_complex_2alpha_complex_persistence_8cpp-example.html
 
 To compile use e.g.:
 g++ alpha_shapes.cpp -std=c++11 -lgmp -lCGAL -I /usr/local/include -I /usr/local/include/Eigen/ -lboost_system -I /home/daniel/Documents/2018-09-04-14-25-00_GUDHI_2.3.0/include -o alpha_shapes  
 */
 
 #define M_PI 3.14159265358979323846
 #include 
 #include 
 #include 
 #include 
 #include 
 #include 
 #include               // for numeric limits
 #include 
 #define CGAL_EIGEN3_ENABLED    // auxiliary setting
 #include 
 #include 
 #include 
 #include 
 
 using Kernel = CGAL::Epick_d >;
 using Point = Kernel::Point_d;
 using Vector_of_points = std::vector;
 using Simplex_tree = Gudhi::Simplex_tree<>;
 using Filtration_value = Simplex_tree::Filtration_value;
 
 int main(int argc, char *argv[])
 {
   // Get spherical point cloud parameters from input
   double r, sigma;
   long n;
   if (argc==4)
   {
     r = std::atof(argv[1]);
     n = std::atol(argv[2]);
     sigma = std::atof(argv[3]);
   } 
   else 
   {
     r = 1.;
     n = 100;
     sigma = 0.1;
     std::cout  dist_uniform(0.,2.*M_PI);
   std::normal_distribution dist_normal(0.,sigma);
   double phase, x, y;
   std::ofstream out_pts("pts.dat", std::ofstream::out);
   for (long i=0; i::infinity()};
   
   // Initialize the alpha complex of the point cloud
   Gudhi::alpha_complex::Alpha_complex alpha_complex_from_points(pts);
   
   // Initialize the corresponding simplex tree to store the complex
   Simplex_tree simplex_tree;
   
   // Create the complex
   char name[1000];
   if (alpha_complex_from_points.create_complex(simplex_tree, alpha_square_max_value))
   {
     std::cout  pcoh(simplex_tree);
   Filtration_value min_persistence = 0.;
   pcoh.init_coefficients(coeff_field_characteristic);
   pcoh.compute_persistent_cohomology(min_persistence);
   
   // Print persistence diagram to file
   std::ofstream out_dgm("dgm.dat", std::ofstream::out);
   pcoh.output_diagram(out_dgm);
   out_dgm.close();
   
   return 0;
 }

## References
