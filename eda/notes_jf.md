## Kaggle prompt/description
- should we use [ROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) to evaluate models?
- kaggle mentions a benchmark random forest model (link is broken) - should we try this as our benchmark?

## NLP Getting Started
- this example is about tweets, which is only words. Pizza project has words and other features... break out text separately and evaluate?
- potentially helpful code snippets:
    - in addition to other imports: `from sklearn import feature_extraction, linear_model, model_selection, preprocessing`

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
    - <span style="color:green">**QUESTION FOR GROUP**: turn this into 1 and 0 or OK as is?</span>
- does not appear to be any missing values - all columns have 4040 entry count
- `post_was_edited` looks weird - should be boolean but have non 0/1 entries - may need to impute
    - 299/4040 (~7.5%) of observations are not 0 or 1
    - 346/4040 (~8.6%) of observations are 1
    - 3395/4040 (~84%) of observations are 0
- the 4 columns that sum/subtract upvotes and downvotes may need imputing. max upvote is 345, max downvote is 47, but sums are in millions - is this total for the user (requester)? Or just for this post?
- notable correlations:
    - strong positive correlation (0.92) between `requester_upvotes_minus_downvotes_at_request` and `requester_upvotes_plus_downvotes_at_request`
    - strong positive correlation (0.75) between `requester number of subreddits at request` and `requester_number_of_comments_at_request`
    - <span style="color:green">**QUESTION FOR GROUP**: a few in the ~0.5 range, do we want to look more into these too?</span>
- a lot of skewed distributions for the features
    - <span style="color:green">**QUESTION FOR GROUP**: should we transform?</span>
- `requester_subreddits_at_request`
    - this lists the different subreddits the user is part of
    - <span style="color:green">**QUESTION FOR GROUP**:can probably drop unless we want to look at specific subreddit relationships. If we want count, we can use column `requester_number_of_subreddits_at_request`</span>
- `request_title`
    - each title starts with some version of "[Request]"
        - need to figure out how to handle this

## Other
- <span style="color:green">**QUESTION FOR GROUP**: Should we try using wikipedia data (would need to find it) and transfer learnings into a model for us?</span>