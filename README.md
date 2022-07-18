# reddit-post-classification
**Exploring Dataset:**
The Reddit dataset is divided into three categories: training, validation, and testing. The training set is used to train the model, make it learn hidden patterns in the data and fit the parameters to the model, while the validation set is used to provide an unbiased evaluation of a model fitted on the training dataset and provided information that helps for tuning hyperparameters, and the test set is used to provide an unbiased evaluation of a final model fitted on the training dataset. The dataset is divided into three parts to ensure that the classification algorithm can generalise effectively to fresh data after being trained.
There are 1200 reddit posts in the training set, and 400 in each of the validation and test sets. The label to predict is the 'Subreddit' column in the dataset, which contains nine distinct values (PS4, pcgaming, NintendoSwitch, antiMLM, HydroHomies, Coffee, xbox, Soda, tea). Within each dataset (train/validation/test), the number of occurrences in each label is more or less similar, resulting in a balanced train, validation and test dataset. However, when the full dataset is divided into three sets, all of the labels are appeared in three divided sets, but they are not evenly distributed among train/ validation /test dataset leading to the suspicion that the data is biased (unbalanced data set)

![image](https://user-images.githubusercontent.com/92384002/179508600-fc01696b-f7bd-429c-b1ef-b4c7d1b0ebc3.png)

**Classifiers Implemented**<br />
	&nbsp;&nbsp;&nbsp;&nbsp;1.Dummy Classifier with strategy="most_frequent"<br />
	&nbsp;&nbsp;&nbsp;&nbsp;2.Dummy Classifier with strategy="stratified"<br />
	&nbsp;&nbsp;&nbsp;&nbsp;3.Logistic Regression with One-hot vectorization<br />
	&nbsp;&nbsp;&nbsp;&nbsp;4.Logistic Regression with TF-IDF vectorization (default settings)<br />
	&nbsp;&nbsp;&nbsp;&nbsp;5.SVC Classifier with One-hot vectorization (SVM with RBF kernel, default settings)

![image](https://user-images.githubusercontent.com/92384002/179509090-8db04acd-b12f-4a78-a5a2-03cf96989f17.png)

**Creation of Custom Tokenizer**<br />
function name: custom_tokenizer() for converting the text (body of reddit post) into list of words assuming that the better we tokenize the body text, the better the final result will be. <br />
The function custom_tokenizer() removes <br />
	&nbsp;&nbsp;&nbsp;&nbsp;• html elements, URLs, digits from reddit post body <br />
	&nbsp;&nbsp;&nbsp;&nbsp;• emojis. I observed the presence of emoji’s in reddit post body which is not relevant to the problem statement <br />
	&nbsp;&nbsp;&nbsp;&nbsp;• all special characters and punctuators from reddit post body <br />
	&nbsp;&nbsp;&nbsp;&nbsp;• removed stop words and spaces <br />
	&nbsp;&nbsp;&nbsp;&nbsp;• and expanded commonly seen short form of words. For example, isn’t -> is not, can’t -> can not <br />
	&nbsp;&nbsp;&nbsp;&nbsp;• normalise the text by converting all words to lowercase <br />
	&nbsp;&nbsp;&nbsp;&nbsp;• tokenize/split the body text into list of tokens/words <br />
	&nbsp;&nbsp;&nbsp;&nbsp;• applied lemmatization on tokens (eg., dancing -> dance)<br />

**Feature Engineering**<br />
&nbsp;&nbsp;&nbsp;&nbsp;Below features are selected to add to the tuned model.<br />
	&nbsp;&nbsp;&nbsp;&nbsp;• **Added other properties of reddit posts** <br /> ‘Title’ has been added as an additional feature. In a normal context, title of a reddit post shows a very brief description of the subreddit. It will be shown in the tab's text, as well as in Reddit and Google search results. As a result, if we add title as a new feature, there may be a significant increase in classifier performance. <br />
	<br />
	&nbsp;&nbsp;&nbsp;&nbsp;• **Word embedding using Gensim word2vec** <br />
word2vec is used for word embedding. Reddit post ‘title’ has been passed to gensim function created. Since it is capable of capturing word similarity using vector arithmetic, it may improve model performance. Also size of generated vector is small and flexible. gensim.utils.simple_preprocess is used for text preprocessing and tokenization.
