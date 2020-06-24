# Segmentation-of-Credit-Card-Customers

## Table of Content
  * [Directory Tree](#directory-tree)
  * [DATA AVAILABLE](#data-available)
  * [BUSINESS CONTEXT](#business-context)
  * [EXPECTATIONS FROM THE TRAINEES](#expectations-from-the-trainees)
  * [DATA DICTIONARY](#data-dictionary)
  * [LICENSE](#license)

### Directory Tree

```
├── CC_GENERAL.csv
├── Credit_new_cust.xlsx
├── Profiling_output.csv
├── Segmentation of Credit Card Customers.ipynb
├── pandas_profiling.html
├── python_FA.xls
├── LICENSE
├── README.md
```

### DATA AVAILABLE: 

 CC GENERAL.csv 

### BUSINESS CONTEXT: 

This case requires trainees to develop a customer segmentation to define marketing strategy. The sample dataset summarizes the usage behavior of about 9000 active credit card holders during the last 6 months. The file is at a customer level with 18 behavioral variables.   Expectations from the Trainees:  

### EXPECTATIONS FROM THE TRAINEES: 

 Advanced data preparation: Build an ‘enriched’ customer profile by deriving “intelligent” KPIs such as:  
 Monthly average purchase and cash advance amount   
 Purchases by type (one-off, installments)   
 Average amount per purchase and cash advance transaction,  
 Limit usage (balance to credit limit ratio),  
 Payments to minimum payments ratio etc.  
 Advanced reporting: Use the derived KPIs to gain insight on the customer profiles.  
 Identification of the relationships/ affinities between services.  
 Clustering: Apply a data reduction technique factor analysis for variable reduction technique and a clustering algorithm to reveal the behavioural segments of credit card holders  
 Identify cluster characterisitics of the cluster using detailed profiling.  
 Provide the strategic insights and implementation of strategies for given set of cluster characteristics  
 
### DATA DICTIONARY: 
 
<b>CUST_ID:</b> Credit card holder ID   
<b>BALANCE:</b> Monthly average balance (based on daily balance averages)   
<b>BALANCE_FREQUENCY:</b> Ratio of last 12 months with balance   
<b>PURCHASES:</b> Total purchase amount spent during last 12 months   
<b>ONEOFF_PURCHASES:</b> Total amount of one-off purchases  
<b>INSTALLMENTS_PURCHASES:</b> Total amount of installment purchases   
<b>CASH_ADVANCE:</b> Total cash-advance amount   
<b>PURCHASES_ FREQUENCY:</b> Frequency of purchases (Percent of months with at least one purchase)   
<b>ONEOFF_PURCHASES_FREQUENCY:</b> Frequency of one-off-purchases   
<b>PURCHASES_INSTALLMENTS_FREQUENCY:</b> Frequency of installment purchases   
<b>CASH_ADVANCE_ FREQUENCY:</b> Cash-Advance frequency   
<b>AVERAGE_PURCHASE_TRX:</b> Average amount per purchase transaction   
<b>CASH_ADVANCE_TRX:</b> Average amount per cash-advance transaction   
<b>PURCHASES_TRX:</b> Average amount per purchase transaction   
<b>CREDIT_LIMIT:</b> Credit limit   
<b>PAYMENTS:</b> Total payments (due amount paid by the customer to decrease their statement balance) in the period   
<b>MINIMUM_PAYMENTS:</b> Total minimum payments due in the period.   
<b>PRC_FULL_PAYMEN:</b> Percentage of months with full payment of the due statement balance   
<b>TENURE:</b> Number of months as a customer   

### LICENSE

[MIT License](https://github.com/vicky60629/Segmentation-of-Credit-Card-Customers/blob/master/LICENSE)

Copyright (c) 2020 Vicky Gupta

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
