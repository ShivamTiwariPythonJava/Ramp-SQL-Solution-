Question- Please follow this link (https://www.db-fiddle.com/f/fufVxMKne1xMNHCbFoANMo/0) and fork the dataset. In the text box below, provide January 31's rolling 3 day average of total transaction amount processed per day and provide the link to your solution

Solution - 
SELECT
    transaction_date,
    AVG(transaction_amount) OVER (ORDER BY transaction_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS rolling_avg_3_day
FROM (
    SELECT
        DATE(transaction_time) AS transaction_date,
        transaction_amount
    FROM
        transactions
    WHERE
        EXTRACT(YEAR FROM transaction_time) = 2021
        AND EXTRACT(MONTH FROM transaction_time) = 1
) AS subquery
ORDER BY
    transaction_date;
