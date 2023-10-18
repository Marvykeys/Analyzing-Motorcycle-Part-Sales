# Analyzing-Motorcycle-Part-Sales :mountain_bicyclist:
Here's a fictional company that sells motorcycle parts, and they've asked for some help in analyzing their sales data!

They operate three warehouses in the area, selling both retail and wholesale. They offer a variety of parts and accept credit cards, cash, and bank transfer as payment methods. However, each payment type incurs a different fee.

The board of directors wants to gain a better understanding of wholesale revenue by product line, and how this varies month-to-month and across warehouses. I have been tasked with calculating net revenue for each product line and grouping results by month and warehouse. The results should be filtered so that only `"Wholesale"` orders are included.

They have provided me with access to their database, which contains the following table called `sales`:

## Sales
| Column | Data type | Description |
|--------|-----------|-------------|
| `order_number` | `VARCHAR` | Unique order number. |
| `date` | `DATE` | Date of the order, from June to August 2021. |
| `warehouse` | `VARCHAR` | The warehouse that the order was made from&mdash; `North`, `Central`, or `West`. |
| `client_type` | `VARCHAR` | Whether the order was `Retail` or `Wholesale`. |
| `product_line` | `VARCHAR` | Type of product ordered. |
| `quantity` | `INT` | Number of products ordered. | 
| `unit_price` | `FLOAT` | Price per product (dollars). |
| `total` | `FLOAT` | Total price of the order (dollars). |
| `payment` | `VARCHAR` | Payment method&mdash;`Credit card`, `Transfer`, or `Cash`. |
| `payment_fee` | `FLOAT` | Percentage of `total` charged as a result of the `payment` method. |


My query output should be presented in the following format:

| `product_line` | `month` | `warehouse` |	`net_revenue` |
|----------------|-----------|----------------------------|--------------|
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_one | --- | --- | --- |
| product_two | --- | --- | --- |
| ... | ... | ... | ... |

```Python
# A query to return product_line, the month from date, displayed as 'June', 'July', and 'August', the warehouse, and net_revenue.

SELECT product_line,
    CASE WHEN EXTRACT('month' from date) = 6 THEN 'June'
        WHEN EXTRACT('month' from date) = 7 THEN 'July'
        WHEN EXTRACT('month' from date) = 8 THEN 'August'
    END as month,
    warehouse,
    ROUND(SUM(total * (1 - payment_fee))::numeric, 2) AS net_revenue
FROM sales
WHERE client_type = 'Wholesale'
GROUP BY product_line, warehouse, month
ORDER BY product_line, month, net_revenue DESC;
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product_line</th>
      <th>month</th>
      <th>warehouse</th>
      <th>net_revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Breaking system</td>
      <td>August</td>
      <td>Central</td>
      <td>3009.10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Breaking system</td>
      <td>August</td>
      <td>West</td>
      <td>2475.71</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Breaking system</td>
      <td>August</td>
      <td>North</td>
      <td>1753.19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Breaking system</td>
      <td>July</td>
      <td>Central</td>
      <td>3740.94</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Breaking system</td>
      <td>July</td>
      <td>West</td>
      <td>3030.39</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Breaking system</td>
      <td>July</td>
      <td>North</td>
      <td>2568.55</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Breaking system</td>
      <td>June</td>
      <td>Central</td>
      <td>3648.14</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Breaking system</td>
      <td>June</td>
      <td>North</td>
      <td>1472.93</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Breaking system</td>
      <td>June</td>
      <td>West</td>
      <td>1200.64</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Electrical system</td>
      <td>August</td>
      <td>North</td>
      <td>4673.99</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Electrical system</td>
      <td>August</td>
      <td>Central</td>
      <td>3095.22</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Electrical system</td>
      <td>August</td>
      <td>West</td>
      <td>1229.45</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Electrical system</td>
      <td>July</td>
      <td>Central</td>
      <td>5521.94</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Electrical system</td>
      <td>July</td>
      <td>North</td>
      <td>1693.06</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Electrical system</td>
      <td>July</td>
      <td>West</td>
      <td>444.98</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Electrical system</td>
      <td>June</td>
      <td>Central</td>
      <td>2875.93</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Electrical system</td>
      <td>June</td>
      <td>North</td>
      <td>2002.30</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Engine</td>
      <td>August</td>
      <td>Central</td>
      <td>9433.48</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Engine</td>
      <td>August</td>
      <td>North</td>
      <td>2300.96</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Engine</td>
      <td>July</td>
      <td>Central</td>
      <td>1808.77</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Engine</td>
      <td>July</td>
      <td>North</td>
      <td>997.08</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Engine</td>
      <td>June</td>
      <td>Central</td>
      <td>6483.40</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Frame &amp; body</td>
      <td>August</td>
      <td>Central</td>
      <td>8571.50</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Frame &amp; body</td>
      <td>August</td>
      <td>North</td>
      <td>7819.95</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Frame &amp; body</td>
      <td>August</td>
      <td>West</td>
      <td>821.40</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Frame &amp; body</td>
      <td>July</td>
      <td>North</td>
      <td>6093.11</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Frame &amp; body</td>
      <td>July</td>
      <td>Central</td>
      <td>3103.82</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Frame &amp; body</td>
      <td>June</td>
      <td>Central</td>
      <td>5060.29</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Frame &amp; body</td>
      <td>June</td>
      <td>North</td>
      <td>4861.08</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Frame &amp; body</td>
      <td>June</td>
      <td>West</td>
      <td>2751.96</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Miscellaneous</td>
      <td>August</td>
      <td>North</td>
      <td>1823.03</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Miscellaneous</td>
      <td>August</td>
      <td>Central</td>
      <td>1722.40</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Miscellaneous</td>
      <td>August</td>
      <td>West</td>
      <td>805.31</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Miscellaneous</td>
      <td>July</td>
      <td>Central</td>
      <td>3087.31</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Miscellaneous</td>
      <td>July</td>
      <td>North</td>
      <td>2380.63</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Miscellaneous</td>
      <td>July</td>
      <td>West</td>
      <td>1145.26</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Miscellaneous</td>
      <td>June</td>
      <td>West</td>
      <td>2258.20</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Miscellaneous</td>
      <td>June</td>
      <td>Central</td>
      <td>1859.34</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Miscellaneous</td>
      <td>June</td>
      <td>North</td>
      <td>508.86</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Suspension &amp; traction</td>
      <td>August</td>
      <td>Central</td>
      <td>5362.59</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Suspension &amp; traction</td>
      <td>August</td>
      <td>North</td>
      <td>4874.51</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Suspension &amp; traction</td>
      <td>August</td>
      <td>West</td>
      <td>1069.99</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Suspension &amp; traction</td>
      <td>July</td>
      <td>Central</td>
      <td>6392.23</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Suspension &amp; traction</td>
      <td>July</td>
      <td>North</td>
      <td>3677.21</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Suspension &amp; traction</td>
      <td>July</td>
      <td>West</td>
      <td>2909.98</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Suspension &amp; traction</td>
      <td>June</td>
      <td>North</td>
      <td>7985.17</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Suspension &amp; traction</td>
      <td>June</td>
      <td>Central</td>
      <td>3291.80</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Suspension &amp; traction</td>
      <td>June</td>
      <td>West</td>
      <td>2348.83</td>
    </tr>
  </tbody>
</table>
</div>
