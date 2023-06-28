## Kaggle prompt/description
- should we use [ROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) to evaluate models?
- kaggle mentions a benchmark random forest model (link is broken) - should we try this as our benchmark?

## NLP Getting Started
- this example is about tweets, which is only words. Pizza project has words and other features... break out text separately and evaluate?
- potentially helpful code snippets:
    - in addition to other imports: `from sklearn import feature_extraction, linear_model, model_selection, preprocessing`
    - 

## Random Acts of Pizza Subreddit
### Intro to Random Acts of Pizza Rules on Reddit
- strict rules
- users cannot request within 7 days of an unfulfilled request, 90 days of a fulfilled request
    - <span style="color:red">*our dataset spans 1,026 days (12/8/2010 - 9/29/13) - may want to check balance of fulfilled/unfulfilled, users with repeat entries*</span>
    - <span style="color:red">*does # of posts end up resulting in a free pizza?*</span>
- users able to request side orders and soft drinks ONLY (in addition to pizza)
    - <span style="color:red">*does our dataset have what was requested?*</span>
- from the [Evaluating Requests](https://www.reddit.com/r/Random_Acts_Of_Pizza/wiki/howto_fulfill/#wiki_evaluating_requests) section
    - it warns against fulfilling request to users with low karma
        - <span style="color:red">*EDA: look at karma distribution?*</span>
        - <span style="color:red">*what other "user" metrics are there?*</span>

## Associated Paper
- break analysis into two factors:
    1. **social factors** (who is asking and how the recipient is related to the donor and community)
    2. **linguistic factors** (how they are asking and what linguistic devices accompany successful requests)
- they used logistic regression
- in the timeframe specified (12/8/10 - 9/29/13), there were actually 21,577 posts in the subreddit. However, the data for this only includes users who made a single request (more info as to why in section 2 of the paper)
    - <span style="color:green">**LIMITATION** - we are not able to assess users who made repeat requests</span>
- the data was split 70/30 train/test such that both sets mirror the average success rate in our dataset of 24.6%
    - <span style="color:green">**QUESTION FOR GROUP**: do we want to merge all data together and split differently?</span>
    - <span style="color:green">**QUESTION FOR GROUP**: do we want an additional split within training to include a train and validation set (90/10?)</span>
- categories/factors:
    - Textual Factors:
        - *politeness*
        - *evidentiality*
        - *reciprocity*
        - *sentiment*
        - *length*
    - Social Factors:
        - *status*
        - *similarities*
    - <span style="color:green">**QUESTION FOR GROUP**: should we try some kind of clustering with the text? Perhaps resulting in feature engineering of one-hot encoding?</span>

## EDA Notes/Findings
- `requester_received_pizza` column is boolean outcome label