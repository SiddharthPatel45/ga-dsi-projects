# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 1: SAT & ACT Analysis

This is the first project done as part of the General Assembly's Data Science Immersive in May 2021.

## Problem Statement

The data provided contains the SAT and ACT standardization test scores & participation rates for each state in the United States from 2017 & 2018. The goal is to make a recommendation to the College Board (the administer of SAT), based on our analysis of the data, to improve the participation rates in certain states of interest.

## Executive Summary

In this project, we work with data containing the test scores and participation rates for the two standardization tests, SAT & ACT, conducted in the US and mandated by many universities and colleges as part of their admission requirements. The datasets provided had state-wise mean values for the following features-
- SAT datasets: State, Participation Rate, Math & Evidence-Based Reading and Writing, and Total scores.
- ACT datasets: State, Participation Rate, Math, Science, Reading, English, and Composite scores.

After importing all the data into the code, an initial visual inspection revealed that the data was complete and that there were no null values. Each dataset had all the states' info and thus a comparison study can be done to understand certain trends. However, there were some anomalies with the datatypes which were addressed along the way. After cleaning and verifying, all datasets were merged into a single file to perform 
Exploratory Data Analysis (EDA) as well as plot the trends.

Frequentist inferences were drawn from the datasets to look for any underlying relationships between the participation rates and states. There were a few interesting observations that are analysed for reasoning. An interesting highlight was the _uncanny_ resemblence of states' political alignment and it's preference for SAT/ACT. Finally, the conclusions and recommendations were listed at the end.

## Data Dictionary

The four datasets for SAT & ACT for 2017-2018 were cleaned and combined into a single file, that was used to perform the EDA and plot analysis. The features of the dataset and their properties are listed below.

#### Data dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|_object_|2017 ACT/SAT|All the 50 states of the US and District of Columbia|
|sat_2017_participation|_int_|2017 SAT|Participation percentage for SAT 2017|
|sat_2017_ebrw|_int_|2017 SAT|Average Evidence-Based Reading and Writing score for SAT 2017 (between 200~800)|
|sat_2017_math|_int_|2017 SAT|Average Math score for SAT 2017 (between 200~800)|
|sat_2017_total|_int_|2017 SAT|Average Total score for SAT 2017 (between 400~1600)|
|act_2017_participation|_int_|2017 ACT|Participation percentage for ACT 2017|
|act_2017_english|_float_|2017 ACT|Average English score for ACT 2017 (between 1~36)|
|act_2017_math|_float_|2017 ACT|Average Math score for ACT 2017 (between 1~36)|
|act_2017_science|_float_|2017 ACT|Average Science score for ACT 2017 (between 1~36)|
|act_2017_reading|_float_|2017 ACT|Average Reading score for ACT 2017 (between 1~36)|
|act_2017_composite|_float_|2017 ACT|Average Composite score for ACT 2017 (between 1~36)|
|sat_2018_participation|_int_|2018 SAT|Participation percentage for SAT 2017|
|sat_2018_ebrw|_int_|2018 SAT|Average Evidence-Based Reading and Writing score for SAT 2017 (between 200~800)|
|sat_2018_math|_int_|2018 SAT|Average Math score for SAT 2017 (between 200~800)|
|sat_2018_total|_int_|2018 SAT|Average Total score for SAT 2017 (between 400~1600)|
|act_2018_participation|_int_|2018 ACT|Participation percentage for ACT 2017|
|act_2018_english|_float_|2018 ACT|Average English score for ACT 2017 (between 1~36)|
|act_2018_math|_float_|2018 ACT|Average Math score for ACT 2017 (between 1~36)|
|act_2018_science|_float_|2018 ACT|Average Science score for ACT 2017 (between 1~36)|
|act_2018_reading|_float_|2018 ACT|Average Reading score for ACT 2017 (between 1~36)|
|act_2018_composite|_float_|2018 ACT|Average Composite score for ACT 2017 (between 1~36)|


## Conclusions and Recommendations

After analysing, plotting, analysing again and finding some studies on the topic, it can be concluded that the nation-wide trends and states' own policies and preferences are a good predictor of the participation rates for the SAT and ACT tests. Recently, many universities and colleges across the country have opted to remove the standadization tests, both SAT & ACT, from their admission requirements but that has not stopped students from taking either or even both tests.

Many have postulated that the SAT & ACT scores are a good predictor of the students' GPA in the freshmen year ([source](https://www.forbes.com/sites/evangerstmann/2020/05/23/dropping-the-sat-and-act-is-about-politics-not-diversity/?sh=3086520c2948)). Alternatively, it has also been pointed out that having this tests as requirements is a hurdle for many low-income households, or people from minorities, or first-gen immigrants. Universities, by removing these requirements, are eliminating barriers to such candidates and open their doors to a wider diversity & talent. The argument, on the contrary, as stated in this [report](https://senate.universityofcalifornia.edu/_files/underreview/sttf-report.pdf), is that the standardization test scores promote minority students and gives them a path to succeed at good schools.

The College Board has taken some steps to improve the SAT participation rates in the United States, which have proven quite helpful in getting the rates up in some states. Take Based on the analysis conducted above, it can be recommended to increase the collaborations with schools to organize the "school days", which are the days on which the SAT is conducted on-campus, is free of charge, and the school conducts them. Moreover, the deals with individual states helps to incentivise promotion of SAT, as then the public schools don't have to spend extra budget on having to give the SAT for free to its students. These deals can also include helping schools take PSAT, as in _Illinois_, for 9th and 10th grade students so they become comfortable with the format. The College Board can also partner with schools and other tutoring centres to provide low-cost or free SAT preparation material to boost students' support and confidence in the test.

Take _North Dakota_, for instance, the state has mandated ACT as its prefered test for seniors and has a state-wide test for the juniors. In 2018, the state was granted one-of-a-kind permission to- "_to use a new kind of testing flexibility in federal law: the right to let school districts substitute the ACT for the state’s own required high school assessment._" ([source](https://www.edweek.org/policy-politics/north-dakota-is-first-state-to-let-districts-use-act-instead-of-state-exam/2018/03)). The state wants to follow the national trend of conducting fewer types of tests so students can focus more in class. In order to facilitate the state to switch to SAT, the College Board can work with the state authorities to do a technical review, a federal requirement to choose one of the national tests. Along with the recommendations above, this can really help the College Board get higher participation for SAT in the state.

Some other conclusions and inferences from the plots and analysis above can be summarized below as-
- Increase in participation rates in a state will result in decrease in the final score of the test, showing a negative correlation.
- Most of the states have a preference for one of the tests, and it has an uncanny resemblence to the politcal alignment on the map of United States.
- All the variables in this study had bimodal distribution.
- ACT is preferred more than SAT in many states but SAT is slowly getting more popular.
- There were four states in 2017 that had more than 50% participation in both SAT & ACT, and five states in 2018.

Lastly, a deeper study into the reason behind why states choose SAT over ACT, or otherwise, and why universties are opting to remove them from their admission requirements can be done.

## References

[1]. https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/

[2]. https://www.act.org/content/dam/act/unsecured/documents/cccr2017/ACT_2017-Average_Scores_by_State.pdf

[3]. https://newsroom.collegeboard.org/more-2-million-students-class-2018-took-sat-highest-ever

[4]. https://collegereadiness.collegeboard.org/pdf/guide-2018-act-sat-concordance.pdf

[5]. https://www.collegeraptor.com/getting-in/articles/act-sat/preference-act-sat-state-infographic/

[6]. https://time.com/4561625/electoral-college-predictions/

[7]. https://chicago.chalkbeat.org/2018/7/27/21105418/illinois-has-embraced-the-sat-and-the-act-is-mad-about-it

[8]. https://www.chicagotribune.com/news/breaking/ct-met-illinois-act-test-scores-20181016-story.html

[9]. https://www.testive.com/colorado-sat-change-2017/

[10]. https://www.orlandosentinel.com/news/education/os-ne-act-sat-florida-scores-20181024-story.html

[11]. https://www.forbes.com/sites/evangerstmann/2020/05/23/dropping-the-sat-and-act-is-about-politics-not-diversity/?sh=3086520c2948

[12]. https://senate.universityofcalifornia.edu/_files/underreview/sttf-report.pdf

[13]. https://www.edweek.org/policy-politics/north-dakota-is-first-state-to-let-districts-use-act-instead-of-state-exam/2018/03