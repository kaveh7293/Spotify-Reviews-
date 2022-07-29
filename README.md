# Spotify-Reviews-Classification
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
<p> The architecture of the RNN model is shown in the following figure.<br><br>

<img src='https://github.com/kaveh7293/Spotify-Reviews-/blob/main/Screenshot%202022-07-29%20014349.jpg' height='600' width='800'><br>
  
  As shown, I considered the length of all the sentences to be <strong> 30 </strong>. We use padding for the reviewes to make the length of all the reviewes 30. We use a embedding length so that the sequence of the words can be converted to sequences of vectors with a length of 30 (i.e., embedding dimension is 30). We then use LSTM units with 20 elements. One hundred LSTM units whill be used in parallel since the input sequences has a length of 0. As shown, we used bidirectional LSTM to account for the correlation between all the words in a sentence. Next, we use maxpooling units to get the maximum value from each LSTM unit and pass that into a fully-connected layer with <strong>three outputs</strong> with softmax activation functions. </p>
  
<h3> Fitting the Model</h3>
<p> I fitted the model using 15 epochs and a batch size of 120. Also, I also allocated 30 of the data for validation (i.e., I put validation_data=(xtest, ytest)) to see the performance of the fit when the test data is used). The performance of our model can be seen in the following. As shown an accuracy of ~80 was obtained for both training and test datasets. In the next step, since no overfitting is shown, I used the whole dataset to fit the data.</p><br>

<img src='https://github.com/kaveh7293/Spotify-Reviews-/blob/main/download%20(1).png'><br>

<h3> Model Testing</h3>
<p> In this section, the model is tested using several different sentences to check whether the trained model is working properly. In the following table, the sentence that has been used and the corresponding predicted value is shown.<br>
  <table>
  <tr>
    <th>Comment</th>
    <th>Predicted Rating</th>
  </tr>
  <tr>
    <td>absoloutly love the songs, liked the suggestions, love the user-friendly environment</td>
    <td>Good</td>
  
  </tr>
  <tr>
    <td> I hate the app</td>
    <td>Bad</td>
  </tr>
  
  <tr>
    <td> It is an awful app</td>
    <td>Bad</td>
  </tr>
  <tr>
    <td>I absoloutely recommend it to others</td>
    <td>Good</td>
   </tr>
</table>
