# I. Background 
You are a Data Analyst working for an e-commerce company called X. You are given the standard task of giving a presentation to present an overview of the business and operations of the computer company. Up to the present time at for Sales Manager and Operations Manager. The presentation should at a minimum, include the following information: business overview, customer satisfaction, and 2 to 3 suggestions (area) where the company can improve.


# II. Analysis

### Business situation of the company
### 1. Business situation by year and month of the company

```php
import matplotlib.ticker as mtick
from pandas.plotting import register_matplotlib_converters
register_matplotlib_converters()

ax = turnover.T.plot.bar(figsize=(15,10), xlabel="Years", ylabel="Payment_value", color=sns.color_palette('Set2'))
ax.yaxis.set_major_formatter(mtick.StrMethodFormatter('{x:,.0f}'))
ax.set_xlabel('Years',fontsize=20)
ax.set_ylabel('Payment Value', fontsize=20)
ax.set_xticklabels(ax.get_xticklabels(), rotation=0, ha='center')
plt.show()
```
![image](https://user-images.githubusercontent.com/110837675/226807037-ff44e509-7594-4bad-8253-4e75370a6508.png)

#### A. Business situation by year 
```php
import plotly.express as px

turnover_year = df.groupby('year')['payment_value'].sum().reset_index()

fig = px.bar(turnover_year, x='year', y='payment_value', title='Revenue By Month')

fig.update_layout(xaxis=dict(type='category'),width=900,height=700,font=dict(color='black'))
fig.update_traces(marker=dict(line=dict(width=50)),text=turnover_year['payment_value'],textfont=dict(color='black'))
fig.show()
```
output:

![image](https://user-images.githubusercontent.com/110837675/226799131-02b61b01-05c8-45e6-a4b2-9925f390ec04.png)

 The company's business situation over the years has grown stronger, the revenue source has increased rapidly over the years, in 2016 the revenue was only $18202,78 USD, in 2017 the revenue increased to $2124535.1 USD (revenue). And by September 2018 the revenue was $2659783,53 (September 2018 revenue grew by 25.2% compared to 2017). Therefore, the company has grown very strong, the number of sales orders in recent years has increased a lot, bringing a lot of revenue to the company.
 
 
=> The company's high revenue shows that the company's business situation has improved and developed strongly over the years.


#### B. Business situation by month

```php
import plotly.express as px
turnover_month= df.groupby('month')['payment_value'].sum().reset_index()
fig= px.line(turnover_month,x='month',y='payment_value', markers=True, title='Revenue By Month')
fig.update_traces(marker=dict(line=dict(width=10)),text=turnover_year['payment_value'],textfont=dict(color='black'))
fig.show()
```
output:

![image](https://user-images.githubusercontent.com/110837675/226800408-c21a3a11-4462-4032-9317-4da4328bb53d.png)

- Revenue from January to August generally has a uniform growth, and August revenue has a marked increase compared to the previous months, but this is only September 2018 not enough data to evaluate. Prices in the months after September 2018, but it can be seen that the increase in monthly revenue shows that the company has a good development.


### 2. Top product groups (product_category_name) bring the most revenue for the company 

```php
import plotly.graph_objs as go

fig = go.Figure(
    data=[go.Pie(labels=product['product_category_name'], values=product['payment_value'], pull=[0.09, 0])])
fig.update_layout(title="Percentage Revenue By Product_Category",width=1140, height=600, legend_title_text='Product Category Name')
fig.show()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/226800499-02eee2f8-bd62-4642-87a1-cdd38a08da9e.png)

The product groups above the graphic are the best-selling and highest-recall product groups for the company. Those are the strong products of the company store because the company's revenue is mainly due to those product groups falling behind. Therefore, we need to focus more resources to develop our company's strong products. The following ideas can be developed:
 

- After knowing the company's strong selling product groups, you can:
  
  -Product ecosystem development. More specifically, focus on building, supporting products, auxiliary products or accessories for these top products.
  
  -Provide vouchers for ancillary products (ecosystem) when buying top products, to stimulate demand they can buy additional accessories.
  
### 3. Number of orders delivered successfully and canceled (Số đơn hàng giao thành công và bị hủy)

```php
fig= px.pie(values=delivered['proportion'],names=delivered.index, hole=.3, title='Order Status')
fig.update_layout(annotations=[dict(text='Status', x=0.50, y=0.5, font_size=20, showarrow=False)])
fig.update_layout(
    width=1140,
    height=600, legend_title_text='Status')
fig.show()
```
![image](https://user-images.githubusercontent.com/110837675/226800799-a2f2e271-d275-4073-9ae8-f8d23e0f2243.png)

-Looking at the Graphic , the number of canceled orders is 123 orders, accounting for45.89% of the total number of successfully delivered orders, we need to find out the reason why the orders are canceled for any reason and from there we need to fix it. To minimize the number of canceled orders. These are the customer ids who cancel the most orders:

```php
fig= px.pie(values=customer_cancel['order_status'],names=customer_cancel['customer_id'], hole=.3, title='CustomerId_Cancel')
fig.update_layout(annotations=[dict(text='Cancel', x=0.50, y=0.5, font_size=20, showarrow=False)])
fig.update_layout(
    width=1140,
    height=600,legend_title_text='Customer_id')
```

![image](https://user-images.githubusercontent.com/110837675/226801089-a5d3fdbf-c57c-47fe-9fa2-17dcaac9eb4c.png)

   -These are the customer ids with the most order cancellations, need to find out the reason for canceling orders from them, and we should also warn them to help them reduce the cancellation rate by is that the promotional vouchers for these people will be limited and they are unlikely to receive much discount vouchers, or the shipping time will be longer than expected, and the order account will be limited. In some articles, which have been cancelled a lot...


### 4. Payments

```php
payment_type= df.groupby('payment_type')['customer_id'].count().reset_index()
fig= px.bar(payment_type, x="payment_type",y='customer_id',title='Payment Type of customer')
fig.update_layout(xaxis=dict(type='category'), width=1000, height=700)
fig.update_traces(marker=dict(line=dict(width=0.6)))
fig.show()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/226801448-ac80ff3e-8f51-43fe-87ba-bffb73d80567.png)


-Based on the chart, the form of payment that customers use the most to pay is credit_card, because people often have the habit of shopping online with credit cards.

=>The goal is to minimize cash transactions. Prioritize payment via credit card/debit card to minimize the rate of customers not receiving the goods.

=> Create promotions that apply to credit/debit card payments. (Tạo các chương trình ưu đãi áp dụng cho hình thức thanh toán bằng thẻ tín dụng/ghi nợ.)


### 5. Customer review title (Tiêu đề đánh giá của khách hàng)

```php
tile=df['review_comment_title'].value_counts().nlargest(10).reset_index()
fig = px.treemap(tile, path=[px.Constant('Review Comment Title'),'index'], values='review_comment_title')
fig.show()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/226882999-87545479-1d8d-4153-a0ee-63cc66b862bd.png)


Translate the meanings of the words in the graphic 

-Recomendo: Recommendation

-Bom: Good

-super recomendo: should try 

-Excelente: The products are supper good

-Muito bom : very good

- Looking at the data table, recomendo and super recomendo are rated by customers quite a lot, which shows that seller_id's products are not really good.
 advised and suggested by customers to correct, the sales people should approach and take care of them to find out the cause of the bad products, then absorb and improve the product to match the needs. from buyers, thereby increasing sales revenue.


- For products that are well-reviewed by customers, it is advisable to continue to maintain the quality of that product and continue to develop higher quality to earn more revenue. 

### 6.Customer Satisfaction Level. (Mức Độ Hài Lòng của khách hàng.)

```php
fig = go.Figure(data=[go.Pie(labels=star['review_score'], values=star['count'], pull=[0.1, 0.2, 0, 0, 0])])
fig.update_layout(title="Number of star customer evaluate")
fig.update_layout(height=600, width=1130,legend_title_text='Star')
fig.show()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/226801881-81e6d259-88f7-4eea-85dc-a801d5ee5dbb.png)

-For product groups that are rated 1 and 2 points, we need to reconsider, need to find out the reason, and consider which product group 1,2 reviews come from / seller id, thereby improving product quality to meet the needs of customers.

### 7. List of product groups rated 1 and 2 points

```php

star12 = df.loc[(df['review_score'] == 1) | (df['review_score'] == 2)]
star12 = pd.crosstab(star12.product_category_name, star12.review_score).sort_values(by=1, ascending=False)
star12 = star12.nlargest(columns=[1,2], n=3)

fig = px.bar(star12, x=star12.index, y=[1,2], labels={'x': 'Product Category', 'y': 'Number of Reviews'})
fig.update_layout(title="Number of 1- and 2-Star Reviews By Product Category", legend_title_text='star')
fig.show()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/226807507-4a83294f-9d88-441b-a40e-7060f864493c.png)

These are graphic of top 3 product groups that are rated 1 and 2 points. (Đây là những danh sách nhóm sản phẩm bị đánh giá 1 và 2 điểm.)

Step 1: We have to find out the reason from the seller id (seller_id) why customers rate 1 and 2 points.

Step 2: We need to collect customer feedback, find out the reason. 

Step 3: Categorize the cause. Is a bad review due to a bad product or bad service? If it is due to the product, consider improving the quality of the product, or removing the product from the sales list. If it is due to poor service quality, it is necessary to find out and work with the supplier.

Step 4: If the reason for evaluating 1 2 points is legitimate, it is necessary to take measures to compensate the customer. It is possible to compensate with an email voucher to apologize, promising to improve service/product quality.


### 8. List of seller ids with 1 and 2 star reviews. 

```php
star12 = df.loc[(df['review_score'] == 1) | (df['review_score'] == 2)]
star12= star12.groupby('seller_id')['review_score'].count().sort_values(ascending=False).nlargest(5).reset_index()
fig = go.Figure(data=[go.Pie(labels=star12['seller_id'], values=star12['review_score'],pull=[0, 0.1, 0, 0, 0])])
fig.update_layout(title="1 And 2 Rated Star Of Seller Id")
fig.update_layout(height=600, width=1130, legend_title_text='Seller_id')
fig.show()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/226802119-772f396f-b894-4a64-8a3b-c67db9bf3a81.png)

These are top5 the seller id  with the highest ratings of 1 and 2. In this case, the company needs 

Step 1: Classify the causes from rating 1 and 2 points. 

Step 2: Ask the seller to explain about the rating of 1 or 2 points. Seller needs to present the way to remedy the consequences, improve the product/service and commit to doing so.

Step 3: Compensate customers with bad experiences. (voucher, refund, product exchange, ...)

Step 4: Evaluate the seller's ability. If the rating of 1 or 2 points is too much, the seller does not improve the product or service => ban id seller.
 
And should warn seller id, when being rated 1 and 2 stars, that low score will be pushed up and will bring trouble to other customers when they see such low score, they will lose faith in the product. Doubts about quality and do not make a purchase decision will make sales go down, orders will not be sold much anymore, and especially they have to improve their own products.


### 9. Customers with the most orders.

```php
df['payment_installments']= df['payment_installments'].apply(lambda x:'pay one' if x ==1 else 'pay installments')
top_10_customers = df['customer_id'].value_counts().head(10)
top_10_df = df[df['customer_id'].isin(top_10_customers.index)]
fig = px.histogram(top_10_df, x='customer_id', color='payment_installments',title='Customer ID have most order')
fig.update_layout(width=1150, height= 700)
fig.show()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/226802365-743c07ea-c439-4629-8994-4e8f525025ed.png)

- This is a graphic of top 10 customers with the highest number of orders at the company, they are the ones who believe in the company's products, so it is necessary to pay attention to taking care of them regularly so that they do not leave buying products from the company. own company.


Usually, consumers tend to choose to buy in bulk. Therefore, when a business satisfies the existing group of customers, these people will act as intermediaries to introduce products / services to their acquaintances. Unwittingly, loyal customers have become salespeople for the products of the businesses they trust. This will be vital to business enterprises in the 4.0 era, where the power of word-of-mouth marketing is being blown along with the development of the internet. Almost just need to take good care of existing customers, will have more new customers.
Treatments may include:


-	Give vouchers to customers when reaching spending levels according to each milestone. 
-	Email inquires when customers do not buy goods for a long time. 


### 10. List of customers who bring the highest revenue for the company. 

```php
df_sorted = df.groupby('customer_id')['payment_value'].sum().sort_values(ascending= False).reset_index().nlargest(columns='payment_value',n=10)
df_sorted['cumulative_percent'] = 100 * df_sorted['payment_value'].cumsum() / df_sorted['payment_value'].sum()
# create the bar chart for the payment values
bar_chart = go.Bar(x=df_sorted['customer_id'], y=df_sorted['payment_value'])

# create the line chart for the cumulative percentage
line_chart = go.Scatter(x=df_sorted['customer_id'], y=df_sorted['cumulative_percent'], yaxis='y2', name='% Cumulative')
# set the layout for the chart
layout = go.Layout(title='Top 10 Customers Who Bring Highest Revenue', yaxis=dict(title='Payment Value'), yaxis2=dict(title='% Cumulative', overlaying='y', side='right'), width=1150, height=600, margin=dict(l=50, r=50, b=50, t=50), plot_bgcolor='#f8f8f8')
# create the figure and plot the chart
fig = go.Figure(data=[bar_chart, line_chart], layout=layout)
fig.show()
```

![image](https://user-images.githubusercontent.com/110837675/226802529-83dae0be-4855-4ec9-89de-b671e407bec5.png)

-These are the top 10 customers that bring the main revenue to the company, we need to pay special attention and care to these customers so that they do not leave our services, and need to create promotional vouchers. Best forever to encourage them to buy their products, because they are the main source of income for the company, if not well taken care of, they will leave then the company's revenue will go down. Although customers order from the company a lot, but based on the Pareto chart, it can be seen that only 20% of those customers bring in 80% of the company's profits, so it is necessary to take special care of these customers.

### 11. Percentage of customers paying in a lump sum and one-time payment.

```php
fig= px.pie(values=tile['payment_installments'],names=tile['index'], hole=.3, title='Paying in a lump sum and one-time payment')
fig.update_layout(annotations=[dict(text='Payments', x=0.50, y=0.5, font_size=20, showarrow=False)])
fig.update_layout(
    width=1140,
    height=600, legend_title_text='Payments')
fig.show()
```
![image](https://user-images.githubusercontent.com/110837675/226803861-9f8c26ab-8901-43b1-9cfd-98fb825a95af.png)


-The number of one-time payments and installment payments are almost the same, but for installment customers, we need to pay attention and remind them to learn to pay debt and interest on time, to avoid annoying cases. both of us have to call and text them and hpj will both be bothered by my messages and their interest will increase if not paid on time.


### 12. Cities that bring in the highest revenue for the company

```php
# create the bar chart for the payment values
bar_chart = go.Bar(x=data_sorted['customer_city'], y=df_sorted['payment_value'])

# create the line chart for the cumulative percentage
line_chart = go.Scatter(x=data_sorted['customer_city'], y=data_sorted['cumulative_percent'], yaxis='y2', name='% Cumulative')
# set the layout for the chart
layout = go.Layout(title='Top 10 City That Bring The Highest Revenue', yaxis=dict(title='Payment Value'), yaxis2=dict(title='% Cumulative', overlaying='y', side='right'), width=1150, height=600, margin=dict(l=50, r=50, b=50, t=50), plot_bgcolor='#f8f8f8')
# create the figure and plot the chart
fig = go.Figure(data=[bar_chart, line_chart], layout=layout)
fig.show()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/226806929-250ca3f4-31a0-4148-bb92-cc12ec381595.png)

- The company's revenue is mainly concentrated in these cities, proving that customers are mainly concentrated in these cities for optimization, it is advisable to place warehouses so that transshipment can be saved. Save more and customers when ordering can receive their goods faster and they also save on their shipping costs.


### Provide solutions for the company (Đưa ra giải pháp cho công ty)
# III. Conclusion (Kết luận)

- The company's business situation in the past 3 years has developed strongly when the revenue has increased a lot each year, the number of sales orders has also increased significantly, but the monthly revenue has changed. not crowded when the first months of the year sold a lot of orders, but conversely, the months at the end of the year, the revenue decreased more than we need to review to improve this. For product groups that bring high revenue to the company, it is necessary to focus resources to develop more strongly because it is their strength, and for installment customers, employees need to pay attention and reminding them to pay their debts and interest on time, in addition, taking care of customers who bring high revenue to the company is also very important because they are the lifeblood of the company, so it is necessary to have a customer care team. special for these people.

Areas where the company can improve: (Các lĩnh vực mà công ty có thể cải thiện)

  - The first is that the product and seller id have low ratings, this is the first important thing the company needs to improve, the company needs to remind about the seller id has to improve for the items that are damaged. low rating, because customers often have the phenomenon of following the crowd when the product rating is so low, it will make the customers behind them feel afraid about making a purchase decision, maybe they will give up the product service. products to choose a service to buy from another company. In order to improve this, it is necessary to collect and listen to all customer opinions about the product, thereby improving the product to suit the market needs and customers' needs.
  
  
  The second is about taking care of customers that bring high profits to the company, because they are a living part of the company, contributing very high revenue to the company, in order to retain them, it is necessary to have a caring team. Special customer care for these customers, need to regularly email or call to ask them about our products, in addition we can create special vouchers based on customers This is to retain them and stimulate them to buy their products, as mentioned above, customers often follow the phenomenon of the majority. Therefore, when a business satisfies the existing group of customers, these people. will act as an intermediary to introduce products/services to his acquaintances. Unwittingly, loyal customers have become salespeople for the products of the businesses they trust.
    
    
  -Thirdly, about the installment customers, the company needs to pay attention to this group of installment customers. It needs to notify the customer care department to regularly pay attention and see if they have paid their debt and interest on time. or not, remind them, to overcome this situation, we can create promotions for customers who pay once to stimulate them to buy and pay once.
  
  
  
[Click the link to view the dashboard](https://app.powerbi.com/groups/7ddb72d0-2e02-4a0e-b5c4-8d1493524633/reports/9cd9c119-a222-4fe1-93c3-58cc08bf4a82/ReportSection)
   
   




