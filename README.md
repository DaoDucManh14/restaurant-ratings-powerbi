# Restaurant Ratings Analysis

## Table of Contents
- [Project Description](#project-description)
- [Dataset Description](#dataset-description)
- [ER Diagram](#er-diagram)
- [Data Cleaning](#data-cleaning)
- [Calculated Fields (DAX)](#calculated-fields-dax)
- [Data Analysis & Insights](#data-analysis--insights)
- [Dashboards](#dashboards)


## Project Description
Restaurant ratings in Mexico by real consumers from 2012, including additional information about each restaurant and their cuisines, and each consumer and their preferences.
This project uses Power BI to analyze restaurant review data, aiming to uncover patterns in customer satisfaction and dissatisfaction. The focus is on food quality, service experience, pricing concerns, and customer behavior to provide actionable insights.

## Dataset Description

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

## ER Diagram
![Restaurant-ratings drawio](https://github.com/DaoDucManh14/restaurant-ratings-powerbi/blob/main/screenshots/Er_diagram.png)

## Data Cleaning

### Importing Data from Folder
1. Home → Get Data → More → Folder  
2. Paste folder path → Connect → OK  
3. Click **Transform Data**
4. Duplicate each file, click **Binary** to expand
5. Repeat for all datasets

### Calculated Fields (DAX)

The following calculated columns were created to group values and support better filtering and insights.

#### Age Group
```
AgeGroup = 
SWITCH(
    TRUE(),
    consumers[Age] <= 18, "Children and Adolescents",
    consumers[Age] <= 30, "Young Adults",
    consumers[Age] <= 45, "Adults",
    consumers[Age] <= 60, "Middle-aged Adults",
    "Seniors"
)
```
#### Service Rating Category
```
Service_Rating_Category = SWITCH(
    TRUE(),
    ratings[Service_Rating] = 0, "Unsatisfactory",
    ratings[Service_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)
```
#### Overall Rating Category
```
Overall_Rating_Category = SWITCH(
    TRUE(),
    ratings[Overall_Rating] = 0, "Unsatisfactory",
    ratings[Overall_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)
```
#### Food Rating Category
```
Food_Rating_Category = SWITCH(
    TRUE(),
    ratings[Food_Rating] = 0, "Unsatisfactory",
    ratings[Food_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)
```
## Tools Used

- **Power BI**: Used for building interactive dashboards and data visualizations.
- **Power Query**: Utilized for data cleaning, transformation, and combining multiple datasets.
- **DAX (Data Analysis Expressions)**: Applied to create calculated columns and measures for advanced insights.
- **Microsoft Excel**: Initial data inspection and formatting before importing to Power BI.


## Key Questions
1. Which restaurants have the highest number of reviews for food and service?  
2. What are the most common factors cited in negative reviews?  
3. How does customer behavior (time, frequency, device type, age group) influence review patterns?


## Data Analysis & Insights

The analysis revealed several key patterns regarding restaurant performance and consumer satisfaction:

### 1. Restaurants with High Food & Service Ratings Dominate the Top

- Restaurants that rank highest in overall customer satisfaction consistently receive a score of 2 (Highly Satisfactory) in both `Food_Rating` and `Service_Rating`.
- This confirms that food quality and service are the two most critical dimensions influencing overall ratings.

### 2. Poor Service is the Main Reason for Low Ratings

- The majority of negative overall ratings (score = 0) are strongly correlated with a `Service_Rating = 0`.
- In contrast, customers are more forgiving of food quality than of poor service, suggesting service has a larger impact on user perception.

### 3. Price and Parking Influence Negative Feedback

- Restaurants with `Price = high` or no parking options (`Parking = none`) are more likely to receive lower ratings.
- This implies that customers expect higher value and better convenience when paying premium prices.

### 4. Consumer Demographics Affect Rating Behavior

- **Young Adults (19–30 years old)** are the most active reviewers and are more likely to give polarized feedback (either 0 or 2), especially when their expectations aren’t met.
- **Consumers with a low budget** are more critical of food quality, often rating food as unsatisfactory even when overall ratings are decent.
- **Frequent social drinkers** tend to give more favorable reviews, especially in restaurants that offer alcohol service.

## Dashboards

### Overview of Ratings  
![Overview](https://github.com/DaoDucManh14/restaurant-ratings-powerbi/blob/main/screenshots/overview.jpg?raw=true)

### Negative Review Factors  
![Negative Factors](https://github.com/DaoDucManh14/restaurant-ratings-powerbi/blob/main/screenshots/negative_factors.jpg?raw=true)

### Customer Behavior Analysis  
![Customer Behavior](https://github.com/DaoDucManh14/restaurant-ratings-powerbi/blob/main/screenshots/customer_behavior.jpg?raw=true)
