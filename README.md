# GCP 
## Cheat  | Palavras/Serviços chaves
https://github.com/priyankavergadia/google-cloud-4-words

## View Sample Billing Data with BigQuery
Part of working with billing data is working with data exported to BigQuery. In this lab, we are going to view sample billing exports maintained by Google, and conduct queries against a public dataset of billing exports. This will be a fun lab in that we can play around with SQL queries in BigQuery and see what kind of results we can get. Let's get started!

Once you are in your lab project, we will need to get into the BigQuery web console. From the top left menu, scroll down to Big Data, and select BigQuery.

Now that we are in BigQuery, let's look at the sample dataset we are going to work with. We are going to view all columns in our example table to see what fields are included. From the large Query Editor box, copy and paste the following query, then click the Run button:

#### Documentos
https://cloud.google.com/billing/docs/how-to/billing-access

https://support.google.com/a/answer/9807615

```sql
SELECT *  
FROM `cloud-training-prod-bucket.arch_infra.billing_data`

```
If we click the Results tab underneath, we can view the entire table we are going to work with. Feel free to experiment with other queries such as ordering by cost or usage amount by adding the below string to your query to sort by the column of your choice:
```sql
SELECT *  
FROM `cloud-training-prod-bucket.arch_infra.billing_data`
ORDER BY cost DESC

```
In this query, we are bringing up the entire table contents, but sorting by the highest cost first. You can experiment with other fields as well.

Let's now do some specific queries. In the same Query editor box, delete the existing contents, and enter the below query to find all charges that were more than 3 dollars:
```sql
SELECT product, resource_type, start_time, end_time,  
cost, project_id, project_name, project_labels_key, currency, currency_conversion_rate,
usage_amount, usage_unit
FROM `cloud-training-prod-bucket.arch_infra.billing_data`
WHERE (cost > 3)

```
Next let’s find which product had the highest total number of records:


```sql
SELECT product, COUNT(*)
FROM `cloud-training-prod-bucket.arch_infra.billing_data`
GROUP BY product
LIMIT 200

```
Looks like Pub/Sub is pretty popular here...

Finally, let’s see which product most frequently cost more than a dollar:

```sql
SELECT product, cost, COUNT(*)
FROM `cloud-training-prod-bucket.arch_infra.billing_data`
WHERE (cost > 1)
GROUP BY cost, product
LIMIT 200

```

```sql


```

```sql


```
