---
layout: article
title: Bayes Theorem and ROC
tags: probability Mathematics
aside:
    toc: true
  
---

## Conditional Probability

Is the idea of understanding the probability an event A occurs given an event B. We formally say the **Conditional Probability** of A given B is defined as: 

$$P(A | B ) = \frac{P(A \cap B)}{P(B)}$$

<p>
    <img src="/assets/images/bayes/ConditionalProbability.jpg" alt="Bayes Theorem"/>
    <br>
    <em>Photo Courtesy of 
    <a href="https://www.cut-the-knot.org/Curriculum/Probability/ConditionalProbability.shtml">[“Conditional Probability and Independent Events”]</a>
    </em>
</p>

Pictorially we consider the 3 intersected events in $A \cap B$ in the new sample space $B \subset \Omega = 25 $ as all the only possible outcomes when A occurs given B. We easily see that $\frac{P(A \cap B)}{P(B)} = \frac{3}{25}$.

# Bayes Theorem

Since we know that the conditional probabilities are defined as:

$$P(A | B ) = \frac{P(A \cap B)}{P(B)}$$

and 

$$P(B | A ) = \frac{P(A \cap B)}{P(A)}$$

we can plug the second equation into the first and arrive at **Bayes Theorem**:

$$P(A | B ) = \frac{ P(B | A ) \cdot P(A)}{P(B)}$$

There are alternative forms of Bayes, but first consider this image.
<p>
    <img src="/assets/images/bayes/intersection_AB.png" alt="Intersection of A and B"/>
    <br>
    <em>Photo Courtesy of 
    <a href="https://commons.wikimedia.org/wiki/File:Intersection_of_sets_A_and_B.svg">[“Intersection of sets A and B”]</a>
    </em>
</p>

We can alternatively define a set B as the addition of the $B \cap A$ (purple) and $B \cap A^c$ (orange) elements, or $B = (B \cap A) \cup (B \cap A^c)$. Basically a set B is the portion that intersects with B and the portion that does not intersect with B.

Then we can write Bayes Theorem as:

$$P(A | B ) = \frac{ P(B | A ) \cdot P(A)}{P(B \cap A) + P(B \cap A^c)}$$

Or more compactly if you replace the two terms in the denominator again with bayes theorem. 

i.e. $P(B \cap A) = P(B \mid A) \cdot P(A)$ and 
$P(B \cap A^c) = P(B \mid A^c) \cdot P(A^c)$:

We arrive at the alternate form of **Bayes Theorem**.

$$P(A | B ) = \frac{ P(B | A ) \cdot P(A)}{P(B | A ) \cdot P(A) + P(A^c) \cdot P(B | A^c)}$$

## Binary Classification

When we consider two indicator Random Variables $X \sim Bern(P)$ and $Y \sim Bern(P)$, $X$ pertaining to ground truth observations and $Y$ a model mapping new observations to a set of known memberships (binary memberships in our case) then we can perform the task of **classification**.

If we want to evaluate the performance of our model we first need to define a few terms.

If X is our ground truth and Y is our classifier, then all the possible outcomes of our Random Variables are as follows:

1. $X = \text{False} \cap Y = \text{True}$ **False Positive**. The model inaccurately determined an observation was positively a member of the the class we are interested in.

2. $X = \text{True} \cap Y = \text{False}$ **False Negative**. The model inaccurately determined an observation was not a member of the the class we are interested in.

3. $X = \text{True} \cap Y = \text{True}$ **True Positive**. The model accurately determined a positive membership.

4. $X = \text{False} \cap Y = \text{False}$ **True Negative**. The model accurately determined a negative membership.


**Prevalence** ($\varpi$) is the measure interested in quantifying the probability or percentage of observations belong to the the membership we are interested in.

$$ \varpi = P(X = \text{True})$$

**Sensitivity** ($\eta$) (Recall / True Positive Rate) is the measure of *correctly* classifying an observation to be a member of the class we are interested in. In other words, the Probability of a True Positive occurring out of a positive result.

$$ \eta = P(Y = \text{True} \mid X = \text{True})$$

$$ = \frac{P(Y = \text{True} \cap X = \text{True})}{P(X = \text{True})}$$

$$ \eta = \frac{P(Y = \text{True} \cap X = \text{True})}{\varpi}$$


**Specificity** ($\theta$) (Selectivity / True Negative Rate) is conversely the measure of correctly classifying an observation to *not* be a member of the class we are interested in. The Probability of a True Negative.

$$ \theta = P(Y = \text{False} \mid X = \text{False})$$

$$ = \frac{P(Y = \text{False} \cap X = \text{False})}{P(X = \text{False})}$$

$$ \theta = \frac{P(Y = \text{False} \cap X = \text{False})}{1 - \varpi}$$

**Fall-out** (False Positive Rate) is the probability that a negative sample is accurately classified. 

$$ = P(Y = \text{Positive} \mid X = \text{False})$$

$$ = 1 - P(Y = \text{False} \mid X = \text{False})$$

$$ = 1 - \theta$$



# Reciever Operating Characteristic Curve (ROC)

Is a metric to evaluate the accuracy of a classifier based on the the $\frac{\text{True-Positive Rate}}{\text{False-Positive Rate}}$ $\big( \frac{\eta}{1 - \theta} \big)$ as functions of a parameterized function. 

<p>
    <img src="/assets/images/bayes/roc_curve.png" alt="ROC Curve"/>
    <br>
    <em>Photo Courtesy of 
    <a href="https://www.theanalysisfactor.com/what-is-an-roc-curve/">[“What is an ROC Curve”]</a>
    </em>
</p>

The top left corner of the ROC space corresponds to a perfect classifier. As the curve travels toward the right corner along the green line, you will notice the classifier's tendency to classify things as positive until it always classify a sample as positive. Every point on the green line corresponds to the accuracy of flipping a coin. 



