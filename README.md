# Social Network Analysis

This project is about Amazon’s co-purchase network; i.e., which products are purchased together on Amazon. 

There are two data files: “products.csv” and “copurchase.csv”. “products.csv” contains the information about the products. “copurchase.csv” contains the co-purchase information (i.e., if people bought one product, then they also co-purchased the other). 

* “products.csv” has the following variables: 
  + Id: Product id
  + title: Name/title of the product
  + group: Product group (Book, DVD, Video or Music etc.)
  + salesrank: Amazon Salesrank
  + rating: User rating on a scale of 1 to 5 
  + total number of reviews: Total number of product reviews available on Amazon

* “copurchase.csv” has two variables, which are Product ID’s:
  + Source: This is the focal product that was purchased 
  + Target: People who bought “Source” also purchased the Target product 

The complete analysis can be seen: https://hehuiyin.github.io/Social-Network/
