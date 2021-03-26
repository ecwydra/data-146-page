# Midterm Corrections

## Question 18

I got this problem wrong because of a rounding issue. I cut off the number of decimal points I returned for the test results and the answer was rounded up to 0.602. I attended office hours and after talking with Professor Frazier I think the way to solve this is to not automate the rounding, but to print the whole value and then leave the rounding up to me. 

## Question 19

Similar problem here as with 18, I got this problem wrong because of a rounding issue. I cut off the number of decimal points I returned for the test results and the answer was rounded up to 0.602. I attended office hours and after talking with Professor Frazier I think the way to solve this is to not automate the rounding, but to print the whole value and then leave the rounding up to me.

## Question 20

Same problem as 18 and 19, I got this problem wrong because of a rounding issue. I cut off the number of decimal points I returned for the test results and the answer was rounded up to 0.602. I attended office hours and after talking with Professor Frazier I think the way to solve this is to not automate the rounding, but to print the whole value and then leave the rounding up to me.

## Question 21

I got this question wrong partly because I didn't understand what data it was asking for, but also because I didn't understand what to return. I thought it was asking for the least correlated feature from problem 15 and 16, and I thought I was supposed to return the r2 value of the model that had the lowest score.

Instead, I was supposed to use the whole standardized dataset, create the three models with the previously found hyperparameters, fit the created models, and return the coefficient for the least correlated feature. 

## Question 22

I got this question wrong almost exactly the way I got question 21 wrong. I didn't understand what data it was asking for or what to return. I thought it was asking for the most correlated feature from problem 15 and 16, and I thought I was supposed to return the r2 value of the model that had the lowest score.

Instead, I was supposed to use the whole standardized dataset, create the three models with the previously found hyperparameters, fit the created models, and return the coefficient for the most correlated feature. 

## Question 24

The issue for this answer is near identical to the issue for 18, 19, and 20. I entered the answer as 0.002, because of the automated rounding: `print('Optimal alpha value: ' + format(a_range[idx], '.3f'))`. If I had left off the rounding, I would have gotten 0.00186, which is the correct answer.

