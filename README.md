# Profit Margin Validation and Prediction with AMECO

## Table of Contents
1. [Overview](#Overview)
2. [Introduction](#Introduction)
   2.1 [AMECO](#AMECO)
   2.2 [Problem Statements](#Problem-Statements)
   2.3 [Project Goals](#Project-Goals)
   2.4 [Data](#Dataset)
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

Our client, AMECO, a construction site services company, desires to the stickiness of current 


### AMECO Background <a name="AMECO"></a>

This Capstone project is in collaboration with AMECO, a construction site services company. 


### Problem Statements <a name="Problem-Statements"></a>

### Project Goals <a name="Project-Goals"></a>

Our first goal is to validate their current profit margin. The idea is to find the profit margin for each product class and compare it with target margin.

### Data <a name="Dataset"></a>

## Profit Margin Validation <a name="Profit-Margin-Validation"></a>

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

