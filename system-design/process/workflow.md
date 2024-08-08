# System Design Workflow

## Step 0: General Pointers

See [here](general.md).

## Step 1: Requirements clarifications

Ask questions about the exact scope (what is expected) of the problem we are trying to solve. Go over `functional` and `non-functional` requirements. E.g. for a twitter like system:

- Will users of our service be able to post tweets and follow other people?
- Should we also design to create and display the user's timeline?
- Will tweets contain photos and videos?
- Are we focusing on the backend only, or are we developing the front-end too?
- Will users be able to search tweets?
- Do we need to display hot trending topics?
- Will there be any push notification for new (or important) tweets?

All such questions will determine what our end design will look like.

For more see [here](estimations.md).

## Step 2: Scale Estimation

Based on the requirements, estimate the scale of the system we're going to design. This will also help later when we focus on scaling, partitioning, load balancing, and caching.

- What scale is expected from the system (e.g., number of new tweets, number of tweet views, number of timeline generations per sec., etc.)?
- How much `storage` will we need? We will have different storage requirements if users can have photos and videos in their tweets.
- What network `bandwidth` usage are we expecting? This will be crucial in deciding how we will manage traffic and balance load between servers.
- Is it write or read heavy?

For more see [here](requirements.md).

## Step 3: System interface definition

Define what APIs are expected from the system. This will establish the exact contract expected from the system and ensure if we haven't gotten any requirements wrong. Some examples of APIs for our Twitter-like service will be:

```
postTweet(user_id, tweet_data, tweet_location, user_location, timestamp, …)

generateTimeline(user_id, current_time, user_location, …)

markTweetFavorite(user_id, tweet_id, timestamp, …)
```

## Step 4: Defining data model

Defining the `data model` in the early part of the interview will clarify how data will flow between different system components. Later, it will guide for data partitioning and management. Should identify various system entities, how they will interact with each other, and different aspects of data management like `storage`, `transportation`, `encryption`, etc. Here are some entities for our Twitter-like service:

```
User: UserID, Name, Email, DoB, CreationDate, LastLogin, etc.
Tweet: TweetID, Content, TweetLocation, NumberOfLikes, TimeStamp, etc.
UserFollow: UserID1, UserID2
FavoriteTweets: UserID, TweetID, TimeStamp
```

Which `database system` should we use? Will `NoSQL` like Cassandra best fit our needs, or should we use a `MySQL`, like solution? What kind of block storage should we use to store photos and videos?

## Step 5: High-level design

Draw a diagram representing the core components of the system. The diagram should identify enough components that are needed to solve the actual problem from end to end.

For Twitter, at a high level, we will need multiple application servers to serve all the read/write requests with load balancers in front of them for traffic distributions. If we're assuming that we will have a lot more read traffic (compared to write), we can decide to have separate servers to handle these scenarios. On the back-end, we need an efficient database that can store all the tweets and support a large number of reads. We will also need a distributed file storage system for storing photos and videos.

![](images/high-level-design.png)

## Step 6: Detailed design

`Dig deeper into two or three major components`; the interviewer's feedback should always guide us to what parts of the system need further discussion. We should `present different approaches`, their `pros and con`s, and explain why we will `prefer` one approach over the other. Remember, there is no single answer; the only important thing is to consider tradeoffs between different options while keeping system constraints in mind.

- Since we will be storing a massive amount of data, how should we partition our data to distribute it to multiple databases? Should we try to store all the data of a user on the same database? What issue could it cause?
- How will we handle hot users who tweet a lot or follow lots of people?
- Since users' timeline will contain the most recent (and relevant) tweets, should we try to store our data so that it is optimized for scanning the latest tweets?
- How much and at which layer should we introduce cache to speed things up?
- What components need better load balancing?

## Step 7: Identifying and resolving bottlenecks

Try to discuss as many bottlenecks as possible and different approaches to mitigate them.

- Is there any single point of failure in our system? What are we doing to mitigate it?
- Do we have enough replicas of the data so that we can still serve our users if we lose a few servers?
- Similarly, do we have enough copies of different services running such that a few failures will not cause a total system shutdown?
- How are we monitoring the performance of our service? Do we get alerts whenever critical components fail or their performance degrades?
