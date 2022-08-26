# Privacy challenges in the AI Era
:label:`privacy_challenges`

In 2007-2009, Netflix --- a DVD-rental-by-mail company --- challenged the machine learning research community with a One-Millon-Dollar bounty to be awarded to whoever comes up with a new movie recommendation algorithm that beats their baseline by 10%. It was a huge success. Not only did they identify the key elements of a successful recommender system, the Netflix Prize has influenced an entire generation of brilliant machine learning researchers and inspired more to join this vibrant community.

However, when they were preparing to to do it again in 2010, the whole thing had to be put to a halt due to a class action lawsuit filed by the Federal Trade Commission in response to a privacy breach using the anonymized dataset from the first Netflix Prize. 

What happened? Netflix did everything a responsible company would do to anonymize the dataset for competition. They removing personal identifiable information (PII) such as names, addresses and demographic information and left only movie ratings on the scale of 1 to 10 indexed by ```(User i, Movie j)``` and a time-stamp. But this is not enough.  Vitaly Shmatikov et al demonstrated that one can robustly and accurately re-identify 99% of the 50000 Netflix subscribers by matching their patterns of "which movies did X watch?" to specific users on International Movie Database (IMDb). Other attacks have been shown to break more advanced anonymization tools such as k-anonymity. This story tells us that anonymization and PII removal do not work, since everything else about the dataset is just as sensitive and can be used as pseudo-identifiers, especially when some side-information is available.
 
## Aggregate statistics can be used to identify individuals.

It turns out that your privacy is under fire even if the raw data (anonymized or not) is not released publically. The privacy risk remains even if only aggregate statistics are revealed. Consider the following two database queries:
> ```sql
SELECT COUNT(*) FROM employees 
WHERE salary > 200000;
```
>
```sql
SELECT COUNT(*) FROM employees
WHERE salary > 200000 AND name != 'yu-xiang wang';
```

While each query is likely to return a large number that pose no privacy risk by itself, the combination of them directly enables the salary I am earning to be identified by a binary-search like procedure. A study conducted by the US Census Bureau concludes that the summary statistics published by US Census can be used to reconstruct 100% of the US population with 38% matching  perfectly in all fields to commertial datasets with personal identifies. Quoting US Census's Chief Scientist, John M. Abowd, in his well-articulated ICML'19 keynote, "(the privacy concern) is no longer a risk, but an issue."


## What about machine learning models? 
Machine learning models are described by their parameters --- optimized on the training data. These parameters can be viewed as aggregate statistics of the training data but the specific relationships are somewhat opaque and unexplanable. The opaqueness begs the question whether they can be associated with any privacy risks in practice.

It turns out that opaqueness does not help much. It was reported that mere black-box access to trained deep learning models can be used to infer whether an individual is a member of the training dataset (a.k.a. Membership Inference Attacks) and to reconstruct credit card numbers from the training data using just the last four digits (Data Extraction Attacks). Modern pre-trained large language models essentially memorized the entire training corpus and will generate specific sequence verbatim if a specific prompt is given. I give two examples below:

> 1. *Text completion*:  If trained by user emails, then it is likely complete with users’ text verbatim.
> 2. *Code generation*:  generating the same piece of code might be violating copyright.



## Dinur-Nissim Attack and whole database reconstruction

The data reconstruction attack conducted by the US-census is a variant of the seminal Dinur-Nissim attack, which uses linear programming to accurately reconstruct any dataset in a very general "bit-sequence" representation.  The attack implies an information-theoretic lower bound that governs the **fundamental law of privacy-accuracy tradeoff**, which limits the accuracy *any* methods can achieve when they need to reveal a high-dimensional statistic of the dataset while preventing more than 90% of the dataset to be reconstructed. It is to be noted that the Dinur-Nissim attack does not require any additional side information.

The exact details of this attack is beyond the scope of this book chapter, but it is worth-while remembering the take-home message in layman's terms:  

>`"Revealing too much information about a dataset too accurately allows the dataset to be blatantly reconstructed!"`


For this reason, it is to be expected that any algorithm that comes with valid privacy guarantees under *any meaningful definition of privacy* will have to have a price to pay in terms of its utility. The primary focus of research in privacy is to quantify the precise privacy-utility tradeoff and achieves what is information-theoretically possible. This is the theme that we will revisit again and again in the remainder of the book chapter.


