# Data Collection and Processing for Travel Recommandations

*This project (among others) has been submitted for my Jedha Data Fullstack program certification*

## Video Presentation

**Checkout the 10min project presentation video (in French) here: https://share.vidyard.com/watch/QtiptXeWTm1SKDivRNHuj5?**

## Goal of the project 

**Create recommendations of top places to visit and hotel accomodations in France by :**  
1. **Collecting weather forecast data** via requests to the OpenWeatherMap API and processing it to create a ranking of destinations
2. **Collecting accomodation data** via web scraping of Booking.com website for a shortlist of top destinations
3. **Showing the destinations / hotels recommendations** in interactive maps

_Note : The destinations candidates are here taken from a list of ['35 cities to visit in France'](https://one-week-in.com/35-cities-to-visit-in-france/) but can be changed by modifying 'cities' object in the 'Perimeter' section of the notebook "Weather_data_collector.ipynb"._

## Getting started - Prerequisites

1. Clone this repository to create your project folder :
    ```sh
    git clone https://github.com/Acsts/Data_Collection--Travel_Recommandations.git
    ```

2. Installations : 

    All the source code is written in Python3. 
    The dependencies you need to run the code are listed in the 'requirements.txt' file, you can install them with pip by running 

    ```sh
    pip install -r requirements.txt
    ```

3. Get a free OpenWeatherMap API key by signing up at https://home.openweathermap.org/users/sign_up

4. Set your secrets variables by creating a '.env' file (don't share this file with anyone) in your project folder , and fill in your API key in it the file :

    ```sh
    OWM_API_KEY=<YOUR_OPEN_WEATHER_MAP_API_KEY>
    ```

5. _Optional - Only if you want to use your Amazon S3 account to run the last section of the notebook 'Hotels_info_collector.ipynb' :_ 
    
    Add your AWS access keys in your '.env' file (don't share it)
    ```sh
    AWS_ACCESS_KEY=<YOUR_AWS_ACCESS_KEY>
    AWS_SECRET_ACCESS_KEY=<YOUR_AWS_SECRET_ACCESS_KEY>
    ```


## Usage

### Full pipeline

The pipeline of the project consists in these 3 consecutive steps :
1. **API requests** (collect weather data) 
2. **Web scraping** (collect hotels informations)
3. **Data Vizualisation**  

You can run the full pipeline  by executing the notebooks in that order : 
1. **Weather_data_collector (Input: None -- Ouptut: 'weather_data.csv' file):** 
    - collect weather and localization data for all destinations in the scope
    - create a ranking of the destinations by computing a 'weather score' for each
    - store the data into a file in project subfolder 'data' => 'weather_data.csv' 
2. **Hotels_info_collector (Input: 'weather_data.csv' file -- Output: 'top_destinations.csv' file):**
    - Identify a short-list of top destinations (ranked by their weather score) for which we will collect hotels information
    - collect information on the most recommended hotels for each destination of the short-list by web-scraping booking.com
    - store the aggregated data (destinations localization and weather + hotels information) into a file in Amazon S3 => 'top_destinations.csv'
3. **Vizualisations_loader (Input: 'top_destinations.csv' file -- Ouptut: HTML figures):** 
    - Show recommendations on a map with : 
        - Weather score for all destinations in the scope
        - 20 Best recommended hotels for the top-5 destinations and their ratings

### Partial pipeline

If you don't want to run the whole pipeline, you can either :    
    - skip to step 2 (web scraping) by using the 'weather_data.csv' file stored in the 'data' folder of the project  
    - skip to step 3 (vizualisations) by using the 'top_destinations.csv' file stored in Amazon S3 (or the one stored in 'data' project subfolder)

## Datasets

No input dataset is used nor needed to run this project
