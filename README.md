# Synaptosearch InnerMatch
---

**Introduction**
- This matching framework not only provides matching functionality between two data items, but also helps the user discover and understand what he/she is truly looking for, by providing feedback capability to the user and also extracting and representing underlying hidden aspects that the user might not be aware of, regarding his/her preferences.
---

**How It Works**
Euclidean distance has been vastly used as a measure of closeness and similarity between two vectors. In geometry, the measure is defined as the length of straight line segment connecting two points. Considering two vectors (array of numbers) X(1) and X(2), the Euclidean distance between the two vectors can be defined as
follows:

![Euclidean distance](Euclidean_distance.png)
In Machine Learning and Artificial Intelligence, each element of the vectors represents a meaningful feature of the data such as color, size, shape, orientation, etc. Considering the Euclidean distance as a measure of similarity, based on the formula above, we can see that the difference between the values of each feature in the two vectors has a role in computing the similarity. In a simple binary case for instance, where the value of each feature can be zero or one:
The value of same features corresponding to the two vectors, should be similar in order to reduce the distance between two vectors and increase the similarity.

## Current Problems
Although this concept seems trivial and reasonable for matching two vectors, however we believe that Euclidean distance is missing some critical properties, some of which listed as follows:

- **Cross feature effect**: In some applications we might need to consider the relation between different features in calculating the matching between two vectors. For instance, we might need a case where:
If object A is a ball and object B is a racket, then the possibility of the two objects matching should increase.
In this case if being a ball is one feature and being a racket is another feature, Euclidean distance would not be able to match two vectors having these features active in a binary case.

- **Inhibition**: In some cases, we might need the presence of one feature in a
vector prevent the presence of the same or other feature in the second
vector. For instance, consider the case below:
If object A is a bolts and object B is screwdriver, then the possibility of match between the two vectors should decrease. In this case, if being bolts is one feature and being screwdriver is another feature, Euclidean distance would not be able to reduce the possibility of match between two vectors containing them.

- **Negative effect**: In some cases, we might need some features to affect thesimilarity negatively while the others affecting it positively. For instance, consider the following case:
If we have some demographic features including gender and language, we might want the feature gender to have negative effect on the similarity, e.g. if both items (vectors) are male (or female) we would like to reduce the chance of match while having the same language would increase the chance
of match. In such cases, standard Euclidean distance is not able to treat gender and language differently while computing the match between two vectors.
---

## Proposed Solution
At Synaptosearch, we have been working of a new distance measure for Machine Learning and Artificial Intelligence applications that would provide the properties of cross feature effect, Inhibition and negative effect at the same time. The proposed method could be considered at high level as a ‘programmable distance measure’ where the required relation between the features to calculate the distance can be learned through feed-back during the execution of the algorithm in real-life scenarios. 
The proposed solution, has the following benefits:
- There is no required training and testing phase, unlike ordinary machine learning approaches and the algorithm learns the required relations between the features throughout the real-time online execution of the system.
- The algorithm starts from the baseline Euclidean distance and improves gradually through getting feed-back from the corresponding system which complements the first benefit mentioned above.
- The algorithm with some additional steps can potentially work on any type of vectors representing the data e.g. bag-of-words, clustered data, local representations, distributed representation, etc.
- The algorithm works with a very light model to compute the distances which makes it very time and memory efficient.
- The most important benefit of the algorithm is the ability to incorporate relations between features such as cross feature effects, inhibition and negative effect.
- And finally, as mentioned before, the relation between features do not need to be hardcoded by an expert, while they can simply be learned through the feed-back given by the system.

# Key Product Features

- **Feature scalability**: Using existing (deep learning) models, developers are not able to extend or limit the feature space during the runtime, while in real world, this capability can be considered as a valuable feature.

- **Interactiveness**: Existing applications, except recommender systems, do not really incorporate feedback from the users, while these feedbacks could be valuable in reshaping the matching algorithm for future.

- **No Cold start**: While learning algorithms require a lot of data for training, matching algorithms usually suffer from the cold start problem in which the performance of the matching is low in initial steps and interactions until the algorithm gathers enough data to learn the underlying patterns. A matching algorithm that can, 1- start from a reasonable starting point and 2- learn fast in terms of amount of data required to train the model, can be of a valuable benefit.

- **Dimensional search**: Existing matching algorithms, even though some of which consider user feedbacks, don’t explore the feature space for relevant dimensions in performing the match, while searching through the dimensional space of input through interactions could provide valuable insight about what features really contribute to the match more.

- **Real-time requirements**: One of the most important requirements of the matching algorithm is its performance. As the matching algorithm is supposed to be called several times for each query, fast and simple computation capability of the matching algorithm is a valuable benefit.

- **Dynamic preferences**: One of the main requirements of the matching algorithms is the ability to adapt to user dynamic preferences, as the user might change his/her preferences along time. A matching algorithm that is able to track the changes and adapt to them in an appropriate speed could provide additional value to the corresponding application.

- **Modality agnosticism**: Existing matching algorithms purely rely on the modality of input data, while being able to combine and transform multiple modalities by encoding data into a unified representation can be valuable.

---

# Examples Of Business Use Cases

## Talent Matching (HR/Recruiting)

### Use Cases:
- Personalized job matching that evolves with candidate preferences and career goals.
- Hiring platforms that adapt based on recruiter or hiring manager feedback.
- Discover latent candidate qualities (e.g. ambition, cultural alignment) beyond the resume.
### Business Values:
- Reduce time-to-hire by understanding real-fit factors early.
- Decrease turnover by aligning deeper personal and cultural preferences.
- Solve cold-start by offering quality matches even for new users or roles.
---

## Dating Apps
### Use Cases:
- Dynamic partner matching that evolves with the user’s romantic experiences and reflections.
- Help users discover what traits actually matter to them through guided feedback.
- Identify latent compatibility factors like communication style, values, or attachment types.
### Business Values:
- Boost user engagement and retention by personalizing the discovery journey.
- Improve long-term match success rates.
- Stand out with a "growth-focused" dating experience, not just swiping.
---

## Recommender Systems
### Use Cases:
- Adaptive product/content recommendation that learns from nuanced feedback over time.
- Exploration of feature dimensions (e.g. tone, aesthetic, function) to discover preferences.
- Cross-modal recommendations (text, image, video) based on unified user understanding.
### Business Values:
- Higher conversion rates through relevance and serendipity.
- Reduced bounce rates by adapting fast to new or cold users.
- More insightful analytics on why customers choose products.
---

## Learning Platforms
### Use Cases:
- Match learners with courses, contents or resources that evolve with their goals and learning pace.
- Help users discover learning paths based on strengths, weaknesses, and goals they didn’t know they had.
- Personalized mentor or study group matching.
### Business Values:
- Increase course completion and satisfaction rates.
- Personalize education with minimal upfront data.
- Enable lifelong, dynamic learner journeys.
---

# Enterprise Knowledge Discovery
### Use Cases:
- Match employees with documents, experts, or datasets even when they don’t know what exactly they need.
- Enable contextual, real-time knowledge surfacing across departments.
- Learn from feedback to improve future discovery relevance.
### Business Values:
- Reduce knowledge silos.
- Speed up research, innovation, and collaboration.
- Support tacit knowledge discovery via belief-based exploration.
---

# Information Retrieval
### Use Cases:
- Support exploratory queries in which the user doesn't yet know what to ask.
- Help researchers find hidden, cross-disciplinary or latent relationships in data.
- Feedback-informed retrieval that evolves with a researcher’s line of thinking.
### Business Values:
- Accelerate time to insight.
- Enable production of new knowledge, not just retrieval of old.
- Facilitate intellectual exploration in ambiguous or emergent domains.
---

# Search Engines
### Use Cases:
- Help users refine their beliefs and needs during search, not just serve known-intent queries.
- Power belief-based, conversational or introspective search.
- Disentangle intent dynamically through user feedback.
### Business Values:
- Improve query satisfaction even in complex or ill-defined searches.
- Reduce abandonment by guiding users through query evolution.
- Create next-gen search experiences that feel intelligent and empathetic.
---

# Real Estate
### Use Cases:
- Match users with properties based on evolving preferences like neighborhood vibes, emotional
- resonance, lifestyle fit — not just filters.
Use feedback to explore which features (e.g. lighting, layout, proximity) matter most.
- Handle cold-start users through smart defaults and belief prompts.
### Business Values:
- Improve lead conversion by aligning with deeper homebuyer needs.
- Shorten the property discovery cycle.
- Deliver surprisingly relevant listings that increase engagement.
---

# Mentorship Programs
### Use Cases:
- Match mentors and mentees dynamically as interests, goals, and personalities evolve.
- Capture and respond to feedback loops in mentorship satisfaction.
- Suggest mentorship topics or pairings based on latent growth desires.
### Business Values:
- Enhance mentorship success and retention.
- Enable scalable, personalized mentorship at institutions or enterprises.
- Create self-improving networks through continuous feedback.
---

## Example

First you need define your feature space.

Example: skills list in your HR database:

| index | skill      |
| ----: | ---------- |
|     0 | Python     |
|     1 | SQL        |
|     2 | Kubernetes |
|     3 | React      |

If HR chose: Python and Kubernetes → your query_vector becomes:

```json
[1,0,1,0]
```

Each job position MUST have vector representation with exact **same index ordering**.

Example, Job #17:

```json
[1,1,1,0]
```

### step 1, /follow

Send the query + all candidates job.
InnerMatch responds with ranked matches.

## 1) POST /follow

**Purpose:** initial retrieval

**body:**

```json
{
  "user_id": "<hr unique auth id>",
  "session_id": "<uuid of this search session>",
  "query_vector": [0,1,0,1,1,...],
  "target_vector_array": [
    [1,0,0,1,...],
    [0,1,1,0,...],
    ...
  ]
}
```

**response:** ranked matched targets

### step 2, user interacts (clicks, dwell time, etc)

Send those interactions as feedback to `/feedback`.
## 2) POST /feedback

**body:**

```json
{
  "user_id": "<same user id>",
  "session_id": "<same session id>",
  "query_vector_array": [
    [0,1,0,1,1,...]
  ],
  "target_vector_array": [
    [1,0,0,1,...]
  ],
  "feedback_array": [1]   // 1 = like, -1 = dislike
}
```

Note: You may send multiple feedback objects in one call as arrays.

### step 3, the model evolves in this session

At any moment, call `/features` → InnerMatch will output the current importance weights it learned.

## 3) POST /features

**Purpose:** ask InnerMatch:
“What features are now actually important in this session?”

**body:**

```json
{
  "user_id": "<same user id>",
  "session_id": "<same session id>",
  "query_vector": [0,1,0,1,1,...]
}
```

**response:** a score per feature.

---

# FAQ

### Can InnerMatch work with sparse high dimensional vectors?

Yes. Even 20,000 + features is fine.

### Does order of array indexes matter?

**Yes.** It must remain consistent across query + targets + feedback.

### Can I update model during the same session any time?

Yes. InnerMatch is online learning, instant adaptive.

### Where do I deploy InnerMatch?

Available on **Google Cloud Marketplace**

---

# Summary

InnerMatch is not a ranking API.
It is a **self-correcting matcher**.

You send vectors, it learns, per user, per session.

By the time user has interacted with 5–15 items, the system now understands **what they were really searching for**.

