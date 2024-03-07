---
toc: True
comments: True
layout: post
title: Computing Bias
courses: {'csp': {'week': 12, 'categories': ['4.A']}}
categories: ['C1.4']
---

## <mark>Introduction to Computing Bias</mark>
A brief introduction to computing biases is that human biases are usually incorporated into algorithms or data. If this is confusing to understand, here is one example. When you are browsing Netflix and look at the different categories, you see that typically there are a bunch of Netflix exclusives being displayed more than non-exclusives. This is a form of computing bias as this would benefit Netflix, as the movie or show will never leave Netflix. So, if you get hooked on that show, then you will inevitably keep paying the Netflix subscription.

## <mark>Explicit Data vs Implicit Data</mark>
Many software apps such as Netflix mentioned previous collect a lot of data. There are two types of data that apps collect and they are Explicit and Implicit.

### <mark>Explicit</mark>:
- Examples:
    - Name
    - Adress
### <mark>Implicit</mark>:
- Examples(Netflix):
    - What you watch
    - When you watched
    - Engagement(Watch Retention)
    - Types of movies or shows

## <font color = "ADD8E6">Popcorn Hack 1</font>
Name a software app you know about and name some explicit and some implicit data that they collect from you the user.

Answer: Facebook obtains your email address and some personal information (don't know, never used) and then tracks your connections with other users and viewership of certain content categories.

## <mark>Loan Company Example</mark>
Another bias can be observed in trends. In the context of an app that collects information for loan officers to help them decide who the best candidate is to give a loan to, trends, for example, could show that a certain age group is comprised of better candidates for a loan. This bias is based on trends and data, and it could be beneficial to the loan officers, preventing them from losing money on loans and avoiding complications with the loanee. However, this could be harmful to the candidate applying for the loan because they might be turned away simply because they don't qualify within a certain age or race bracket.

## Example #2
- <mark>Movies</mark>
    - A movie such as Dispicable Me has more of a demographic for younger people. Even though this is a bias is is beneficial because it is content that is specific to someones wants.
    - Movies such as Star Wars are more geared toward older poeple as their target audence in contrary to a cartoon.
- <mark>Video Games</mark>
    - Casual Audience: These games are has a bias towards an audience that want to play casually
        - Candy Crush
        - Minecraft
    - Sweaty Games: These have more of a bias for people that want to get better and play competitively
        - Counter Strike
        - Call of Duty

## <font color = "ADD8E6">Popcorn Hack 2</font>
Give an example of a movie, show, or video game or even a certain softare that has a certain bias and what who the bias is towards

Answer: Scipy Python package is biased towards professional researchers, as its documentation makes use of many advanced statistical terms despite some functions being overall fairly simple to use (e.g. drawing samples from skewed normal distributions).

## <mark>Mitigating Bias in Algorithms</mark>

To address  human biases, programmers must work towards minimizing bias in algorithms used for computing innovations. Software should aim for neutrality, considering all perspectives and actively rejecting inherent human biases.

Key considerations during program development:

- Identify potential sources of bias.
- Assess whether your program is amplifying or intentionally excluding certain elements.
- Solicit feedback from a diverse and widespread group of individuals.
- Contemplate how people who differ from you might utilize your developments.

## Questions to ask About Bias
- In the example of the Loan Company the bias was unintentional but could be potentially excluding fit candidates. In the example of Netflix, the bias of adding exclusives in the front of categories is intentianal but not harmful for anyone. This leads to some questions to ask if you encounter bias in a software.

- <mark>Questions</mark>:
    - Is it enhancing or intentionally excluding?
    - Is the bias intensionally harmful or hateful?
    - Are you receiving feedback from a wide variety of people?

Using these questions, software developers are able to reduce harmful bias in algorithms and data.

## Homework Hacks:
The implementation of a predictive policing algorithm in a city has raised concerns regarding potential biases,leading to disporotionate targeting of specific neighborhoods. This over-policing could result in civil rights violation. Your task is to propose a solution to mitigate this bias and explain the method you'd use to remove computing bias. Make a full paragraph that is at least 4 sentences

Disproportionate targeting in a predictive algorithm usually means that the algorithm's training dataset is inappropriately skewed towards certain elements of the analyzed dataset, since most useful predictive algorithms these days are trainable neural nets and not primitive hard-coded things. To mitigate this bias, the most important action is to retrain the algorithm with a more representative data set - the old one would have to be discarded. In order to collect such a dataset, I would divide neighborhoods based on individual police administrations and harvest a certain fixed number of records from each police station to serve as the new predictive training dataset. This would reduce the biases towards certain neighborhoods because the training sample is no longer overly weighted towards neighborhoods with higher crime rates, and thus the algorithm is less likely to make inappropriate associations between residents of those neighborhoods and criminal activity.
