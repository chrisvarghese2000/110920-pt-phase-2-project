# King County Home Price Analysis

This repository offers an analysis of factors that influence housing prices in King County, WA

## This Repository

### Repository Directory

```
├── README.md        <-- Main README file explaining the project's business case,
│                        methodology, and findings
│
├── data             <-- Data in CSV format
│   ├── processed    <-- Processed (combined, cleaned) data used for modeling
│   └── raw          <-- Original (immutable) data dump
│
├── notebooks        <-- Jupyter Notebooks for exploration and presentation
│   ├── exploratory  <-- Unpolished exploratory data analysis (EDA) notebooks
│   └── report       <-- Polished final notebook(s)
│
├── references       <-- Data dictionaries, manuals, and project instructions
│
└── reports          <-- Generated analysis (including presentation.pdf)
    └── figures      <-- Generated graphics and figures to be used in reporting
```

### Quick Links

1. [Final Analysis Notebook](notebooks/exploratory/report/Final_Book.ipynb)
2. [Presentation Slides](reports/KC_Presentation.pdf)

### Setup Instructions

TODO: add setup instructions (e.g. the name of the Conda environment file)

## Business Understanding

For the average American household, Home is the biggest asset. While many factors come into choosing a home, and certainly differ by prefrence, I want to investigate the relationship that various home-improvement strategies may have on affecting sale price. To do this, I will be examining the properties located in King County from 2019, and will have these three questions in mind in particular. 
- Enclosing a porch will increase the sale price of a home
- Converting a garage to a bedroom is a good way to increase the sale price of a home
- Upgrading to a forced-air heating system will increase the sale price of a home

## Data Understanding

For this project, I used 4 data sets:

EXTR_LookUp.csv
EXTR_Parcel.csv
EXTR_ResBldg.csv
EXTR_RPSale.csv

There are three main data tables and one look up data table. Extra_RPSale.csv is the lengthiest data set as it contains transactions for any property that has occured in King County. Following this is EXTR_Parcel.csv. This data set give various facts about any parcel of land and fact pertaining to this such as topographical features. The third data set is EXTR_ResBldg.csv. This data set contains many fields of interest since it pertains to facts of residential properties such as room, bath count, and square footage.

The first part of my analysis that I would like to point to, is the base of my linear regression model. I started out by examining the various correlations between many parameters of interest and sale price. This can be easily seen in the heatmap I created.
['heatmap hopefully'](references/figures/heatmap.png)
(figure 1)

While this heatmap easily highlights correlations, it is notable that the correlation coefficients are quite low on both the positive and negative spectrum. Because of this, it was a great challenge to even try and create a linear model that attempted to statisfy various assumptions, soley because the relationships in the data were seemingly weak to begin with.

I used the relationship between total sq ft of living space and sale price to begin my model.
['graph of living space and price'](references/figures/livingsp-price.png)
(figure 2)

This data is somewhat trending in a weakly positive, but linear relation. Even though there is a trend, there is the presence of outliers and the data is too spread out to really point out a clear direction. Adding to this model, I utilized the total square ft of porch space and the total square ft of garage space to the sale price. Although these had weaker correlations, I added them to the model since they had decent correlations and they would help me answer my targeted questions.

I wanted to address the significance of heating system and its affect on price, so this is a chart of the various distributions of several heating systems and the corrosponding sale price of its home.
['force air map'](references/figures/forced_air.png)
(figure 3)

This chart shows that there is not a huge amount of variation in pricing between different heating systems.

## Data Preparation

between the 3 data sets containing records, there were only a few parameters in each I was interested in. Since my target was to analyze home improvement strategies, naturally the dataset containing the residential property was the most useful. I utilized most columns from this data frame and used the sales dataset to retrieve pricing and dates and the parcel dataset to get some insight on water and contamination hazards, as well as property type.

After carefully filtering out obsolete columns, I proceeded to ensure that all the data types were in the correct form and that incomplete fields were taken care of. I merged all the data sets using the unique major + minor identification, and filtered data from 2019 that pertained to residential properties. I also refrenced the pdf dictionary to use the look up data set to fill in all unknown numerical parameters.

## Modeling

Since sq ft of living space had the highest correlation, .259, with sale price, this became the first pointer in my base model. I tested out various other pointers such as number of living spaces, number of bedrooms, and number of baths, but these pointers seems to violate independance assumptions. After testing, I was able to increase the R2 value of my model without further violationg anymore assumptions, as well as attempt to address two questions from the three targeted questions since these pointers corrosponded directly with them. These pointers are the total sq ft of porch space and attached garage space. 

## Evaluation

The final regression model uses total sq feet of living space, sq feet of an open porch, and sq ft of an attached garage as pointers for sale price. It explains about 7% of the variation in sale prices for homes in King County. Based on this model, there is statistically significant evidence that, for the data the model explains, every increase in sq ft of living space will increase the sale price by about 336 dollars and every increase in sq ft of porch space will increase the sale price by about 274 dollars. Because the correlations were so low and how small the R2 value was, it was difficult to meet requirements for many tests, however all the variables were reasonably independant so this assumption was not violated.

## Conclusion

Based on the models predictions, it is statistically signficant to say that increasing living space and porch space do add to the value of a home. However, given how low the correlation is and how little of the variation in sale prices that the model represents, I am unable to make any conclusive statements to homeowners. Further analysis is required to explore the relationship between these housing indicators and the actual sale prices. It would be useful to utilize data from 2020 and 2021 as the housing market has changed, as well as consider examining a more diverse area. I would also want to analyze the current appraisals for all of the parcels as opposed to just the sale prices, since this may give me a better insight into the valuation of the home and what indicators will improve this. Further analysis must be done on the impact of a heating system and its role in fluctating the sale price of a home. 
