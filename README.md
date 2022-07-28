# Spotify-Reviews
<h3> Spotify Reviews Dataset </h3><br>
<p> In this problem, we use the spotify dataset to obtain the the corresponding ratings for the comments given by the users. The dataset from kaggle website can be obtained from <a href='https://www.kaggle.com/datasets/mfaaris/spotify-app-reviews-2022'>here</a>. We assign the ratings 4 and 5 as the good review, 3 as the neutral review and one and two as bad reviews. Our goal is to predict the reviews based on the comments that are given. </p>
<h3> Steps</h3>
<ol> The following steps were used to train a RNN with LSTM:
  <li>Preprocessing of the data were implemented wherein:
    <ul><li>All the uppercase letters were converted into  lowercase letters</li>
      <li>The short forms are converted into the formal forms (e.g., i'm to i am)</li> 
      <li>Special characters such as @ and # are removed from the text</li> 
      <li>Stop words are removed</li>
      <li>Lemmatisation is done to use the root of the words (e.g., convert provided to provide). Note that lemmatisation is more powerful than stemming where the resulting outcome are usually meaningless (e.g., convert provided to provid).</li>
    </ul>
   <li> A tockenizer is used to convert the texts into the numbers and assign a unique number to each distinct word. Padding is done in the next step in order to convert the sequences with different lengths into the same size by putting additional zeros at the start of the sequence with shorter lengths than the maximum sequnce length.</li>
  <li> An embedding matrix is constructed based on the tocknized values of the words and using already trained embedding matrix downloaded from <a href='https://nlp.stanford.edu/projects/glove/'> here </a>.</li>
