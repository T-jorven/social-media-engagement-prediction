# Social Media Engagement Prediction (Machine Learning)

This project explores how different content characteristics influence social media performance using machine learning regression models.
Based on historical post data (media type, timing, caption length, hashtags, content category, and traffic source), the goal is to predict engagement-related metrics such as engagement rate, reach, likes, and followers gained.
The project focuses on:
Feature engineering from timestamp, text length, and categorical metadata
Building and comparing regression models (Linear Regression, Random Forest, Gradient Boosting)
Preventing data leakage in engagement metrics
Interpreting feature importance to derive actionable content insights
The outcome provides both predictive models and data-driven recommendations for optimizing content strategy.

The data can be found here: https://www.kaggle.com/datasets/kundanbedmutha/instagram-analytics-dataset

Initial regression models predicting follower growth achieved near-baseline performance, indicating limited explanatory power of post-level features for follower acquisition. This finding motivated a shift toward predicting engagement-related metrics, which are more directly influenced by content characteristics. 

The reach prediction model leverages post-performance engagement signals (likes, comments, shares, saves) to explain how content is distributed. As such, it is intended for post-hoc analysis rather than pre-publication forecasting.

While reach can be predicted with high accuracy when impressions are included, removing impressions causes model performance to collapse. This indicates that reach is largely determined by distribution mechanics rather than by content or timing features alone.

Impressions and reach are primarily driven by platform-level distribution mechanisms that are not captured by post-level metadata or engagement signals in this dataset.

##  Summary of Findings

This project explored the extent to which social media post performance can be explained and predicted using post-level metadata, engagement signals, and timing information. The dataset contains approximately 30,000 posts with content attributes (media type, category, caption length, hashtags), timing features, engagement metrics, and exposure metrics.

---

### 1. Exploratory Data Analysis

Exploratory analysis revealed that most content-related features exhibit **only small average differences** across groups:

- **Media type** (Photo, Carousel, Video, Reel) shows minimal variation in follower growth and engagement, indicating that format alone is not a strong differentiator.
- **Posting day** has a mild effect: weekends tend to perform slightly better in terms of follower growth, while engagement peaks mid-week. However, these effects are relatively small.
- **Posting hour** could not be analyzed, as all posts were published at the same hour, making it non-informative.

Overall, EDA suggested that no single content or timing feature strongly drives performance on its own.

---

### 2. Predicting Follower Growth

Initial regression models attempted to predict `followers_gained`.

- Both Linear Regression and Random Forest models performed **no better than predicting the mean** (R² ≈ 0).
- This indicates that follower acquisition is highly noisy and likely influenced by external factors such as audience size, trends, and platform dynamics that are not present in the dataset.

**Conclusion:** Follower growth cannot be reliably predicted using post-level metadata and engagement signals alone.

---

### 3. Predicting Reach

Reach was evaluated as a potentially more stable target.

- When **impressions were included as a feature**, reach could be predicted with very high accuracy (R² ≈ 0.94).
- Feature importance analysis showed that impressions accounted for over 95% of the predictive power, revealing a near-proxy relationship between impressions and reach.
- When impressions were removed, model performance collapsed (R² ≈ 0), indicating that reach is primarily determined by distribution mechanisms rather than content attributes.

**Conclusion:** Reach is predictable only when using impressions, which limits the interpretability and usefulness of the model for content strategy.

---

### 4. Predicting Impressions

Models predicting `impressions` using content metadata and engagement actions performed poorly.

- Both linear and non-linear models achieved R² values close to zero.
- This suggests that impressions are largely controlled by platform-level algorithms and are not directly explainable by post-level features.

**Conclusion:** Impressions cannot be reliably predicted from the available data.

---

### 5. Predicting Likes

Regression models were also trained to predict `likes`.

- Both Linear Regression and Random Forest failed to outperform a mean baseline.
- This indicates that likes are driven by latent factors such as content quality, emotional resonance, novelty, and audience context, none of which are captured in the dataset.

**Conclusion:** User engagement actions such as likes are weakly related to the available features and are not suitable regression targets in this dataset.

---

### 6. Overall Conclusions

Across multiple modeling attempts, a consistent pattern emerged:

- Metrics tied to **algorithmic distribution** (impressions, reach) are not predictable from post-level metadata.
- Metrics tied to **user behavior** (likes, followers gained) are highly noisy and influenced by unobserved factors.
- Strong predictive performance is only achieved when using **near-proxy features**, which limits interpretability.

These findings highlight the importance of aligning machine learning objectives with the underlying data-generating process and demonstrate that not all performance metrics are equally suitable for prediction.

---

### 7. Key Takeaways

- Negative modeling results can be meaningful and informative.
- High model accuracy may indicate proxy leakage rather than true insight.
- Careful feature selection and target choice are critical in applied machine learning.
- Understanding *why* a model fails is often as valuable as building a successful one.

