
# Reuniting Pets and Owners Using Machine Learning:

## Module 3 Project:

The purpose of this project is to examine data from one of Austin's largest animal shelters and build a machine learning model to predict outcomes of animals as they come in and are processed in the system.  An efficient and intelligent model can help "manage the inventory" of the shelter and get animals adopted more quickly or returned to their owners more quickly when applicable.  <br><br>
The different outcomes from this shelter are listed below:
- Transfer           
- Adoption           
- Euthanasia        
- Return to Owner     
- Died                 
- Rto-Adopt
- Missing
- Disposal  <br>

With an effective model, we can predict animals outcomes as they enter the shelter, and with that knowledge, run the shelter more efficiently leading to happier animals and shelter employees!

Stakeholders: The stakeholders for this project are both the Austin Animal Center and shelters everywhere. The employees of this shelter could benefit from an algorithm that would tell them with reasonable certainty which animals have owners actively searching for them.  With that knowledge, these pets can get out of the shelter much more quickly.<br><br>

Aside from the regular cleaning, I made one major adjustment to the data.  I removed all outcomes aside from Return to Owner (RTO), Transfer, and Adoption.  The reason is simply that I will not create a model that will recommend euthanasia.  This is a no-kill shelter (except when the animal is badly sick), and even if it were a shelter that euthanizes animals, it would be morally wrong to build a model that would suggest killing animals for innocuous features. <br><br>

Here is a quick look at the top three outcomes over time for both dogs and cats:
![Imgur](https://i.imgur.com/QjqDNdk.png)

These heatmaps can also give you an idea of the different intake conditions and how they can relate to outcome:
![Imgur](https://i.imgur.com/D8sSNbU.png)<br>
![Imgur](https://i.imgur.com/YhZCshO.png)

## Objectives:

Goal: Maximum recall when it comes to the 'return to owner' outcome. We want to be certain that we are giving maximum exposure to pets that need to be returned to their families. At the same time, though, we need to give exposure to animals that are likely to be adopted as well.  Maximum recall for RTO cannot be our only objective, though.  We need accuracy throughout the entire model to make sure we aren't biased towards one outcome or another.

Success Criteria: 
- Easy to understand/use machine learning model
- Easy to implement algorithm
- High recall when it comes to pets that can be returned to families
- High recall for pets that are adopted
- High accuracy for the model as a whole

## Data:

Data Source: https://www.kaggle.com/aaronschlegel/austin-animal-center-shelter-intakes-and-outcomes?select=aac_intakes_outcomes.csv

The data for this project has been generously provided by the city of Austin in their initiative for open data sources.  The data consists of roughly 80,000 rows where each row displays a different outcome of a given animal in a shelter.  For example, a row might have the data for a month old kitten, domestic short hair breed, that was taken in off the street in an injured condition and adopted a month later.  Each line tells the story of a different dog or cat's journey through the shelter.  
<br>

## Modeling:

For this project I built a few different models, but the ones that stood out were Random Forest due to ease of understanding and speed compared to some other models and XG Boost due to a slight increase in accuracy.  I tuned both models using number of trees, learning rate, max depth, and a few other hyperparameters.  At the end of the day, I was able to acheive roughly 80% accuracy overall for this ternary classification problem.  On top of that, I was able to achieve 94% adoption recall and 80% RTO recall.  I would have loved to have much higher RTO recall, but that can be a challenge for another time, perhaps with better data!


## Model Evaluation:

Measuring accuracy for multiclass classification problems can be tricky.  It's easy to get caught up in dizzying array of possible accuracy metrics one can use.  Here is the list I settled on for this ternary classification puzzle:
<br>
- __Training Accuracy__ 
    - General accuracy of the training set - useful to make sure you're not overfitting the model
- __Testing Accuracy__
    - Ratio of correct classifications to total classifications - useful metric, but there's more to dig into!
- __RTO Precision__ 
    - Ratio of correct RTO classifications to correct RTO + False positives 
    - Useful to make sure you're not biased too heavily and making too many false positives
- __RTO Recall__ 
    - Ratio of correct RTO classifications to correct RTO + the ones the model missed i.e. false negatives
    - Useful to see what ratio of the target class you're identifying, i.e. not missing anyone
- __Adoption Precision__ 
    - Same as RTO Precision but with the adoption metric
- __Adoption Recall__ 
    - Same as RTO Recall but with the adoption metric
<br>


A few things may stand out.  The first glaring issue is the lack of metrics around the 'Transfer' outcome.  I chose to ignore this as adoption and return to owner are the main important outcomes here.  In most cases, transferring an animal occurs when it can neither be adopted or returned to an owner.  For my model to be effective, I wanted to make sure that every pet with an owner searching for it got returned home, and every pet that is able to be adopted is adopted.  The above list of metrics tells me everything I need to know in that regard.
<br><br>
Here is the confusion matrix for the best performing model, the XG Boost:
- 1 = Return to Owner
- 2 = Transfer
- 3 = Adoption
<br><br>

![Imgur](https://i.imgur.com/Yl6jEZ8.png)

Additionally, I put together a chart to show the differences between the major models:
![Imgur](https://i.imgur.com/n3gEEoD.png)
As you can see, the XG Boost performed the best overall.  While it did not have the best performance in every single category, it is one of the more powerful machine learning models and had consistently excellent performance.  As such, it is the model I would recommend if the Austin Animal Center were to use it in their day to day operations.

## Conclusion: 

This exercise in model building has been quite informative.  While pets returned to owners are the smallest of the main groups, it's crucial they get the attention they need instead of being transfered out or adopted to another family.<br><br>

__Returning to Owner:__
- Pets that are the most likely to have their families looking for them should be put front and center on the website so families can find them easily.
- The XG Boost model can identify pets with families searching for them almost 85% of the time.  With this knowledge, they can be returned much more quickly than if the families had to search through the entire site or visit the shelter to search for their pet.

__Adoption:__
- Pets likely to be adopted should be a close second in terms of priority. 
- Recall for adoption is even higher.  With XG Boost, the shelter can identify 94% of animals that will be adopted.  The sooner they leave the shelter, the better, so it would be helpful to advertise these identified animals more heavily on the site compared to ones likely to be transferred.

__Data Collection:__
On top of that, we can improve data collection in the future to improve the model.  There are a few major areas that could help:
- Change color upon intake to one of 15 or so values instead of an arbitrarily chosen color.  This has resulted in over 500 different colors recorded in the dataset.
- Change location data to longitude and latitude data.  This makes it much easier to compare locations.  It can also help when implementing maps on the site.
- Include a measurement of temperament, perhaps on a scale of 1-10.  This can also help with adoption and RTO recall.
- Change breeds to a more standardized list as well.  Like color, this model is too unwieldy to use effectively.
<br>
Overall, though, this model should help the vast majority of pets find their way to owners.  With some work on the website and internal database applications, we can set up a system to help animals find their homes!
<br>
Please let me know if you have any questions or comments on the code
<br>
Thanks for reading!

-Thomas Brown
