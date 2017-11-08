# tsne
tSNE--A Visualization Technique

## An Example of Visualization

We are familiar with maps (or atlases or charts).
A map represents continents, countries and the like as two-dimensional figures.
A continent, or a country have a three-dimensional topography.
For example, in the US, think to yourself how high the Rocky Mountains are, and how deep the Grand Canyon is.
That should convince you that the US (or for that matter any country) is a three-dimensional geometrical figure.
But on a map, the US is a two-dimensional gemetrical figure.
That is a good example of visualization.

## Mathematical Statement of the Visualization Problem

We are given a .csv file, such as this one:

    1    2    3    4
    3    2    1    5
    6    0    1    4
    7    8    9    6
    5    6    4    9
    
The .csv file above has 4 columns.
Let us denote the number of columns as m; in our example, m = 4.
We will suppose that m is a given integer > 2.
Why should m > 2?
If m <=2 there is no need for a special visualization algorithm---we can directly plot the columns in the XY plane!
The need for a visualization algorithm arises only if m > 2.

In the example above there are 5 rows.
The objective of the visualization algorithm is to generate 5x2 = 10 numbers,

    a b c d e f g h i j

such that:

    the pair (a, b) is in some sense a representative (or proxy) for the 1st row of the .csv file
    the pair (c, d) is in some sense a representative (or proxy) for the 2nd row of the .csv file
    the pair (e, f) is in some sense a representative (or proxy) for the 3rd row of the .csv file
    the pair (g, h) is in some sense a representative (or proxy) for the 4th row of the .csv file
    the pair (i, j) is in some sense a representative (or proxy) for the 5th row of the .csv file
    
 What do we mean by the phrase "in some sense a representative (or proxy)"?
 Recall that the first row is a point in R^4, (1, 2, 3, 4).
 It is not possible to draw a 4D point.
 Now let us turn to the pair (a, b), which is described as being a representative (or proxy).
 (a, b) is a point in R^2.
 We can certainly mark a point (a, b) in R^2, provided, of course, our algorithm has computed the
 values of a and b.
 For example, if our algorithm has computed that a=2.5, b = 2.7, we can mark the point (2.5, 2.7)
 on a sheet of graph paper.
 (A sheet of graph paper is R^2!)
 We can say that (2.5, 2.7) is a representative (or proxy) of the 4D point (1, 2, 3, 4).
 
