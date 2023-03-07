# Airbnb-Hostbook
The project aims to use supervised learning techniques to identify the features that lead to high-value ratings in Airbnb listings by analyzing the Detailed Listings data from various cities, developing a guide handbook, and improving guests' confidence in Airbnb's value proposition.

## Business Problem to be solved
Airbnb management is receiving a lot of complaints from their hosts regarding the value ratings submitted by guests. </br>
</br>
The hosts are removing their listings due to their low-value ratings submitted by the guests, which have severely impacted the possibility of their potential lettings. 
If Airbnb manages to identify the contributing features that lead to high-value ratings, they will develop a guide handbook and share it with all Airbnb hosts. </br>
</br>
Such a guide handbook will help Airbnb hosts to boost their value ratings and will also help Airbnb to retain their hosts.

## Data Description
The data used to approach this problem is the ‘Detailed Listings data’ (e.g., for Amsterdam: http://data.insideairbnb.com/the-netherlands/north-holland/amsterdam/2022-01-06/data/listings.csv.gz). </br>
</br>
Since the analysis is not focused on a city specifically but should serve as a general (global) best practices overview, all available data sets for the different cities will be combined. These data sets contain 74 columns however non-statistical relevant columns like ids, names, etc. will be dropped. Also, some columns are not relevant for the business goal and can be excluded (e.g., reviews per month). Additionally, there is a target leakage with all scores in the dataset. The overall rating score is computed by taking the average over 6 other rating scores (incl. the objective variable, review_scores_value, but also other scores like communication or cleanness). Thus, all other scores will be removed, the analysis only focuses on features of the property and how they should be presented. With all columns to be removed, there are about 40 left for the analysis, which gives enough information for an actual analysis but also is not too busy from an interpretability viewpoint.</br>
</br>
Some text features like description or host_about might be transformed into numerical values (e.g., text length).

## Model Training
In the Jupyter Notebook file, you can see that the first attempt was to use linear regression, but due to the target feature being a continuous variable, it was difficult to predict a specific value. As a result, the target feature was transformed into a categorical feature. Logistic regression, random forest, and decision tree models were trained on the Detailed Listings data from various cities. The results showed that the random forest model outperformed all other models in terms of accuracy, although it came at the cost of interpretability.
![image](https://user-images.githubusercontent.com/123428884/223525934-0d6782d9-d085-400a-964a-6f458703c521.png)</br>
</br>
To improve the performance of the random forest model, GridSearchCV was used to find the best parameters. This was done by searching over a range of hyperparameters to identify the combination that produced the best performance. Once the best parameters were identified, the random forest model was rebuilt with the new parameters. The final model was evaluated using the RMSE score as the evaluation metric.
![image](https://user-images.githubusercontent.com/123428884/223526021-70649faa-c742-41df-b7b1-6020159cffdd.png)</br>

## Model Interpretation
#### Implications of top 10 features
Feature | Weight | Implication
--- | --- | --- 
instant_bookable_TRUE | 0.27 | Instant bookable feature provides more convenience and ease to customers and thus lead to higher satisfaction rate and higher overall ratings
price | 0.10 | Customers are extremely sensitive to prices, in which their overall score ratings hinges on whether they perceive a listing to be a good value for money or not
amenities | 0.09 | The number of amenities has a positive correlation with the overall score rating of a listing, the more amenities the listing has the better the overall rating gets
host_acceptance_rate | 0.07 | Guests tend to like properties which’s hosts have a high acceptance rate. Most likely this is a corelation without major implication for hosts
description | 0.07 | The description of a listing influences how customers perceive the overall quality of a listing; hence the more elaborate the description is the higher the overall score rating gets
maximum_nights | 0.05 | It is inconvenient for customers to relocate from a listing when the max nights available don’t match their total stay duration and thus higher max nights lead to more satisfied customers
neighborhood_overview | 0.05 | Neighbourhood has a huge influence on customers overall experience whilst renting a property, and thus impacts the overall score ratings
host_about | 0.05 | About host feature gives a better credibility to hosts and make their profiles more legitimate, the older the description of the profile is the better the overall score rating
host_verifications | 0.04 | Customer would feel safer and more relieved if an Airbnb host has a verified identity and thus it would enhance their overall experience and overall score rating
minimum_nights | 0.04 | Flexible stay duration in terms of minimum nights provide more convenience to short-stay customers and thus has a negative correlation with the overall score rating
