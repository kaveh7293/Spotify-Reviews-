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
  <li> An embedding matrix is constructed based on the tocknized values of the words and using already trained embedding matrix downloaded from <a href='https://nlp.stanford.edu/projects/glove/'> here. </a> To do so, the row number in the embedding matrix corresponds to the index of the word based on their tockenized values.</li>
  <li> The embedded matrix is used in the embeddding layer and set trainable option to false so that no embedding is implemented.</li>
  <li> Fifty bidirectional LSTM units are added next to the embedding layer and a dropout layer is also added to prevent overfitting. </li>
  <li> A global maxpooling layer is added afterwards so that the results from all LSTM units become equally important (i.e., by doing so we further improve the long term memory of our neural network).</li>
  <li> The results of the global maxpooling layer is connected to a dense layer with 3 softmax units</li>
  <li> The model is compiled and the model is trained based on training data.</li>
 </ol>
<h3> Model Description </h3>
<p> The architecture of the RNN model is shown in the following figure.

<img src='https://github.com/kaveh7293/Spotify-Reviews-/blob/main/Screenshot%202022-07-29%20014349.jpg'>

</p>
