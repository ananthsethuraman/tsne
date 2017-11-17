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
In particular, letting probability play a role will allow us to transform a problem into an
optimization problem with cross-entropy as an objective function.

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
 
## An Idea for a Probability Mass Distribution

Thus far we have described experiments named

    Ex1, Ex2, Ex3, ..., Exm
    Ey1, Ey2, Ey3, ..., Eym
    
We have also described the outcomes of each of these experiment.
But we have not spoken of a probability mass distribution yet.
Let us turn to that.

As an example, take the experiment Ex1.
In Ex1, the question is "What is x that is closest to x1?"
And the possible outcomes are x2, x3, x4, ..., xm.
So far, so good.

Let us use the following notation:

    || x2 - x1 || = distance between x2 and x1
    || x3 - x1 || = distance between x2 and x1
    || x4 - x1 || = distance between x2 and x1
    ..........................................
    || xm - x1 || = distance between x2 and x1
    
Could these distances be quoted as the probability mass distribution?
That is to say, is it valid to quote that:

    probability that Ex1's outcome is x2 = || x2 - x1 ||
    probability that Ex1's outcome is x3 = || x3 - x1 ||
    probability that Ex1's outcome is x4 = || x4 - x1 ||
    ....................................................
    probability that Ex1's outcome is xm = || xm - x1 ||
    
## Objections to the Foreging Idea

There are three objections to the foregoing idea for a probability mass distribution.

First, a probability must be a number between 0 and 1; there is no assurance that distances like

    ||x2 - x1||, ||x3 - x1||, ||x4 - x1||, ..., ||xm - x1||
    
are numbers between 0 and 1.  They could easily greater than 1.

Second, the sum of all the probabilities in a probability mass distribution is 1; there is no
assurance that the sum

    ||x2 - x1|| + ||x3 - x1|| + ||x4 - x1|| + ... + ||xm - x1|| = 1
    
Third, the distances

    ||x2 - x1||, ||x3 - x1||, ||x4 - x1||, ..., ||xm - x1||
    
are not normalized.  In one application, the x's may have the interpretation of being lengths in
inches; in another application, the x's may have the interpretation of being weights in pounds;
in yet another application, the x's may have the interpretation of being money in USD; and so on.

## How to Normalize

We will deal with the third objection first.

We will introduce a parameter sigma1.
This sigma1 will be a length in inches, if the x's are lengths in inches; sigma1 will be a
weight in pounds, if the x's are weights in pounds; sigma1 will be money in USD, if the x's are
money in USD; and so on.
Therefore the quantities

    ||x2 - x1||, ||x3 - x1||, ||x4 - x1||, ..., ||xm - x1||
    -----------  -----------  -----------       -----------
       sigma1       sigma1       sigma1            sigma1
       
will be non-dimensional.
Still, there is a problem.
What is the actual numerical value of sigma1 going to be?
Further, who is responsible for computing sigma1--the user or the tSNE algorithm?

In fact, it is the tSNE algorithm that computes sigma1.
The way it computes sigma1 is somewhat heuristic in nature.
The value of sigma1 is chosen such that some 7-50 of the distances

    ||x2 - x1||, ||x3 - x1||, ||x4 - x1||, ..., ||xm - x1||
    
are comparable or smaller than sigma1.
The intuition is that if || xi - x1 || is a good bit greater than sigma1, then
xi has a poor probability of being picked as the outcome of the experiment Ex1, i.e.,
xi has a poor probability of being picked as the x that is closest to x1.

The previous paragraph contained the sentence

    "The value of sigma1 is chosen such that some 7-50 of the distances ..."
    
This raises a question.  Should it be 7?  Or 50?  Or some number between 7 and 50, e.g., 28?

The author of tSNE says that the visualization generated is about the same whether it is 7,
or 50 or 28.

On the other hand, a paper by Cao and Wang suggest that it does matter, and further, their
paper offers an automatic way of picking whether it should be 7, 50, 28, 64, 128 or some other
number.

Whatever the number that is picked--be it 7, 50, 28, 64, 128 or some other number--that number
is termed the perplexity.
Perplexity is termed a tunable parameter, or a knob or a hyperparameter.

## Softmax Function

We can now deal with the first and second objections.
To this end, we use the softmax function.
With the softmax function we can write the probablity mass distribution of the
experiment Ex1 in this way:

    probability that Ex1's outcome is x2 = softmax ( || x2 - x1 || / sigma1 )
    probability that Ex1's outcome is x3 = softmax ( || x3 - x1 || / sigma1 )
    probability that Ex1's outcome is x4 = softmax ( || x4 - x1 || / sigma1 )
    .........................................................................
    probability that Ex1's outcome is xm = softmax ( || xm - x1 || / sigma1 )
    
 In the same way, the probability mass distribution of the experiment Ex2 would be:

    probability that Ex2's outcome is x1 = softmax ( || x1 - x2 || / sigma2 )
    probability that Ex2's outcome is x3 = softmax ( || x3 - x2 || / sigma2 )
    probability that Ex2's outcome is x4 = softmax ( || x4 - x2 || / sigma2 )
    .........................................................................
    probability that Ex2's outcome is xm = softmax ( || xm - x2 || / sigma2 )
    
 In the same way, the probability mass distribution of the experiment Exm would be:

    probability that Exm's outcome is x1 = softmax ( || x1 - xm || / sigmam )
    probability that Exm's outcome is x2 = softmax ( || x2 - xm || / sigmam )
    probability that Exm's outcome is x3 = softmax ( || x3 - xm || / sigmam )
    .........................................................................
    probability that Exm's outcome is x{m-1} = softmax ( || x_{m-1} - xm || / sigmam )
    
## Older Proposal for Probability Mass Distribution of Ey1, Ey2, ... Eym

Recall that the parameters sigma1, sigma2, sigma3, ..., sigmam serve to normalize the distances between the x's.
In the same way, we should introduce additional parameters tau1, tau2, tau3, ..., taum in order to normailize the distances between the y's.
On this ground, then, the probability mass distribution of the experiment Ey1 would be:

    probability that Ey1's outcome is y2 = softmax ( || y2 - y1 || / tau1 )
    probability that Ey1's outcome is y3 = softmax ( || y3 - y1 || / tau1 )
    probability that Ey1's outcome is y4 = softmax ( || y4 - y1 || / tau1 )
    .........................................................................
    probability that Ey1's outcome is ym = softmax ( || ym - y1 || / tau1 )
    
In reality this is an older proposal.
We will retain it because it is helpful in teaching.
After a bit we will replace it with a more modern proposal.

Now recall that the parameter sigma1 was determined by a concept named perplexity.
That is to say, tSNE would determine sigma1 such that the number of x's that are close to x1 would be 7-50.
Does tSNE have something similar in order to determine tau1?
It turns out that nothing this complicated is necessary?
Rather, tSNE can set tau1 to 1 by fiat.
Furthermore, it can compute the y' such that the distances between the y's are on the order of 1.
This is because a visualization algorithm is invariant to scaling in the following sense:
Consider the following three sets:

    A = { y1, y2, y3, ..., ym}
    B = { 10y1, 10y2, 10y3, ..., 10ym}
    C = { 100y1, 100y2, 100y3, ..., 100ym}
    
Let a software package depict A on one computer screen, depict B on a second computer screen and depict C on a third computer screen.
The pictures on the three computer screens will look the same, apart from scaling.
That is to say, B will look like A, magnified by a factor 10.
C will also look A, magnified by a factor 100.

This is the reason tau1 can be set a priori to 1.
Similarly, tau2, tau3, tau4, ..., taum can all be set a priori to 1.

## The Unknowns

At this point, we can say that the unknown variables are:

    y1, y2, y3, ..., ym
    sigma1, sigma2, sigma3, ..., sigmam
    
The aim of the tSNE algorithm are to determine the unknowns.
To this end, tSNE frames the computation as an optimization problem:

    Make the probability mass function of Ey1 close to the probability mass function of Ex1--the closer the better
    Make the probability mass function of Ey2 close to the probability mass function of Ex2--the closer the better
    Make the probability mass function of Ey3 close to the probability mass function of Ex3--the closer the better
    ..............................................................................................................
    Make the probability mass function of Ey4 close to the probability mass function of Exm--the closer the better
    
Now, there is a standard way of reckoning the difference between two sets probability mass distributions, namely, the
Kullback-Leibler divergence.
To use the Kullback-Leibler divergence, we need two subscripts.
One subscript, i, will run over the experiments.
The other subscript, j, will run over probabilities.
For example let i = 2 and j = 4.
Because i = 2, we will go to the pair of experiments Ex2 and Ey2.
Because j = 4, we will go to the following two probabilities:

    In Experiment Ex2, go the outcome x4; its probability is softmax ( || x4 - x2 || / sigma2 )
    In Experiment Ey2, go the outcome y4; its probability is softmax ( || y4 - y2 || / tau2 )
    
We are using the older proposal for the probability mass distributions of Ey1, Ey2, Ey3, ..., Eym here.

We generate the following expression:

    softmax ( || x4 - x2 || / sigma2 ) ln { softmax ( || y4 - y2 || / tau2 ) / softmax ( || x4 - x2 || / sigma2 ) }
    
This is one term of the Kullback-Leibler divergence.
The other terms of the Kullback-Leibler divergence are generated by making i run over all the pairs of experiments (Ex1, Ey1), (Ex2, Ey2), (Ex3, Ey3), ...., (Exm, Eym); further, nested inside i, we allow j to run over all the outcomes of the pair of experiements (Exi, Eyi).
Then we add all the terms.

## Newer Proposal for Probability Mass Distribution of Ey1, Ey2, ... Eym

Recall that that the older proposal has probabilities like these for Ey1:

    probability that Ey1's outcome is y2 = softmax ( || y2 - y1 || / tau1 )
    probability that Ey1's outcome is y3 = softmax ( || y3 - y1 || / tau1 )
    probability that Ey1's outcome is y4 = softmax ( || y4 - y1 || / tau1 )
    .........................................................................
    probability that Ey1's outcome is ym = softmax ( || ym - y1 || / tau1 )
    
The newer proposal has probabilities like these for Ey1:

    probability that Ey1's outcome is y2 = 1 / {1 + ( || y2 - y1 || / tau1 ) }
    probability that Ey1's outcome is y3 = 1 / {1 + ( || y3 - y1 || / tau1 ) }
    probability that Ey1's outcome is y4 = 1 / {1 + ( || y4 - y1 || / tau1 ) }
    ..........................................................................
    probability that Ey1's outcome is ym = 1 / {1 + ( || ym - y1 || / tau1 ) }
    
The new proposal is a Cauchy distribution or a Student t distribution with one degree of freedom.

## Why Do We Want This Newer Proposal?

In this section, we will temporarily forget our notation, and use a new notation: x, y and z will
be real variables.
The new notation is in accord with textbooks of analytical (or coordinate) geometry.

Consider these two circles in R^2:

    Circle C1: x^2 + y^2 = 0.50^2
    Circle C2: x^2 + y^2 = 1.00^2

Also consider these two spheres in R^3:

    Sphere S1: x^2 + y^2 + z^2 = 0.50^2
    Sphere S2: x^2 + y^2 + z^2 = 1.00^2

The area of the circle C1 is (pi)(0.50)^2 = 0.25pi
The area of the circle C2 is (pi)(1.00)^2 = 1.00pi

Now

    0.25pi
    ------ x 100 = 25%
    1.00pi
    
That is to say, C2's inner half contributes 25% to the area.
C2's outer half contributes the remaining 75%.

Let's make a similar calculation for the spheres in R^3.
The analog of the circle C1 would be the sphere S1.
The analog of the circle C2 would be the sphere S2.

The volume of S1 is (4/3)(pi)(0.50)^3 = (4/3)(pi)(0.125)
The volume of S2 is (4/3)(pi)(1.00)^3 = (4/3)(pi)(1.000)

Now

    (4/3)(pi)(0.125)
    ---------------- x 100 = 12.5%
    (4/3)(pi)(1.000)
    
That is to say, S2's inner half contributes 12.5% to the volme.
S2's outer half must contribute the remaining 87.5%.

Now 75% < 87.5%.
That is to say, C2's outer half contributes less to C2 than the S2's outer half contributes to S2.
Or C2's outer half is less roomy than S2's outer half.

The rule is that the lower the space's dimension, the less roomy is the outer half.
It is for this reason the authors of tSNE decided not to stick with the older proposal.
