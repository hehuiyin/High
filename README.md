# Social Network Analysis

## Overview

This project is about Amazon’s co-purchase network (which products are purchased together on Amazon). 

There are two data files used in this project: “products.csv” and “copurchase.csv”. “products.csv” contains the information about the products. “copurchase.csv” contains the co-purchase information (if people bought one product, then they also co-purchased the other). 

* “products.csv” has the following variables: 
  + Id: Product id
  + title: Name of the product
  + group: Product group (Book, DVD, Video or Music etc.)
  + salesrank: Amazon Salesrank
  + rating: User rating on a scale of 1 to 5 
  + total number of reviews: Total number of product reviews available on Amazon

* “copurchase.csv” has two variables, which are Product ID’s:
  + Source: This is the focal product that was purchased 
  + Target: People who bought “Source” also purchased the Target product 

## Analysis
The analysis only focused on books with salesrank<=150,000 and salesrank is not -1. After data cleaning, we found out that there are 20,684 “Source” products people who buy “Target” products buy and 20,684 “Target” products people who buy “Source” products also buy. And we picked product 33 (Double Jeopardy (T*Witches, 6)) for the following analysis based on its 904 subcomponents since it has the highest degree of 53.

Then we visualized the subcomponents:

<img width="662" alt="Screen Shot 2021-08-27 at 14 36 27" src="https://user-images.githubusercontent.com/73683982/131191115-b664358f-a2ea-47f9-9fa5-e9ecb5af75f4.png">

The social graph above shows two main groups, one with Id 33 in the center: Double Jeopardy (T*Witches, 6), another one represented with Id 4429 in the center: Harley-Davidson Panheads, 1948-1965/M418.

Between 4429 and 33, there is a local bridge. It ties between two groups in a social graph that are the shortest route by which information might travel from those connected to one to those connected to the other. If the local bridge is removed, the distance between these two groups will increase. Also, the lack of the local bridge will significantly reduce the probability of co-purchasing behavior between the two groups and the frequency of products being bought.

The diameter, shown in yellow in the graph, is the longest path we can find among all the shortest distances of the vertices. The diameter is 9 and the nodes within this path are Id 37895, 27936, 21584, 10889, 11080, 14111, 4429, 2501, 3588, and 6676.

The size of the bubble is determined by how many connections they have with the other nodes. The larger the bubble, the more nodes link to it. And thus, from the graph, we can see that Id 33 and 4429 are the two biggest nodes that have the most connections. The smaller nodes spread on the edges of the network indicate fewer connections. The number of connections between nodes show how strong the relationship between the nodes are. The nodes clustered in the middle of the graph have a stronger relationship while the nodes that are spread around the border with long ties show a weaker relationship. And those products with long ties which only have 1-2 edges can be easily separated from the whole network.

Next, we ran a Poisson Regression model to predict salesrank of all the books in this subcomponent using products’ own information and their neighbor’s information.

<img width="601" alt="Screen Shot 2021-08-27 at 14 45 17" src="https://user-images.githubusercontent.com/73683982/131191828-f3beac91-29d4-46ed-8cec-45104467711a.png">

Since the Poisson Regression coefficients are given on log scale, we need to convert them back in order to interpret appropriately.

<img width="362" alt="Screen Shot 2021-08-27 at 14 50 46" src="https://user-images.githubusercontent.com/73683982/131192293-4d37d669-81b9-4382-b95b-144f3d306d65.png">

Salesrank represents the rankings of book sales and therefore, the lower the rank number, the better the sales. With the increasing of downloads, hub_score1, authority_score1, in_degree_sub, out_degree_sub, nghb_mn_salesrank, nghb_mn_review_cnt, Salesrank will also increase but it means less sales of the books. And the increase of Review_cnt, rating, closeness, betweenness, nghb_mn_rating will lead to decrease of Salesrank which means more sales of the books and thus, potentially more revenue to the company.

The complete analysis can be found on: https://hehuiyin.github.io/Social-Network/
