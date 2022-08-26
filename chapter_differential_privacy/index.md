# Differential Privacy in Machine Learning
:label:`chap_dp`


**Yu-Xiang Wang** (*UC Santa Barbara / Amazon*)


Machine learning (ML) methods need training datasets to work. Access to task-specific datasets is often taken for granted in typical ML applications. In sensitive applications such as those in healthcare, finance and legal context, however, access to the datasets involving human subjects has been increasingly limited due to various privacy concerns. 

Recent regulations such as the General Data Privacy Regulation (GDPR) in the European Union and the California Consumer Privacy Act (CCPA) have posed steep obstacles for the industry to have access to (their own!) user data for research and product using machine learning. Even in the seemingly benevolent applications where Personal Identifiable Information (PII) is removed from data and only aggregate statistics are revealed, there had been practical attacks that can confidently re-identify individuals or even reconstruct their sensitive data.

Differential privacy (DP) (Dwork et al., 2006) is one of the most promising approaches towards addressing the privacy challenges in the era of artificial intelligence and big data. It is a formal mathematical definition that provides provable guarantees in addressing the aforementioned privacy concerns, thus enabling machine learning for sensitive applications. Recently, DP is going through an exciting transformation from a theoretical construct into a practical technology. Both the private and public sectors are investing heavily in differential privacy research and building them into products.

In this chapter, we will cover the basics of differential privacy and with a focus on its applications to machine learning. By studying this chapter, you will develop sufficient theoretical understanding of DP to correctly interpret its guarantees and gain working hands-on experience of incorporating DP for machine learning applications using open source packages such as ```autodp``` and ```opacus```. Moreover, you will learn to distinguish when DP is a good fit for each application and when not, as well as to explain the semantics of DP to people with variously level of technical backgrounds. 

One unique aspect of the D2L's DP chapter comparing to existing treatments to DP and machine learning with DP is that you will be provided with runnable code blocks with actual ```autodp``` implementation of the DP mechanisms, which you can plug into your own application. The implementation will remain up to date and allow your application to get the benefit from the latest and greatest in modern DP accounting. 

 

```toc
:maxdepth: 2

privacy_challenges
dp_definition
dp_mechanisms
dp_composition
autodp
dpml_intro
dp_linear_regression
dp_logistic_regression
noisygd
noisysgd_dpdl
hyperparameters
future_trend
```
