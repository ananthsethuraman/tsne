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

Two positive integers m and n are given.
We can expect n to be large.
A .csv file is given; it houses m points in R^n,

    x1, x2, x3, ..., xm
    
The visualization algorithm needs to compute m points in R^2,

    y1, y2, y3, ..., ym

We expect that a computer package will depict the points

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
That is to say, tSNE depicts the relationship of "is close to" with a considerable amount of fidelty.
tSNE depicts the relationship of "is far from" with only a small amount of fidelity.

## Precaution

In the last paragraph, the phrase "only a small amount of fidelity" needs to be undersood carefully.
Suppose that x12 and x13 are far away from x11.
We would expect y12 and y13 to be far away from y11.
It would be glaring mistake if either y12 or y13 were close to y11.
tSNE will not make that sort of glaring mistake.

Nevertheless, tSNE will lose some fine-level detail concerning x12 and x13.
For example, suppose that distance between x11 and x13 is 10 times the distance between x11 and x12.
tSNE could compute the y's such that the distance between y11 and y13 could be be only 1.5 times
the distance between y11 and y12.

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
We see that tSNE behaves somewhat like a map.

## Bringing Probability into the Picture

In machine learning, it is common practice to restate a problem statement such that concepts
of probability theory can play a role.
We will make the same move now.
That is to say, we will restate the problem statement using phrases like "experiment", "outcome",
"event" and "probability mass function".

First we need to descrbe what our experiments and what our outcomes are going to be.

Let us take any one of the x's, say, x1.
Let us ask the question, "Of the other x's, which is the nearest to x1?"
The possible answers (or candidate answers) are:

    x2 is nearest to x1
    x3 is nearest to x1
    ...................
    xm is nearest to x1
    
We will term the act of asking this question an experiment.
We can even name this experiment as Ex1.
The outcomes of this experiment Ex1 are the the possible answers or candidate answers listed above.

We can make up many more experiments of the same sort.
For example, the following could be an experiment named Ex2:

    _Experiment Ex2, i.e., a question concerning x2_
    
    Let us pick the point x2.  Of the other x's which is nearest to x2?
    
    _Outcomes of Ex2, i.e., possible answers or candidate answers to the question above_
    
    x1
    x3
    x4
    ..
    xm
    
Here is another experiment:

    _Experiment Ey1, i.e., a question concerning y1_
    
    Let us pick the point y1.  Of the other y's which is nearest to y1?
    
    _Outcomes of Ex2, i.e., possible answers or candidate answers to the question above_
    
    y2
    y3
    ..
    ym
 
