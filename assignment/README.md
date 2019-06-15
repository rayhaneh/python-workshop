## Introduction
For this assignment, a data set provided (`assignment-data.csv`) which contains a list of claims submitted to a company in 2018. It has 100K rows and the following 11 columns:
- `transaction_date`
- `uploader`
- `upload_date`
- `merchant`
- `amount`
- `tax_type`
- `tax_rate`
- `tax_amount`
- `receipt_image`
- `approver`
- `approval_date`

The data is sorted by `upload_date`.

In this assignment, you need to explore the data against 4 potential fraud cases. For each fraud case, a starter file is provided in which all the followings are imported and configured:
- the data set
- all necessary packages
- a helper validation function
- a helper tweet function


## Fraud Cases
### Case 1: Claims just below an approval threshold
Assuming that the signing limit of a company is $500. If someone was trying to defraud the company, they'd probably want to keep the payment amount below this threshold. To identify this type of fraud, write a program that:
- finds a list of unique claimants (`uploader` column)
- loops through the list of unique claimants and for each claimant
   * finds all submitted claims
   * finds the number of claims between $490 and $500 (sum of `amount` and `tax_amount`)
   * and calculates percentage of claims just below the threshold
- ranks claimants by those with a high percentage of claims just below the approval threshold

Starter file: [`assignment_fraud_case_1.ipynb`](./assignment_fraud_case_1.ipynb)

### Case 2: Rounded Amount Invoices
People who commit fraud often create invoices with rounded amounts, which are invoices without pennies. To explore the data set for any fraud of this nature, write a program that:
- finds a list of unique claimants (`uploader` column)
- loops through the list of unique claimants and for each claimant
   * finds all the submitted claims
   * finds the number of claims without pennies (`amount` column in the dataset)
   * calculates the percentage of rounded-amount claims
- ranks the claimants by those with a high percentage of rounded-amount claims

Starter file: [`assignment_fraud_case_2.ipynb`](./assignment_fraud_case_2.ipynb)

### Case 3: An increase in claim volume
Rapid invoice volume increases may indicate that fraudster has become more confident in stealing money. One way to identify this type of fraud is to calculate the percentage of increase in claims compared to first month. For example, if a person submitted 5 claims in the first month and 25 in another, the percentage of increase compared to the first month is 400%. To explore the data set for any fraud of this nature, write a program that
- finds a list of unique claimants (`uploader` column)
- loops through the list of unique claimants and for each claimant
   * finds all the submitted claims
   * find all the months in which claimant made a claim
   * loop through the months and count the number of claims per month
   * calculate the percentage of increase compared to the first month
   * checks if the percentage of increase in claim volume is larger than a threshold (let’s assume 500%) in any month
   * prints a message for further investigation if the percentage of increase is above the threshold
   * visualizes the percentage of increase by month for the suspicious claimants

Starter file: [`assignment_fraud_case_3.ipynb`](./assignment_fraud_case_3.ipynb)


### Case 4: Discrepancy between the submitted data and the receipt
OCR can be used to identify any discrepancy between the data that is submitted and the receipt. To explore the data set for fraud of this nature, write a program that:
- loops through the first 10 claims in the data set and for each claim data
   * opens the receipt_image for each claim
   * run the receipt images through OCR
   * compares the information on the receipt with those in the data set (limit this comparison to `amount` and `tax_amount` columns)
   * print a message whenever a discrepancy is found

Starter file: [`assignment_fraud_case_4.ipynb`](./assignment_fraud_case_4.ipynb)


## Cheat Sheet
- To create a new empty pandas data frame (`data`) with 3 columns:

   ```
   data = pandas.DataFrame(columns = ['column_name_1', 'column_name_2', 'column_name_3'])
   ```

   Example:

   ```
   data = pandas.DataFrame(columns = ['first_name', 'last_name', 'age'])
   ```

- To add a row to a pandas dataframe (`data`):

   ```
   data = data.append({'column_name_1': column_value_1, 'column_name_2': column_value_2}, ignore_index=True)
   ```

   Example:

   ```
   data = data.append({'first_name': 'John', 'age': 22}, )
   ```

- To get unique values from a column in Pandas dataframe (`data`):

   ```
   unique_values = data['column_name'].unique()
   ```

   Example:

   ```
   unique_names = data['name'].unique()
   ```

- To sort a pandas dataframe (`data`) by a one or more columns:

   ```
   sorted_data = data.sort_values(by=['column_name_1', 'column_name_2'], ascending=False)
   ```

   Example:

   ```
   sorted_date = data.sort_values(by=['last_name', 'age'], ascending=False)
   ```

- To get the month from a date column in a pandas dataframe:

   ```
   data['new_column_name'] = pandas.to_datetime(data['date_column_name']).dt.month
   ```

   Example:

   ```
   data['transaction_month'] = pandas.to_datetime(data['transaction_date']).dt.month
   ```

- To round a floating point number (`num`) to `n` digits after the decimal point:

   ```
   rounded_num = round(num, n)
   ```

   Example:

   ```
   rounded_num = round(23.45198, 2)
   ```

- To create lowercased string from the given string (`string`):

   ```
   lowercased_name = string.lower()
   ```

   Example:

   ```
   string = 'Python Data Analysis'
   lowercased_name = string.lower()
   ```