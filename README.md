# Restaurant Ratings Analysis

## Table of Contents
- [Case Study Overview](#-case-study-overview)
- [Dataset Description](#-dataset-description)
- [Data Cleaning](#-data-cleaning)
- [Calculated Fields](#-calculated-fields)
- [Data Analysis & Insights](#-data-analysis--insights)
- [Dashboard Overview](#-dashboard-overview)


## Project Description
This project uses Power BI to analyze restaurant review data, aiming to uncover patterns in customer satisfaction and dissatisfaction. The focus is on food quality, service experience, pricing concerns, and customer behavior to provide actionable insights.

### 1. Consumers

- `consumer_id` – Unique identifier for each consumer  
- `city` – City where the consumer lives  
- `state` – State where the consumer lives  
- `country` – Country where the consumer lives  
- `latitude` – Geographic latitude of the consumer  
- `longitude` – Geographic longitude of the consumer  
- `smoker` – Whether the consumer smokes or not  
- `drink_level` – Drinking behavior: abstemious, casual, or social  
- `transportation_method` – Primary transport method: on foot, public transport, or car  
- `marital_status` – Marital status: single or married  
- `children` – Whether the consumer has children (dependent or independent)  
- `age` – Age of the consumer  
- `occupation` – Employment status: student, employed, or unemployed  
- `budget` – Spending level: low, medium, or high  


### 2. Consumer Preferences

- `consumer_id` – Unique identifier for each consumer  
- `preferred_cuisine` – Types of food the consumer prefers  


### 3. Ratings

- `consumer_id` – Unique identifier for each consumer  
- `restaurant_id` – Unique identifier for each restaurant  
- `overall_rating` – Consumer’s overall rating (0 = Unsatisfactory, 1 = Satisfactory, 2 = Highly Satisfactory)  
- `food_rating` – Rating for food quality (0 = Unsatisfactory, 1 = Satisfactory, 2 = Highly Satisfactory)  
- `service_rating` – Rating for service quality (0 = Unsatisfactory, 1 = Satisfactory, 2 = Highly Satisfactory)  


### 4. Restaurants

- `restaurant_id` – Unique identifier for each restaurant  
- `name` – Name of the restaurant  
- `city`, `state`, `country` – Location details  
- `zip_code` – Zip/postal code  
- `latitude`, `longitude` – Geographic coordinates  
- `alcohol_service` – Alcohol availability: none, wine & beer, or full bar  
- `smoking_allowed` – Whether smoking is permitted in any section  
- `price` – Price range: low, medium, or high  
- `franchise` – Indicates if the restaurant is part of a franchise  
- `area` – Area type: open or closed  
- `parking` – Parking availability: none, public, valet, etc.  


### 5. Restaurant Cuisines

- `restaurant_id` – Unique identifier for each restaurant  
- `cuisine` – Types of cuisine served at the restaurant  

## Data Cleaning

### Importing Data from Folder
1. Home → Get Data → More → Folder  
2. Paste folder path → Connect → OK  
3. Click **Transform Data**
4. Duplicate each file, click **Binary** to expand
5. Repeat for all datasets

### Calculated Fields (DAX)

The following calculated columns were created to group values and support better filtering and insights.

**AgeGroup** 
= SWITCH(TRUE(), `consumers[Age]` <= 18, "Children and Adolescents",  
`consumers[Age]` <= 30, "Young Adults",  
`consumers[Age]` <= 45, "Adults",  
`consumers[Age]` <= 60, "Middle-aged Adults",  
"Seniors")

**Service_Rating_Category** 
= SWITCH(TRUE(),  
`ratings[Service_Rating]` = 0, "Unsatisfactory",  
`ratings[Service_Rating]` = 1, "Satisfactory",  
"Highly Satisfactory")

**Overall_Rating_Category** 
= SWITCH(TRUE(),  
`ratings[Overall_Rating]` = 0, "Unsatisfactory",  
`ratings[Overall_Rating]` = 1, "Satisfactory",  
"Highly Satisfactory")

**Food_Rating_Category** 
= SWITCH(TRUE(),  
`ratings[Food_Rating]` = 0, "Unsatisfactory",  
`ratings[Food_Rating]` = 1, "Satisfactory",  
"Highly Satisfactory")

## Tools Used
- Power BI for data visualization and dashboard creation  
- SQL for data cleaning and data transformations  
- Excel for preliminary data formatting  


## Key Questions
1. Which restaurants have the highest number of reviews for food and service?  
2. What are the most common factors cited in negative reviews?  
3. How does customer behavior (time, frequency, device type, age group) influence review patterns?


## Data Analysis & Insights

The analysis revealed several key patterns regarding restaurant performance and consumer satisfaction:

- **Food and Service are the core drivers of satisfaction**: Restaurants that consistently receive high ratings in both `Food_Rating` and `Service_Rating` are also the ones with the best `Overall_Rating`. Among the top 10 most-rated restaurants, over 80% had scores of 2 (Highly Satisfactory) in both aspects.

- **Unsatisfactory service is the leading cause of poor ratings**: More than 60% of `Overall_Rating = 0` cases are associated with a `Service_Rating = 0`, even if the food was rated as satisfactory. This indicates that bad service strongly outweighs good food in shaping customer perception.

- **High prices and lack of parking correlate with dissatisfaction**: Restaurants categorized with `Price = high` and `Parking = none` showed a higher frequency of poor overall ratings, suggesting that customers expect better value and convenience at premium price levels.

- **Young adults are the most frequent reviewers**: The `AgeGroup = Young Adults (19–30)` represents the largest share of reviewers. This segment also tends to give more polarized feedback (either 0 or 2), reflecting higher expectations and stronger opinions.

- **Budget-conscious consumers are more critical**: Users with `Budget = low` are more likely to give `Food_Rating = 0` even for average-quality meals. This highlights a possible mismatch between pricing and value perception among this group.




## Dashboards

### Overview of Ratings  
![Overview](https://github.com/DaoDucManh14/restaurant-ratings-powerbi/blob/main/screenshots/overview.jpg?raw=true)

### Negative Review Factors  
![Negative Factors](https://github.com/DaoDucManh14/restaurant-ratings-powerbi/blob/main/screenshots/negative_factors.jpg?raw=true)

### Customer Behavior Analysis  
![Customer Behavior](https://github.com/DaoDucManh14/restaurant-ratings-powerbi/blob/main/screenshots/customer_behavior.jpg?raw=true)



## Project Structure

- `report.pbix` – Power BI report file
- `README.md` – Project documentation
- `screenshots/` – Folder containing dashboard images:
  - `overview.jpg`
  - `negative_factors.jpg`
  - `customer_behavior.jpg`

