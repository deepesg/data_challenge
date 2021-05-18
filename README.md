# DEEP ESG Data Processing Technical Challenge

## Introduction

Welcome to the DeepESG data processing test.

The main goal of this exercise is to understand your software development process. The challenge tries to simulate some tasks commonly found in the daily life of a developer in a domain that is also very common in our area of expertise: accounting. But don’t be alarmed, we hope to provide you with all the details and terms necessary for the task!

**We also hope you have fun.**

## The Challenge
As a data-driven startup, having a robust understanding of our primary data source is critical. Serving medium and large companies, we can expect this source to be their accounting data. As such, we often need to create our own data structures representing the financial activity of a customer in question.

Two of the most basic accounting structures of a company are: its [general ledger](https://www.investopedia.com/terms/g/generalledger.asp) and its [chart of accounts](https://www.investopedia.com/terms/c/chart-accounts.asp). In simple terms, we can think of the chart of accounts as an initial categorization and consolidation of a company’s transactions, used later for the structuring of specific reports. Likewise, the general ledger can be understood as a long record of all transactions in a given financial period, having at least two columns: the account number and the financial value of the transaction. *In short, the general ledger is the source of the data being organized in the chart of accounts.* 

**Let's take a look at an example!**

### Example

Consider the following chart of accounts structure containing only one root node (the main consolidated account 1):

```bash
1
├── 1.1  
├── 1.2  
│   ├── 1.2.1  
│   └── 1.2.2  
└── 1.3  
    └── 1.3.1  
        ├── 1.3.1.1  
        └── 1.3.1.3  
```
Below is an example of a general ledger:

|Account number|Value     
| :-: |:-:|
|1.2.1|7|
|1.2.2|8|
|1.1|1|
|1.2.2|2|
|1.3.1.3|10|
|1.3.1.3|6|
|1.3.1.1|2|
|1.2.1|4|
|1.2.1|1|
|1.3.1.3|6|
|1.2.1|9|
|1.3.1.3|10|
|1.3.1.1|8|
|1.3.1.3|9|
|1.1|1|
|1.3.1.1|4|
|1.2.2|7|
|1.3.1.3|7|
|1.2.1|10|
|1.2.2|9|

The consolidation process takes place through the following steps:

#### First step
Add all general ledger’s lines addressed to the accounts 1.1, resulting in a value of 2.

|Account number|Value     
| :-: |:-:|
|...|...|
|**1.1**|**1**|
|...|...|
|**1.1**|**1**|
|...|...|

#### Second step
Add all general ledger’s lines addressed to the accounts 1.2.1, resulting in 31.

|Account number|Value     
| :-: |:-:|
|**1.2.1**|**7**|
|...|...|
|**1.2.1**|**4**|
|**1.2.1**|**1**|
|...|...|
|**1.2.1**|**9**|
|...|...|
|**1.2.1**|**10**|
|...|...|

#### Third step
Add all general ledger’s lines addressed to the accounts 1.2.2, resulting in 26.

|Account number|Value     
| :-: |:-:|
|...|...|
|**1.2.2**|**8**|
|...|...|
|**1.2.2**|**2**|
|...|...|
|**1.2.2**|**7**|
|...|...|
|**1.2.2**|**9**|

#### Fourth step
Add all general ledger’s lines addressed to the accounts 1.3.1.1, resulting in 14.

|Account number|Value     
| :-: |:-:|
|...|...|
|**1.3.1.1**|**2**|
|...|...|
|**1.3.1.1**|**8**|
|...|...|
|**1.3.1.1**|**4**|
|...|...|

#### Fifth step
Add all general ledger’s lines addressed to the accounts 1.3.1.3, resulting in 48.

|Account number|Value     
| :-: |:-:|
|...|...|
|**1.3.1.3**|**10**|
|**1.3.1.3**|**6**|
|...|...|
|**1.3.1.3**|**6**|
|...|...|
|**1.3.1.3**|**10**|
|...|...|
|**1.3.1.3**|**9**|
|...|...|
|**1.3.1.3**|**7**|
|...|...|

#### Sixth step
Populate all chart of account with the sum of the respective account number:

```bash
1
├── 1.1 = 2
├── 1.2  
│   ├── 1.2.1 = 31 
│   └── 1.2.2 = 26
└── 1.3  
    └── 1.3.1  
        ├── 1.3.1.1 = 14
        └── 1.3.1.3 = 48
```

#### Final step
Consolidate the “leave” account’s in the rest of the tree:

```bash
1 = 2 + 57 + 62 = 121
├── 1.1 = 2
├── 1.2 = 57
│   ├── 1.2.1 = 31 
│   └── 1.2.2 = 26
└── 1.3 = 62
    └── 1.3.1 = 14 + 48 = 62
        ├── 1.3.1.1 = 14
        └── 1.3.1.3 = 48
```

**Your challenge is to create a program that receives as input a chart of accounts and a general ledger and as output the chart of accounts populated by the latter.**

### Requirements, specifications and other information 

* The program must be written in python 3+. 
* In the “input” folder you have two example files, general_ledger.xlsx and chart_of_accounts.xlsx. They establish the expected input format. 
* We are not going to force a standard output format. Assume, however, that the output format will be consumed by other processing pipes. 
* Since any serious software development effort demand tests, you must implement them as well. 
* For a small amount of data the examples of input are fine. But how would you handle a massive volume of data? Although we can expect the Chart of Accounts to remain almost constant in size, the General Ledger can grow arbitrarily, making the xlsx format inappropriate. A better solution would be to use a relational database. Can your solution accommodate this case? 

### Criteria 
Some important points to be considered are: 
* **Architecture**. We know that the challenge resolution do not demand rocket science, but can you organize it well an show us your software design approach?
* **Clean code**. Same as above. 
* **Documentation and comments**. 
* **Tests**. 
* **Error handling**.  

### Submission 

Please, create a repository with your solution and send the link to felipe@deepesg.com. Your README.md should explain your decisions (or rationale) to solve the challenge as well as all the instructions required to run your solution and tests in a Linux environment. 

**Good luck!**
