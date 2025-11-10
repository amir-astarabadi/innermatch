# InnerMatch

**InnerMatch**
**Self-improving vector matcher that learns what the user meant, not just what they clicked.**

InnerMatch is an adaptive search engine core.
You give it **binary vectors** representing attributes, and it learns, from the user’s behavior, what attributes truly matter.

The more feedback you send, the smarter it becomes **inside the same search session**.

> Yes: InnerMatch literally evolves during a search session.

---

## Why InnerMatch exists

Users rarely know the exact keywords or filters to click.

InnerMatch solves this:

* HR says “I need Python, Kubernetes”
* HR clicks 3 jobs they like
* InnerMatch learns what “Python, Kubernetes” MEANT for this specific HR person **in THIS search**, and returns more accurate matches next call.

---

## Use-Cases

| domain     |       features     | targets       |
| ---------- | -----------------  | ------------- |
| Job boards |         skill tags | job positions |
| Ecommerce  | product attributes | products      |
| Travel     |     hotel features | hotels        |
| Dating     |   personality tags | profiles      |

etc.

Any domain where “items” have sets of features.

---

## Pre-Requisite

You need **your feature space defined**.

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

---

## Where do I deploy InnerMatch?

→ Available on **Google Cloud Marketplace**

Spin up, get endpoint URL. Done.

---

# HOW THE SYSTEM WORKS

### step 1, /follow

Send the query + all candidates.
InnerMatch responds with ranked matches.

### step 2, user interacts (clicks, dwell time, etc)

Send those interactions as feedback to `/feedback`.

### step 3, the model evolves in this session

At any moment, call `/features` → InnerMatch will output the current importance weights it learned.

---

# API

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

---

## 2) POST /feedback

**Purpose:** teach InnerMatch what the user actually liked/disliked

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

---

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

> see all endpoints documentation for details on /docs.

---

# FAQ

### Can InnerMatch work with sparse high dimensional vectors?

Yes. Even 20,000 + features is fine.

### Does order of array indexes matter?

**Yes.** It must remain consistent across query + targets + feedback.

### Can I update model during the same session any time?

Yes. InnerMatch is online learning, instant adaptive.

---

# Summary

InnerMatch is not a ranking API.
It is a **self-correcting matcher**.

You send vectors, it learns, per user, per session.

By the time user has interacted with 5–15 items, the system now understands **what they were really searching for**.

