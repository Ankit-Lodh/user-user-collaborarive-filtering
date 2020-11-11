# user-user-collaborarive-filtering and item-item-collaborative-filtering

### Part 1 - Without Normalization
First, you will implement user-user collaborative filtering without normalization.

1. Start by downloading the starting spreadsheet. This is a 25 user x 100 movie matrix of ratings selected from the class data set. The spreadsheet has three sheets in it (this is not supposed to be an exercise in spreadsheet tricks; as a result, we’ve already given you a significant start). 1) The first sheet is a ratings matrix with movies as rows and users as columns, 2) The second sheet is a ratings matrix with movies as columns and users as rows, and 3) The third sheet is the start of your correlations matrix.

2. Open the sample matrix in your favorite spreadsheet program. Note that the matrix contains a significant number of missing values -- do not replace these with zeroes, they are correctly missing.

3. Complete the user-by-user correlations matrix. To check your math, note that the correlation between users 1648 and 5136 is 0.40298, and the correlation between users 918 and 2824 is -0.31706. All correlations should be between -1 and 1, and the diagonal should be all 1's (since they are self-correlations).
Identify the top 5 neighbors (the users with the 5 largest, positive correlations) for users 3867 and 89. For example, if the target user were #3712, the closest neighbors are 2824 (corr: 0.46291), 3867 (corr: 0.400275), 5062 (corr: 0.247693), 442 (corr: 0.22713), and 3853 (corr: 0.19366). Don't forget to exclude the target user (corr: 1.0) from your possible selections.

4. The formal formula for correlation-weighted average is

![image](https://user-images.githubusercontent.com/67375613/98549821-5250ed80-22c1-11eb-82b9-790dd54ad03f.png)

 . Remember, you will need to make sure that your weight for each contributed rating is the user-user correlation when that neighbor has rated the movie, but 0 when the neighbor has not rated the movie).
 
5. Indeed, you should look to see what the user’s rating (if any) is for the top-recommended movies. For example, if the user ID was 3712, the correct submission would be:
Top Movie: 641 Prediction: 5.000

2nd Movie: 603 Prediction: 4.856

3rd Movie: 105 Prediction: 4.739

And if the user ID were 3525, there would be a three-way tie among:

Movies: 238, 194, and 38 (all with a prediction of 5.000)

A few tips we hope you’ll find helpful:

Your calculations will be easier if you use some of the built-in functions that spreadsheets have to help. These include SUMPRODUCT (which computes dot-products) and SUMIF (which can be used to compute the total weight). It is also helpful to understand two special paste functions: paste values (which copies cell values without copying the underlying formulas) and paste transpose (which can help re-orient your data).
Your intermediate goal should be to have a sheet for each target user with a user-by-rating table and a set of user weights (for the top-five neighbors) to allow you to compute all 100 predictions for the target user.
Once you have all the predictions, you can always copy them (copy the values) and sort them to find the top three results.
Don’t worry about values that result in division by zero -- those are cases where no neighbors rated the movie.

### Part 2 - Normalization
Next, you will repeat the computation but this time you will normalize the scores.

Repeat step 5 from part 1. This time, however, use the normalization formula:

![image](https://user-images.githubusercontent.com/67375613/98549452-cf2f9780-22c0-11eb-96b2-b316ba8fa1af.png)

 
6. Remember, you do not need to re-compute the correlations, just use the existing correlations but normalize the ratings being averaged by subtracting each neighbor’s mean rating from each of their ratings (and add the target user’s mean back into the total).
For example, if the user ID was 3712, the correct submission would be:

Top Movie: 641 Prediction: 5.900

2nd Movie: 603 Prediction: 5.546

3rd Movie: 105 Prediction: 5.501

Note that it is possible to have movie predictions outside the five-star scale; in this case this is because 3712 rates movies very high to begin with, and his/her neighbors have wider ranges (and think these movies are very high in those ranges).

Also, these top movie predictions are interesting in other ways. The top movie was only rated by one neighbor, but was so highly rated (1.4 above mean) that it stands out.

And if the user ID were 3525, the top three would be:

Top Movie: 238 Prediction: 4.760

2nd Movie: 424 Prediction: 4.663

3rd Movie: 134 Prediction: 4.585

Note how only one of these three is the same as from the top three without normalization! And notice that the (perhaps surprisingly) strong prediction for 134 is again the result of having just a single neighbor’s rating (and that being a neighbor who really liked the movie).


# item item based collaborative filtering
This will explore item-based collaborative filtering. As with the Module 2 Assignment, you will be given a 20x20 matrix where columns represent movies, rows represent users, and each cell represents a user-movie rating.

Assignment 5.xls
Assignment 5.xlsx
Assignment 5.ods
Spreadsheet Layout
In the spreadsheet, you will find 4 sheets: Ratings contains the raw rating data, and NormRatings contains the normalized ratings (each rating adjusted with the user’s mean rating). You will fill out Matrix with the similarities between all items, and FilterMatrix is a filtered view of Matrix where all negative similarities are clamped to 0 (to exclude negative similarities from the computation).

The Ratings and NormRatings sheets also contain the L2 norm (Euclidean length, or square root of sum of squares) of each movie’s ratings.

For each similarity variant, you will fill out the Matrix sheet; use the FilterMatrix sheet to compute recommendations.

Similarity Functions
Your core task in this assignment is to compute item similarities using 2 different similarity functions:

Cosine similarity between items using raw (unnormalized) ratings.

Cosine similarity using adjusted (normalized) ratings.

For the numerator of the similarity, you will probably want to use the SUMPRODUCT function; the provided L2 norms will be useful for computing the denominators.

Deliverables

The output you are supposed to turn in consists of 2 parts. For each part, submit both unnormalized and normalized results.

Top 5 Toy Story

Provide 5 movies most similar to Toy Story, in decreasing order of similarity. Only provide the movie ID, not the title.

Top 5 for User 5277
Provide the top 5 recommended movies for user 5277, using an average of the user’s ratings weighted by similarity to each candidate movie. You do not need to exclude movies they have rated. Consider all movies with nonnegative similarities (do not limit neighborhood size).

Examples
Here are some values to check your calculations:

Similarity between Toy Story and Star Wars, raw: 0.645

Similarity between Toy Story and Star Wars, normalized: -0.378
