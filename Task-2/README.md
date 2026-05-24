**Task-2: Customer Segmentation Using Unsupervised Learning**

**Task Objective:**
The objective of this project is to perform customer segmentation using unsupervised machine learning techniques on the Mall Customers Dataset. The goal is to group customers based on their purchasing behavior, annual income, and spending patterns in order to identify meaningful customer segments. <br>

By understanding different customer groups, businesses can: <br>
improve targeted marketing <br>
personalize customer experiences <br>
optimize promotional strategies <br>
increase customer retention and revenue <br>
<br>

**Approach:**
*1. Exploratory Data Analysis (EDA)*
The first step is to understand the dataset through statistical analysis and visualizations, which included:
<br>
checking missing values<br>
analyzing feature distributions<br>
plotting histograms and scatter plots<br>
studying relationships between variables<br>
<br>
Key analyses performed:<br>
Age distribution<br>
Annual income distribution<br>
Spending score distribution<br>
Gender distribution<br>
Income vs Spending Score relationship<br>
Correlation analysis<br>
<br>
*2. Feature Selection and Scaling*
<br>
The primary features used for clustering were:<br>
Annual Income (k$) <br>
Spending Score (1–100)<br>
<br>
Feature scaling was applied using StandardScaler because K-Means clustering is sensitive to feature magnitude.<br>
<br>
*3. K-Means Clustering*
<br>
Customer segmentation was performed using: K-Means Clustering<br>
The Elbow Method was used to determine the optimal number of clusters.<br>
The optimal cluster count was identified as: K=5<br>
The model grouped customers into five meaningful customer segments based on spending behavior and income patterns.<br>
<br>
*4. PCA Visualization*
<br>
To visualize high-dimensional customer data in two dimensions, the project used: Principal Component Analysis<br>
PCA reduced the dataset into two principal components:<br>
PC1 & PC2<br>
This allowed the customer clusters to be visualized clearly in a 2D scatter plot.<br>

**Results and Findings:**
The K-Means clustering algorithm identified five major customer groups based on annual income and spending behavior.

| Cluster | Customer Type | Characteristics |
|----------|--------------------------|---------------------------------------------|
| 0 | Average Customers | Moderate income and moderate spending |
| 1 | Premium Customers | High income and high spending |
| 2 | Budget Customers | Low income and low spending |
| 3 | Impulsive Buyers | Lower income but high spending |
| 4 | Careful Wealthy Customers | High income but low spending |
<br>
<br>
**Key Findings**
*1. Spending Behavior is Diverse*
<br>
Customers exhibit significantly different spending patterns:<br>
some customers spend heavily despite lower income<br>
some high-income customers spend conservatively<br>
This shows that income alone is not sufficient to predict customer behavior.<br>

*2. Middle-Income Customers Dominate*
<br>
Most customers fall within the middle-income range, indicating that the mall primarily serves middle-class consumers.<br>

*3. Clustering Successfully Identified Customer Groups*<br>

The K-Means algorithm effectively separated customers into meaningful segments with distinct purchasing behaviors.<br>
The PCA visualization confirmed relatively good cluster separation.<br>

*4. Business Value of Segmentation*
<br>
The segmentation results can help businesses:<br>
create personalized marketing campaigns<br>
improve customer targeting<br>
increase customer satisfaction<br>
optimize loyalty programs<br>
improve sales performance<br>

**Conclusion:**
<br>
This project demonstrated how unsupervised learning techniques can be used to analyze customer behavior and generate actionable business insights.<br>
<br>
The analysis highlights the importance of customer segmentation in modern business analytics and demonstrates how machine learning can support data-driven marketing and decision-making.
