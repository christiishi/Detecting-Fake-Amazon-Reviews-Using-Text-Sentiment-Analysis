# Detecting Fake Amazon Reviews Using Text Sentiment Analysis

## Overview
This project analyzes Amazon product reviews to identify suspicious and potentially fake reviews by examining reviewer behavior, textual patterns, and sentiment signals. Using a combination of unsupervised and supervised machine learning techniques, the project detects anomalous review activity and develops interpretable rules to support fraud detection and trust preservation on e-commerce platforms.

## Problem Statement
E-commerce sites like Amazon rely heavily on user reviews to inform purchasing decisions. However, the presence of fake or coordinated reviews undermines customer trust and platform credibility. This project aims to address the following challenges:

* Detect suspicious or potentially fake reviews using behavioral and textual signals
* Identify abnormal reviewer behavior such as high-frequency posting and burst activity
* Understand whether fake reviews exhibit extreme sentiment or abnormal linguistic patterns
* Provide actionable detection rules that can support automated moderation systems

## Data
**Source**: Kaggle – Amazon Products Review dataset

**Total Records**: 568,454 reviews

**Final Dataset**: 567,246 unique reviews after cleaning

**Total Columns**: 10 (expanded via feature engineering)

**Key Features**:
* Review text, star rating, and timestamp
* Reviewer-level activity metrics (posting frequency, burst behavior)
* Text-derived features (review length, sentiment polarity)
* Aggregated user behavior indicators

## Data Processing 

* Removed duplicate reviews based on ProductID, UserID, timestamp, and text
* Filtered invalid helpfulness scores (numerator > denominator)
* Converted Unix timestamps into readable date formats
* Cleaned text using TRIM + LOWER to standardize inputs
* Engineered behavioral and textual features, including:
  * Review length
  * Reviews posted per day
  * Single-day burst frequency
  * Average user sentiment and score consistency
  * Count of extreme (5-star) reviews per user
 
## Modeling Approach

**Text & Sentiment Analysis**
* Applied sentiment analysis to both review summaries and full review text
* Compared sentiment polarity with star ratings to detect inconsistencies
* Generated positive and negative sentiment word clouds to identify linguistic patterns associated with suspicious reviews 

**Customer Segmentation (Unsupervised Learning)**
* Implemented K-Means clustering on behavioral and text-based features
* Identified distinct reviewer behavior profiles
* Flagged approximately 28.5% of reviews as exhibiting anomalous or high-risk patterns
* Used clustering to isolate potential spammer and bot-like reviewer groups 

**Fake Review Detection (Supervised Learning)**
* Built Decision Tree classification models to distinguish normal vs. suspicious reviews
* Evaluated performance using accuracy, precision, recall, F1-score, and confusion matrices
* Performed 5-fold cross-validation to assess model stability and robustness

## Key Results & Insights
* A critical threshold of ~6.5 reviews per day strongly predicts fraudulent behavior
* Suspicious reviews averaged 236 characters, ~40% shorter than legitimate reviews
* Identified 141 duplicated or near-identical review scripts, indicating coordinated review farms
* Decision Tree achieved ~95.5% accuracy, suggesting fake review behavior follows highly detectable rules
* High-frequency burst activity combined with sentiment inconsistency emerged as the strongest fraud signals

## Business Recommendations
Based on our analysis of reviewer behavior, sentiment patterns, and posting frequency, we recommend the following actions to strengthen review integrity and reduce fraudulent activity on the platform:

* Implement automated burst-activity and sentiment-mismatch detection

Reviews should be automatically flagged when abnormal posting frequency is observed or when the emotional tone of the review text contradicts the associated star rating (e.g., highly negative language paired with a 5-star rating). These signals were strongly associated with suspicious review behavior in our analysis.
* Introduce activity-based posting controls for high-risk users

Temporarily restricting posting privileges for users who exceed a defined daily review threshold (e.g., 7+ reviews per day) can help mitigate coordinated or bot-driven review bursts while minimizing disruption to typical users.
* Require additional verification for repeated high-volume or inconsistent behavior

Implementing CAPTCHA challenges or identity verification for users exhibiting repeated high-frequency posting or inconsistent sentiment patterns can act as an effective deterrent against automated or fraudulent review generation.
* Develop a reviewer risk scoring system

A composite reviewer credibility score should be created by combining behavioral metrics (posting frequency, burst activity) with text-based features (sentiment consistency, review length variation). This score can be used to rank reviewers by risk level.
* Prioritize moderation using credibility-based review ranking

Reviews and users with the highest risk scores should be prioritized for manual inspection, allowing moderation teams to allocate resources efficiently while maintaining high detection accuracy.

## Limitations
* Dataset reflects review behavior from the early 2010s and does not capture modern LLM-generated text
* Lack of verified “fake” labels means the model detects high-risk anomalies rather than confirmed fraud
* Detection is optimized for high-volume burst attacks and may flag legitimate power users
* Strict activity thresholds can produce false positives for highly engaged reviewers

## My Contributions
* Led exploratory text analysis, including generation and interpretation of sentiment-based word clouds to identify linguistic patterns associated with suspicious reviews
* Interpreted model outputs and clustering results to extract actionable insights from complex behavioral data
* Translated analytical findings into concrete business recommendations focused on fraud detection, reviewer risk scoring, and platform trust improvement

## Contributors
* **Christie Shin**
* Shivani Vallamdas
* Gema Zhu
* Vishal Srivastava
* Shuai Zhao

