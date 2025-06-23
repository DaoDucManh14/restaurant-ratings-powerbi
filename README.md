# Restaurant Ratings Analysis

## Table of Contents
- [Project Description](#project-description)
- [Tools Used](#tools-used)
- [Key Questions](#key-questions)
- [Key Insights](#key-insights)
- [Sample Dashboards](#sample-dashboards)
- [Project Structure](#project-structure)


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

### 2. Calculated Fields (DAX)

The following calculated columns were created to group values and support better filtering and insights.
-- AgeGroup: Group consumers by their age
AgeGroup = 
SWITCH(
    TRUE(),
    consumers[Age] <= 18, "Children and Adolescents",
    consumers[Age] <= 30, "Young Adults",
    consumers[Age] <= 45, "Adults",
    consumers[Age] <= 60, "Middle-aged Adults",
    "Seniors"
)

-- Service_Rating_Category: Convert numeric service ratings into descriptive labels

Service_Rating_Category = SWITCH(
    TRUE(),
    ratings[Service_Rating] = 0, "Unsatisfactory",
    ratings[Service_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)

-- Overall_Rating_Category: Translate overall rating scores into readable categories

Overall_Rating_Category = SWITCH(
    TRUE(),
    ratings[Overall_Rating] = 0, "Unsatisfactory",
    ratings[Overall_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)

-- Food_Rating_Category: Convert food quality ratings into human-readable labels

Food_Rating_Category = SWITCH(
    TRUE(),
    ratings[Food_Rating] = 0, "Unsatisfactory",
    ratings[Food_Rating] = 1, "Satisfactory",
    "Highly Satisfactory"
)


## Tools Used
- Power BI for data visualization and dashboard creation  
- SQL for data cleaning and data transformations  
- Excel for preliminary data formatting  



## Key Questions
1. Which restaurants have the highest number of reviews for food and service?  
2. What are the most common factors cited in negative reviews?  
3. How does customer behavior (time, frequency, device type, age group) influence review patterns?



## Key Insights

1. **Overview of Ratings**  
   - Most restaurants receive between 3 and 4 stars.  
   - A few restaurants consistently achieve high scores in both food and service categories.  
   - Rating distributions differ depending on price level and restaurant type.

2. **Analysis of Negative Reviews**  
   - Service quality emerges as the top cause of negative feedback.  
   - Other key complaints include high prices, poor food presentation or taste, and issues with cleanliness or ambience.

3. **Customer Behavior Analysis**  
   - Review activity peaks during lunch and dinner hours.  
   - Younger users (ages 18–34) and mobile users are the most frequent reviewers.  
   - Returning customers tend to write more detailed and critical reviews.



## Sample Dashboards

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

