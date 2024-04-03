# Profit Margin Validation and Prediction with AMECO

## Table of Contents
1. [Overview](#Overview)

2. [Introduction](#Introduction)
2.1 [AMECO](#AMECO)
   2.2 [Problem Statements](#Problem-Statements)
   2.3 [Project Goals](#Project-Goals)
   2.4 [Data](#Dataset)
       2.4.1 [Data Cleaning](#Data-Cleaning)
3. [Profit Margin Validation](#Profit-Margin-Validation)
   3.1 [Methods](#Validation-Methods)
   3.2 [Results](#Validation-Results)

4. [Profit Margin Prediction](#Profit-Margin-Prediction)
   4.1 [Methods](#Prediction-Methods)
       4.1.1 [Machine Learning Model](#Machine-Learning-Model)
       4.1.2 [Time Series Model](#Time-Series-Model)
   4.2 [Results](#Results)
       4.2.1 [Model Results](#Model_Results)
       4.2.1 [Model Comparison](#Model_Comparison)

5. [Conclusion](#Conclusion)

6. [Resources](#Resources)

7. [Contributors](#Contributors)


## Overview <a name="Overview"></a>

## Introduction <a name="Introduction"></a>

In the business world, profit margin serves as a critical measure of both overall business efficacy and product performance. This metric is derived by employing the formula: (Revenue - Cost) / Cost. A higher profit margin typically signifies a stronger return on the entire business operation, and a high margin on a specific product indicates a substantial return on that particular item. Conversely, a lower profit margin suggests a less favorable return. Additionally, examining historical profit margins can offer valuable insights for future pricing strategies. For instance, should a product consistently yield a profit margin of 12%, any increase in costs may necessitate an adjustment in its selling price to maintain financial stability and profitability. Consequently, companies establish a general target profit margin for the company and specific profit margins for each product, setting prices accordingly based on cost and desired profit margin. In practice, however, salespersons may not always adhere strictly to these target profit margins. Factors such as market competition, customer bargaining power, and promotional strategies often influence the final selling price, implying a flexible and strategic approach to pricing. 

<img src="https://github.com/PomeloWu99/Capstone/blob/main/05%20Supplementary/pm_demo.png" alt="alt text" height="400" width="600"/>
Credit To: <a href="https://www.investopedia.com/terms/p/profitmargin.asp">Investopedia</a>

</br>Our client, AMECO, a construction site services company, currently undergoing more losses than they expected, desires to examine whether the actual profit margin for each product class has met its target profit margin over the last four years. They also aim to understand how can they price better to gain more profits. 


### AMECO Background <a name="AMECO"></a>

This Capstone project is in collaboration with AMECO, a construction site services company. It operates across different regions in the United States and primarily sells construction goods and welding equipment. Under these two major categories, each has hundereds of product lines. For instance, construction goods contain a product line called safety tools. Within each product line, there are dozens of products, for example, Hand Tools Plumb Bobs within the safety tools.

The pricing of each product is primarily determined by its target profit margins and customers' loyalty level. There are three customer's loyalty level, `Good`, `Better`, and `Best.` Each customer category has slightly different target profit margins with the `Best` customer category has the lowest profit margins, then `Better` customer category, and finally `Good` customers. Product prices are then determined based on the target.

### Problem Statements <a name="Problem-Statements"></a>

As salepersons might not strictly adhere to the selling price calculated by the target profit margins, AMECO wants to identify if there are significant magnitude of differences between the actual and target profit margins, and if these difference contributes to its profit margins to be overall lower. Additionally, they want to check if the current profit margins are optimal and reasonable to operate their business on. 

### Project Goals <a name="Project-Goals"></a>

Based on the above problems, our project goals are two-fold. Our first goal is to validate their current profit margins. The idea is to find the profit margin for each product class and compare it with the corresponding target profit margin. After validating the current profit margins, if we find any differences, we want to find a reasonable profit margin for each product class. To achieve this, we intend to build a model for each product class to predict its profit margins and compare such with the target profit margins. Through these processes, we can help solve AMECO's concerns on their current profit margin performances and find better alternatives.

### Data <a name="Dataset"></a>

Our original dataset spanning from 2016 to 2023 contains 1,155,850 rows and 45 fields. These 45 fields can be categorized into 3 major categories, including product information, pricing information, and other information. Wihtin product information, we have `product category`, `product class`, `specific item` names and all corresponding number identification, `date of transaction`, `stock status`. Within pricing information, we have `quantity`, `cost`, `customer categories`, and `prices`. We also have some available information about `geographics`, `buyer companies`, and `salespersons`.

The original dataset, however, has many missing information. AMECO underwent a system migration in 2019; as a result, the geographic data is missing prior to 2020. The dates of transaction prior to 2020 are coalesced into the 01-01. 

We also obtain two other datasets, one with more detailed client information with company and corresponding customer category, and the other one with target profit margins for each product class in 2023.

#### Data Cleaning <a name="Data-Cleaning"></a>

1. Data Quality Check & Missing & Imputation

We first checked each column with missing information, and tried to come up with an imputation method to fill in those missing information. 

We examined the customer information, including `customer number`, `customer name`, and `customer category.` Initially we found the customer number and customer name were not one-on-one relationship, and then we enforced a consistent customer number format and stripped all additional punctuations from the customer name column. Then we paired these two fields and impute those with missing values. Finally we merged the updated customer category information from AMECO and obtained complete and quality data for `customer number`, `customer name`, and `customer category.`

We then examined the product information. Half of the product category and product class are missing in the original dataset, however, we did have complete product number information. As a result, we used the mode imputation because the product category only has two major categories and it will be straightforward and reasonable to fill in based on mode values. As for the product class we first tried to fill in missing information through pairing. We paired the item number with existing product class and category, and used this to infer information. For those that are still missing, we then used mode imputation.

Finally, we also filled in stock status information based on our client suggestions and used two complementary columns strikeforce flag and stock. The stock is the primary indicator and for those missing stock information, we used strikeforce flag to fill in stock status. The remaining ones are automatically deemed 'in-stock' because this is a more common case.

2. Data Fields Selection

Based on our project goals, we limited the time span from 2020 to 2023 to obtain valid and valuable data for analysis. Additionally, we utilized our client's domain knowledge to select out important fields, including `product category`, `product class`, `specific item`, `date of transaction`, `quantity`, `cost`, `customer categories`, and `prices` in our profit margin validation and prediction processes.

3. Data Manipulation

In the dataset, we have completed date information such as '2023-04-16' and we retrieved `Year` `Month` `Quarter` and `Previous Quarter` to prepare for date analysis.

We also marked AMECO's sub companies to boolean value and stored it to a column called `Own` because we believed the selling prices to sub companies are biased.

Finally, we also calculated the profit margin for each transaction. The formula is (price * quantity - cost * quantity)/price * quantity, here we can take out the quantity and calculated it as (price - cost)/price.

Eventually we created a new dataset 568,081 rows with 17 columns (`Customer Name`, `Product Category`, `Own`, `Year`, `Month`, `Quarter`, `Prev Quarter`, `Date`, `Group`, `Product Class`, `Specific Item`, `Quantity`, `Cost`, `Price`, `State`, `Stock`,`Profit Margin`)

![alt text](https://github.com/PomeloWu99/Capstone/blob/main/05%20Supplementary/table_demo.png)
This table randomly sampled 10 rows for demonstration purpose. 

## Profit Margin Validation <a name="Profit-Margin-Validation"></a>

Our first step is to validate current profit margins for each product class.

### Methods <a name="Validation-Methods"></a>

For each transaction row, we calculate the profit margin based on (price-cost)/price since the quantity will be removed from our formula. Then we took the median of each product class in different years.

### Results <a name="Validation-Results"></a>

![image](https://github.com/PomeloWu99/Capstone/assets/100142240/5d6e840d-ffe9-499e-a462-38654aa6ebdb)

## Profit Margin Prediction <a name="Profit-Margin-Prediction"></a>

### Methods <a name="Prediction-Methods"></a>

#### Machine Learning Model <a name="Machine-Learning-Model"></a>

#### Time Series Model <a name="Time-Series-Model"></a>

### Results <a name="Results"></a>

#### Model Results <a name="Model-Results"></a>

#### Model Comparison <a name="Model-Comparison"></a>

