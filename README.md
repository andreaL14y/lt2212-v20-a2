# LT2212 V20 Assignment 2

PART 1: 
The function EXTRACT_FEATURES creates a numpy array where one element/vector represents one article and the entries denote the amount of a certain word contained in this article. I.e. there is one row per article and one column per word.

There are several helper functions implemented: 
	1. get_words: creates a list of all words of an article. All words are considered in lowercase, by the '\w+' it's guaranteed that one gets only letters or numbers, by the filtering isalpha() strings are kept, that consists only of alphabetic characters, furthermore only strings with length at least 4 are kept (as shorter words usually don't contain any significant content).
	2. get_all_words: puts all words of all sample articles into a list (with repetitions)
	3. get_word_counts: counts the occurance of a word in a list and is used to determine the total occurance of each word in all articles
	4. selected_words_count: takes a list of words and a reference list and counts only the elements that occur also in the reference list, it is needed to get the word_counts after filtering out infrequent words
	5. del_infrequent_words: deletes all words that occur in total less than 20 times. 

PART 2:
REDUCE_DIM is a function to squeeze the dimension of the numpy array down to a given dimension n. It will return a numpy array of the shape (X.shape[0], n), where X is the original array. 
Here the principal components analysis (PCA) is used.

PART 3: 
First there are two classifiers chosen with predifined default-values: 
	1. (id 1) NAIVE BAYES/GAUSSIAN NB 
	(brings into account Bayes' Thm about probabilities which says that the probability of an event A given circumstances B equals the probability of event B given circumstances A multiplied by the probability of A itself(in total) and devided by the (total) probability of B i.e. P(A|B)=P(B|A)*P(A)/P(B).)	
	
	2. (id 2) SVC 
	(a support vector classifier, which draws support vectors (lines) between the points of different classes and tries to maximize their distance)

In SHUFFLE SPLIT the given data is divided in 80% train-part (each testdata and test-labels) and 20% testpart. I used a predefined scikit-learn function to do this but gave also an self-written alternative (which is commented out)
Later the classifier is trained and evaluated in the functions TRAIN_CLASSIFIER (you got a typo here but I did not dare to change) and EVALUATE_CLASSIFIER respectively. To print the accuracy, precision, recall, and F-measure simply the classification report is printed, which includes all desired parameters in the weighted avg (W-AVG: prcision - recall - f1-score). 

PART 4: 
Classifier 1 -> NAIVE BAYES/GAUSSIAN NB
	1. Unreduced array from PART 1:
		Accuracy: 0.99		W-AVG: 0.99 0.99 0.99
	2. Reduced array to 50%
		Accuracy: 0.29		W-AVG: 0.48 0.29 0.27
	3. Reduced array to 25%
		Accuracy: 0.28		W-AVG: 0.48 0.28 0.28
	4. Reduced array to 10%
		Accuracy: 0.21		W-AVG: 0.48 0.21 0.22
	5. Reduced array to 5%
		Accuracy: 0.19		W-AVG: 0.48 0.19 0.18

Classifier 2 -> SVC
	1. Unreduced array from PART 1:
		Accuracy: 0.82		W-AVG: 0.84 0.82 0.81
	2. Reduced array to 50%
		Accuracy: 0.77		W-AVG: 0.82 0.77 0.75
	3. Reduced array to 25%
		Accuracy: 0.77		W-AVG: 0.80 0.77 0.75
	4. Reduced array to 10%
		Accuracy: 0.73		W-AVG: 0.78 0.73 0.72
	5. Reduced array to 5%
		Accuracy: 0.72		W-AVG: 0.76 0.72 0.70

Discussion: The reduction of dimensionality gets faster the less dimensions one will get. In the results there is a big difference between the two different classifiers: While #1 is almost 100% correct with the full data, it gets very bad (around 30%) as soon as one reduces the dimensions. However it doesn't really seem to matter if one uses 50% of the original data or only 5% as the difference is not very big. 
The values of clf #2 is worse if one uses the full dataframe, however it stays very good using the reduced arrays and is even with a dataframe of only 5% of the original array better than clf #1 with 50%. 
Furthermore it should be mentioned that the training of clf #2 lasted much longer than the training of clf #1. 
		


BONUS PART: 
In a second upload TruncatedSVD is used in PART 2 to reduce the dimensions. It lead to the following values:
Classifier 1 -> NAIVE BAYES/GAUSSIAN NB
	1. Unreduced array from PART 1:
		Accuracy: 0.99		W-AVG: 0.99 0.99 0.99
	2. Reduced array to 50%
		Accuracy: 0.26		W-AVG: 0.50 0.26 0.24
	3. Reduced array to 25%
		Accuracy: 0.24		W-AVG: 0.51 0.24 0.24
	4. Reduced array to 10%
		Accuracy: 0.22		W-AVG: 0.51 0.22 0.22
	5. Reduced array to 5%
		Accuracy: 0.21 		W-AVG: 0.52 0.21 0.20

Classifier 2 -> SVC
	1. Unreduced array from PART 1:
		Accuracy: 0.80		W-AVG: 0.83 0.80 0.79
	2. Reduced array to 50%
		Accuracy: 0.79		W-AVG: 0.83 0.79 0.78
	3. Reduced array to 25%
		Accuracy: 0.78		W-AVG: 0.81 0.78 0.76
	4. Reduced array to 10%
		Accuracy: 0.73		W-AVG: 0.78 0.73 0.71
	5. Reduced array to 5%
		Accuracy: 0.70		W-AVG: 0.74 0.70 0.68

Discussion: (Compared to the 1st file using PCA):
CLF #1 accuracy, recall and f1 score are slightly worse, precicion a bit better, the differences are not big at all. 
CLF #2: values of 100% of the data, 10% and 5% are slightly worse, values of 50% and 25% are a little better.
In both cases the difference is not big at all and could be due to some randomization. 
		
		
