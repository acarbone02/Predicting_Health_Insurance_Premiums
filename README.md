# PSTAT 131: Predicting Health Insurance Premiums
This repository contains my Machine Learning project I created for **PSTAT 131** when I was a student at UCSB. The final product was developed over the course of two months *(from 1/16/23 to 3/19/23 or the Winter 2023 semester)*, and received an A. The main goal of the project was to apply at least four machine learning processes learned in class to real world data. For my case, I choose to examine the National Health Interview Survey (NHIS) from the CDC and tried to predict if any of the predictors correlated to a price tag of health insurance premiums.

## Project Description
This project was inspired by the insurance sites I'd often see when researching the topic. There was always a quick 'premium calculator' that took the inputs of your age, health condition, job, and whether you smoked, and gave an estimate of what you would pay. Of course, you would have to speak to a representative for an actual reliable price, but it was this *tool* that got me thinking: ***"Can health premiums really be expressed through machine learning algorithms given the right data?"***

My hypothesis lead me to sort through the CDC's NHIS 2019 data to find out. Note that I intentionally choose 2019 to be the most recent data, disincluding subsequent years focused on COVID-19. There was also no guarantee that the format of prior years would follow the same formatting and variables. It seemed to be fine as the number of observations was close to 32 thousand and had 534 variables. Looking through the dataset, I concluded that the best variable to predict was ***HICOSTR1_A*** or the annual payment of health insurance premiums to private entities.

With a skimmed dataset and re-encoding of variables (which can be found in the **Processed** folder), I then choose a 75/25 split for the training and testing sets and stratified the response variable. In the recipe I created, I elected to create some interactions between predictors I felt were related and normalized everything. Finally, I cross-validated the training sets into five partitions to avoid overfitting and due to the number of observations present.

I then chose five machine learning processes. I wanted to encompass a wide variety of different approaches, ranging from simple to complex, in hopes of gauging where the response variable laid. What I selected was simple linear regression, k-nearest neighbors, elastic net, decision trees, and random forests. To avoid having to re-run these models (especially for random forests), I made sure to store the results of each fit into rda files.

What I found was random forests had the highest training r-squared score, but clocked in at **0.2295**. With such a r-squared score in the training set, the testing set r-squared score could only minimally increase, ending at **0.2426**. This meant that despite the data being encompassing, it was not conclusive/relative to answer the hypothesis. This result was well within in my expectations, since I knew the premiums themselves are governed by other external pressures other than the individuals applying. While my hypothesis is not proven to be true, I can't deny that some aspects do play into the pricing. It is ultimately the contractor following company policies and looking at your provided health data to determine the suitable cost to cover you.

Nonetheless, this project to me was a success in linking machine learning processes to real world data despite the final results. **Lots of things can be modified like the algorithms used, the recipe, predictors chosen and re-encoded, how the data was split, or even the data used.** If I come back to this project, or if someone wants to take a shot, these key areas are what I suggest would be the biggest improvements moving forward.

## Project Download
Accessing the project's code requires R (4.3) and RStudio (IDE) to view. R can be downloaded from their homepage: https://cran.r-project.org/ and RStudio likewise: https://posit.co/. Additionally, this project uses packages to introduce framework of machine learning processes in order to properly predict. The packages used in this project are: 

| Package  | Purpose |
| ------------- | ------------- |
| **knitr**  | Used for tables/plots in pdf form |
|  **tidyverse** | Provides tools used to clean, present, and manipulate data better |
| **tidymodels**  | Provides tools used to make recipes, framework, and indicators for machine learning |
|  **corrplot** | Used to create a correlation matrix between all predictors |
|  **ggplot2** | Introduces stylizable plots with greater detail |
|  **rpart.plot** | Provides framework for decision trees |
|  **ranger** | Provides framework for random forests |
|  **vip** | Adds Variance Importance Plots for machine learning processes |
|  **doParallel** | Overrides R's default CPU core limit and allows for parallel processing  |

In the repository, you should find four folders:
- The **Images** folder contains the two images used in the preamble.
- The **Processed** folder contains the skimmed version of the dataset that is used throughout the code. It should also have a pdf/cookbook explaining all the predictors.
- Likewise, the **Unprocessed** folder is the unedited data taken straight from the CDC homepage and includes their cookbook and summaries. It is a *zip file*, since the actual data was quite large.
- The **RDA-Files** folder contains all the rda files storing each machine learning processes' results

If you are viewing this on a device unable to run R, an html file is also provided, organizing all findings in tabbed sections. I'd recommend to view this project in that state since it will automatically open in any browser and walk you through the project. If you however want to run the code, then the Rmd file is provided as well.

## Limitations
The hypothesis should be apparent. Afterall, health insurance providers are not allowed by law to proactively change insurance premiums upon the discovery of an illness or health condition. Not to mention, the cost of health insurance premiums may be affected by national/regional laws, subsidized by government health acts like Medicare, or be a straight flat monthly fee with no correlation to the contractees that sign. 

The next issue is the usability of the data itself. Since the data comes from a survey, it has to be privatized by law to not leak confidental details of survey takers. The way the CDC approached this was by encoding the data to indicator numbers. The problem with this is that this survey is almost all qualitative questions. That means out of the 534 predictors derived from questions, you would have to manually identity which were qualitative and which were quantitive, and then interpret the qualitative predictors to follow a uniform scale. This by far was the most frustrating aspect of working with the data, especially since the encoding was not consistent.

With such encoding, the machine learning processes suffer. Usually with machine learning, you work with data that is mostly quantitative. The numerical range of quantitative predictors allows for machine learning processes to precisely narrow its prediction better. Qualitative predictors are fine, so long as they do not outnumber quantitative predictors or are used to predict a qualitative result. The final dataset I use however, is composed primarily of qualitative predictors and is trying to predict a quantitative result. It is not a surprise that the r-squared scores were poor.

We did not also have to achieve a good goodness of fit score (or rsq) to be successful. The reason for this was research bias; if low r-squared scores were being produced, then the person developing may have an incentive to modify predictors to get better results (like p-hacking). This may result in a large amount of case studies with good r-squared scores showing what does correlate, but obscures the bad scores and what does not correlate. My case falls in the latter, but allowed me to demonstrate my final results.

## Disclaimer
This project is for the purposes of demonstrating how one would machine learning processes to multivariable data. The health data itself comes from the NHIS, a public national health survey conducted by the CDC, and does not disclose the personal information of any resident in the United States of America. The data is already privatized by the CDC such that any person is allowed to view and draw conclusions from it. 

I also mention that health insurance premiums may be influenced by the person's health disclosed to the insurer. This is just an allusion to my hypothesis in seeing whether there is actual evidence. Of course, I can not reasonably prove this actually occurs, since no corporate entities by name are mentioned in the data, nor in the project. This project does not aim to expose/slander any insurance institution, it just serves to poke curiousity at an obvious question. I am just a student praticing machine learning. 

If you are a student that is taking PSTAT 131, please do not copy/plagarize my work. Feel free to use the same dataset (since its public) and pose a different hypothesis, but don't directly copy the code.

# Credits
This was a solo project implemented by me, Alexander Carbone. All machine-learning concepts and advisory came from Professor Katie Coburn's Winter 2023, PSTAT 131 STAT MACHINE LEARN course at the University of California, Santa Barbara. Thank you Professor for happily and enthusiastically teach this course, you made this course very enjoyable to take. The health survey data, alongside the cookbook and supplementary pdfs, were conducted by CDC and can be found here: https://www.cdc.gov/nchs/nhis/2019nhis.htm. All data belongs to them.
