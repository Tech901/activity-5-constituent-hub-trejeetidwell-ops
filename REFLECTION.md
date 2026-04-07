---
title: "Activity 5 Reflection - Constituent Services Hub"
type: reflection
version: "1.0.0"
---

# Activity 5 Reflection

Answer each question in 3-5 sentences. Thoughtful, specific responses earn full credit.

## 1. PII Redaction in Practice

What PII categories did the Azure AI Language service detect in the Memphis 311 complaints? Did you notice any false positives (non-PII flagged as sensitive) or false negatives (PII that was missed)? How might PII detection requirements differ between a government agency processing citizen complaints and a commercial customer service system?
 The fields detected were name, social security number, address, and phone number. Instances where someone is describing the site of a 311 report such as just beale street or union avenue these were noticable false positives. These detials are essential in understanding where to send the work crews. It also flagged people associated terms like family. There were also times where time based words like "now" were redacted. 

## 2. Sentiment as a Routing Signal

How could sentiment analysis be used to prioritize Memphis 311 complaints — for example, routing highly negative complaints to senior staff? What are the risks of relying solely on sentiment for prioritization (consider complaints that are neutral in tone but urgent in nature)? How would you combine sentiment with other signals for a more robust routing system? 

I could put together a function that takes in account the severity of the call or the number of violations or concerns in the statement. Reports with multiple believed violations would be ranked higher and submitted to senior staff through the routing system. 

## 3. Multilingual Challenges

How accurately did the Language service detect the language of short versus long text samples? What challenges might arise with code-switching (mixing languages in a single message), which is common in multilingual communities? How would you handle a complaint where language detection confidence is low?

In long text samples it did a good job of redacting private information but failed to identify the language being used. This suggest sending the report to a human for review in hopes to clarify what language and the translation accuracy. With low language dectection confidence I would have senior staff to review the report. 

## 4. CLU vs. Keyword Matching

Compare the CLU model's intent classification with the keyword-based fallback. In what scenarios did CLU perform better, and where did keyword matching suffice? What are the trade-offs of training and maintaining a custom CLU model versus using a simpler rule-based approach for a city's 311 system? *(If CLU was not configured in your environment, discuss how you would expect it to differ based on the training data in `data/intent_examples.json`.)*
I believe based on the CLU intent classification it performed better with training data. This would reduce misclassification. The key word matching while simple it would fail when considering certain nuances and doen't extract proper entities. The best route would be to adopt an hybrid approach of using a rule check for high confidence matches with keywords while using CLU for ambigous cases which can be prepared through training data.
## 5. Pipeline Design

Which step in your NLP pipeline was most critical to get right first, and why? If you were deploying this pipeline for production use handling thousands of complaints daily, what monitoring, fallback mechanisms, or error handling would you add? How would you measure pipeline health over time?
I would say PII detection. This is critical due to the nature of the information we are dealing with and that this is a government entity meaning citizen's privacy is of utmost importance. For monitoring purposes I would include latency checks with each API call, error rates (failures per step/timeouts/invalid responses) If i could monitor data quality I would include this as well. To monitor pipeline health I'd include accuracy metrics and cost per compliant to prevent costly errors or misclassifications. 