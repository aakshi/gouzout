---
layout: post
title: Automated text analysis to discover authors gender
date: '2010-07-27 12:39:14'
---

The other day I ran an experiment which involved developing a web application which assessed text and attempted to predict the gender of the author of the text. The application uses a machine learning text classifer which means the system had to be trained to recognise male/female text. The system was trained with a corpus of over 10000 text entries split 50/50 male/female.

Once the system had been trained it’s predictive power was tested against the text produced by 400 participants. The text produced by each participant was at least 200 characters in length and was classified by the application. The application makes a percentage guess of the gender of the texts author. For example the application says the text analysed a 60% chance of having a male author and 40% chance of having a female author.

Once the application had made it’s predictions the result were checked back to the gender of the participants to assess the validity of the predictions. The results were as follows:

N.B. Tolerance the classifier outputs its guesses as a percentage of certainty. The certainty has to be above the tolerance level to be deemed “classified”. If the certainty is under the tolerance level the classifier isn’t sure enough for the text to be considered classified.

<table>
<tr>
<th></th>
<th>Classified %</th>
<th>Unclassified %</th>
<th>Total %</th>
</tr>
<tr>
<td>Classified to gender (Tolerance set at 65% (n = 400))</td>
<td>64</td>
<td>36</td>
<td>100</td>
</tr>
</table>
<table>
<tr>
<th></th>
<th>Correct %</th>
<th>Incorrect %</th>
<th>Total %</th>
</tr>
<tr>
<td>Classified gender correctly (Tolerance set at 65% (n = 256))</td>
<td>66</td>
<td>33</td>
<td>100</td>
</tr>
</table>

The results show that at the set tolerance level the app was able to classify two thirds of participants and of the two thirds it classified the classification was correct 2 times out of 3. It shows that the classifier works significantly better than chance. Also the percentage correct matched the set tolerance which shows that when the classifier says for example that passage has a 67% chance of being written by a female, 67% is a valid figure.

This is just the beginning and we can expect lots more of this sort of approach in the future. There are also a couple of things to consider.

I’m assuming the gender data submitted by the participants is accurate, which it may not be (after all how valid are survey responses?) - The application was trained on blog posts (because I did not have enough first hand participants available). So there may be a difference between the text submitted and posts on a blog which will make the system less accurate. - This was a quick experiment, my first step into this area, I’m confident with a bit tweaking and a bit more knowledge the application could be made more accurate.

Hopefully this has sparked off a few ideas, if you can think of a good application for automated text classification let me know? It would be great if we could build something really useful out of this. 