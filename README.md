# tsne
tSNE--A Visualization Technique

## An Example of Visualization

We are familiar with maps (or atlases or charts).
A map represents continents, countries and the like as two-dimensional figures.

Recall that a continent, or a country, has a three-dimensional topography.
For example, in the US, the Rocky Mountains are very high, and the Grand Canyon very deep.
That should convince you that the US (or for that matter any country) is a three-dimensional geometrical figure.
But on a map, the US (or any country) is a two-dimensional gemetrical figure.

That is a good example of visualization.
Visualization means depicting a geometrical figure that is not two-dimensional as two-dimensional,
then drawing this two-dimensional depiction on paper, or on a computer screen.

## The Visualization Problem in the Context of a .csv File

We are given a .csv file, such as this one:

    1    2    3    4
    3    2    1    5
    6    0    1    4
    7    8    9    6
    5    6    4    9
    
The .csv file above has 4 columns and 5 rows.
The objective of the visualization algorithm is to generate 5x2 = 10 numbers,

    y11    y12
    y21    y22
    y31    y32
    y41    y42
    y51    y52

such that:

    the pair (y11, y12) is in some sense a representative (or proxy) for the 1st row of the .csv file
    the pair (y21, y22) is in some sense a representative (or proxy) for the 2nd row of the .csv file
    the pair (y31, y32) is in some sense a representative (or proxy) for the 3rd row of the .csv file
    the pair (y41, y42) is in some sense a representative (or proxy) for the 4th row of the .csv file
    the pair (y51, y52) is in some sense a representative (or proxy) for the 5th row of the .csv file
    
 What do we mean by the phrase "in some sense a representative (or proxy)"?
 Recall that the first row is a point in R^4, (1, 2, 3, 4).
 It is not possible to draw a 4D point.
 Now let us turn to the pair (y11, y12), which is described as being a representative (or proxy).
 (y11, y12) is a point in R^2.
 We can certainly mark a point (y11, y12) in R^2, provided, of course, our algorithm has computed the
 values of y11 and y12.
 For example, if our algorithm has computed that y11 = 2.5, y12 = 2.7, we can mark the point (2.5, 2.7)
 on a sheet of graph paper.
 (A sheet of graph paper is R^2!)
 We can say that (2.5, 2.7) is a representative (or proxy) of the 4D point (1, 2, 3, 4).
 Or we depict the 4D point (1, 2, 3, 4) as the 2D point (2.5, 2.7).
 
 Recall that in the previous section we discussed that maps (or atlases or charts) are good examples of
 visualization.
 We can construct an analogy:
 The 4D point (1, 2, 3, 4) is similar to, say, a section of the Rocky Mountain.
 The 2D point (2.5, 3.5) is similar to depiction, on a map, of that section of the Rocky Mountain.
 
## Abstract Statement of the Visualization Problem

Let our .csv file house m points in R^n,

    x1, x2, x3, ..., xm
    
The quantities m and n are given positive integers.
We can expect n to be large.

The visualization algorithm needs to compute m points in R^2,

    y1, y2, y3, ..., ym

Our intention is that a computer package will depict the points

    y1, y2, y3, ..., ym
    
on a computer screen; we will consider

    y1 to be the depiction of x1
    y2 to be the depiction of x2
    y3 to be the depiction of x3
    ............................
    ............................
    ym to be the depiction of xm
    
## Desired Trade-off in Our Visualization Algorithm

Consider the following sentences:

    Sentence 1 : x2 is close to x1, and x3 is even more close
    
    Sentence 2 : x12 is far from x11, and x13 is even more far

Ideally, our visualization algorithm should compute the y's such that the following sentences are correct:

    Sentence 3 : y2 is close to y1, and y3 is even more close (Please see Sentence 1)
    
    Sentence 4 : y12 is far from y11, and y13 is even more far (Please see Sentence 2)
    
Experience suggests that visualization algorithms find it hard to make both Sentences 3 and 4 correct.
There seems to be a trade-off: a visualization algorithm can compute the y's such that Sentence 3 is
correct, but Sentence 4 is (in general) not correct.
In the alternative, a visualization algorithm can compute the y's such that Sentence 4 is correct, but
Sentence 3 is (in general) not correct.
Computing the y's such that both Sentences 3 and 4 are correct seems to be too hard a thing to do.

tSNE picks the former.
That is to say, tSNE depicts the relationship of "is close to" with a fair amount of fidelty.
tSNE does not (in general) depict the relationship of "is far from" with fidelity.

## tSNE is Similar to a Map

Let us look at the US as a 3D geometrical figure.
In this 3D geometrical figure, the 48 states are clustered together.
Next, let us look at a map of the US; in that map, the US is depicted as a 2D figure.
In the 2D figure (i.e., in the map), the 48 states are clustered together.
That is to say, the map depicts the relationship of "are clustered together" with fidelity.

Let us sum up the points we have been makinng.
The tSNE algorithm depicts the relationship "is close to" with fidelity;
a map depicts the relationship of "are clustered together" with fidelity.
Now the phrases "is close to" and "are clustered together" are pretty nearly the same thing.
So we see that tSNE behaves somewhat like a map.
