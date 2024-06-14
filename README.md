# Data science projects using SQL, Tableau, Python and Spark

Analyzing employee data with SQL, building a sales dashboard in Tableau, conducting sales analysis in Python, and analyzing services in Spark.

# Employee Data Structure

Let's take a look at the concepts behind our employee data. First, let's see the data structure. Now, a star schema is the typical way we would organize data in what's known as a data mart. Focus on one key aspect of a data mart for the employee data, and that is called a slowly changing dimension, or SCD. This is a way of structuring your data in your star schema so that you can track history appropriately. A good reason to do that might be if you wanted to see how many active employees you had on a given date in history. Well, in order to do that, you would need some form of tracking, and a slowly changing dimension is a good choice. As a refresher, a star schema starts with the subject. In this case, we're looking at sales data. Then, attached to that subject, you have the context. These are known as dimensions. Some examples might be product, territory, time, employee, and customer. So, each one of these are ways that you can analyze that subject. For example, sales by product. Maybe in that product table you have product category, so you can have sales by product category and then bring in date, so you can look at sales by category over time, by a month, by quarter, et cetera. All of these different dimensions allow us different perspectives and ways to analyze our facts in our star schema. The facts, also known as measures, are kind of at the center of it all. Now, our table, as I mentioned before, is a slowly changing dimension, and it's structured this way because it changes over time and we need to track that change. 

![image](https://github.com/mgamzec/Data-science-projects-using-SQL-Tableau-Python-and-Spark/assets/62151645/c991996f-6168-467c-830a-44910348d670)

