# The Foursquare Project!
#### A look into the safest and most family friendly neighborhoods in NYC
                              May 2, 2022 
                             Brandon Louis 




## The Project 


# I. Introduction
Suppose you receive a new job in New York City. Let’s also suppose you have school aged children
and you want to live somewhere safe. Who wouldn’t, right? There are plenty of online resources
that aim to help users find quality places to live. However, there are not a lot of resources that can
give the specific results laid out in this project. It is also very difficult to find clear explanations or the
data in which some of these qualities of life or quality of city ratings come from. This project aims to
gather data from across the internet to provide a qualitative recommendation for the safest and
most educational neighborhood in NYC. The data are collected from the New York City repository
for crime, New York City’s Department of Education repository for schools and programs, and real
estate data from PropertyShark.com.
# II. Data
Data for each of the NYC police precincts are scraped from the website
https://data.cityofnewyork.us/Public-Safety/Police-Precincts/78dh-3ptz. Data from NYC Department
of Education for the types and places of after school activities for children, and the “quality review”
list of school that meet said quality criteria. The after-school activity dataset contains coordinate
information, types of options available, among other unused information. The quality review data
set contains only the names of the schools. These names are then cross-referenced with the
Foursquare API. Other Foursquare API data is used for the collection of locations of afterschool
activities in certain neighborhoods throughout New York City. The mean data of rental property
costs were gathered from PropertyShark.com. These data are available at
https://github.com/loouisbrandon/NY_Foursquare-

# III. Methodology
For this project, I assume that user is interested in finding the safest neighborhood to live in. For this 
reason, the 10 precincts with the lowest number of total crimes are shown in Figure 1.

![enter image description here](https://raw.githubusercontent.com/loouisbrandon/NY_Foursquare-/main/Captura%20de%20tela%20de%202022-05-02%2011-59-33.png)
Ten neighborhoods with the highest total amount of after school activities are shown in Figure 2.

![enter image description here](https://raw.githubusercontent.com/loouisbrandon/NY_Foursquare-/main/Captura%20de%20tela%20de%202022-05-02%2012-49-12.png)

# 

Cross-referencing these neighborhoods with police precincts with Python’s shapely module using
polygons and points, Washington Height South (number 3 most after school activities) neighborhood is
inside the 33rd precinct (the 10th safest precinct). Nearby schools are found in the Foursquare API at a
one-kilometer radius from the centroid of the Washington Heights neighborhood (shapely module).
From these schools, one school was found from cross-referencing the quality schools list. This school is
P.S. 128 Audubon. Now that we are sure there are plenty of after school activities, a quality school in the
neighborhood, housing costs need to be considered.
From the dataset collected from PropertyShark.com, median rent is available. To
estimate the median rent, simple linear regression is employed with single predictor Year and
outcome variable, Price. The model is given by
𝑌𝑖 = 𝑏0 + 𝑏1 𝑥 + 𝜖𝑖
where 𝜖 ∈ 𝑖𝑖𝑑𝑁(0, 𝜎 2 ), 𝑖 = 1,2,3, … ,13, and 𝛽0 , 𝛽1 and 𝜖 are unknown parameters. K-fold cross-
validation with 10 splits is used (although there is such small data) and a simple ensemble of the average
of model intercepts and coefficients to optimize the prediction model. Since an ensemble method was
used, Pearson’s correlation inside Python’s spicy.stats module was used to assess predictions versus
actual prices. This model is finally used to predict the median rent cost.
IV.
Results
The neighborhood within the top ten safest precincts, with the most amount of after school activities is
Washington Heights South in Precinct 33. This neighborhood is in the Manhattan borough. It has 24
available locations with after school activities. The neighborhood with the most after school activities is
Brownsville with 33. The 33rd precinct had 324 total crimes recorded. The precinct with the
lowest crimes in 2019 is the 22nd precinct (AKA Central Park Precinct), also in the Manhattan borough.
There was one school, P.S. 128, in the Washington Heights South neighborhood on the NYC DOE quality
schools list. Below is a choropleth map of the locations of after school activities and P.S. 128. 

# ![enter image description here](https://raw.githubusercontent.com/loouisbrandon/NY_Foursquare-/main/Captura%20de%20tela%20de%202022-05-02%2013-43-19.png)
From the k-fold cross validated linear regression, the final model for median rent price is given by,
𝑦̂𝑖 = −55566.44 + 28.22𝑥𝑖 + 𝜖𝑖
where 𝑦̂𝑖 is the predicted value of median house rent price and 𝑥𝑖 is a numerical variable for year. Using
an ensemble k-fold validation models, a Pearson correlation coefficient of 0.966 with p-value 8.9 x 10-8.
Residual diagnostics testing (provided in the code in the appendix section
https://github.com/loouisbrandon/NY_Foursquare-/blob/main/1_Project_OK.ipynb)
shows that the errors relatively normal and have uniform variance. Assuming the individual using this
program will be moving to New York City, the estimated median rent price would be
𝑦̂ = −55566.44 + 28.23(2020)
= $1458.16.
V.
Discussion
The analyses above displayed how 3 simple life-style choices (safety, after school activities, and quality
schools) can affect one’s choice in neighborhoods in which to life. This project assumed that cost was no
issue and the deliverable of rent price was just an informative number. Provided with more time and
data resources, the calculations of the prices of the individual neighborhoods could also be used as a
determining factor for overall best neighborhood to live. What we can recommend however from this
project is that a family moving to Washington Heights South in Manhattan can expect a very low crime
rate compared to the rest of the city, being a top 10 neighborhood and the overall safest borough. The
user can also enjoy the fact that there are 24 after school activities in the neighborhood to send their
kids and a top school according to the NYC Department of Education.
VI.
Conclusion
Although moving to a new city, especially a gigantic one like New York City, the use of algorithms such as
the one used in this project can be very useful. Adjustment of simple parameters can help give users a
much clearer idea of the place they are moving to than some of the current online resources.

# 

This Project is a work for a Infnet Data science Bootcamp.
Gratitude to all the teachers who are helping me on this journey.
