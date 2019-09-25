# Flight-delays-using-Weather-data

The problem-statement is based on below 4 datasets .
1)weather_hour_data--Consists of weather conditions like Dewpoint , skyconditions , visibility , windspeed etc on hourly basis . 
2)weatherhpd_data -- Consists of weather_data(precipitation content) on hourly basis  .
3)Flight_details ----Consists of flight details on monthly , daily and weekly basis with scheduled and arrival details of flight .
4)AllStations_Data--- Consists of all airports like WeatherStationID,AirportID,GroundHeight,StationHeight,BarometerHeight,Latitude,Longitude,TimeZone


First we Merged weather_hour_data and weatherhpd_data  into one data frame called station_weather_hour_hpd ,with condition merge on 'WeatherStationID','YearMonthDay','Time
Next we merged AllStations_Data with station_weather_hour_hpd on merge condition  'WeatherStationID'
Extracted hours from time column of station_weather_hour_hpd and hours from scheduledDep_time & scheduledArrival_time of flight_details data .
Finally Merged station_weather_hour_hpd with flight train on "Destination","Date","Hours" and now we are ready with final data frame .

Checked if there are any flight with delay like more than one day and removed those rows ( could see 5 rows )
Created target(Flight delay) from ActualArrival timestamp and Schedule arrial timestamp and converted into below format 
Final_train_c['FlightDelay']=Final_train_c['FlightDelay'].apply(lambda x: '1' if x>= 15 else '2')
Converted the target (FlightDelay) varaible in to categorical like if delayed then 1 else 2 .

Derived new column SPEED of the flight from distance and ScheduledTravelTime columns .
Removed unnecessary columns .
Now we got good structured dataframe .
Imputed null values with mean ,mediam  mode of the respective columns .
Made necessary corrections by replacing extra characters with meaning information in columns .
Visulaized the data with matplotlib and seaborn modules .
Lable encoded the columns with categorical levels ranging like 2000 in number .
Splitted the data in to train and val .
On the test data , applied the same preprocessing stpes which applied on train and test_dataframe is ready.

Could see in the target varaibale , there is huge imbalance with delayed and not_delayed levels 
Applied smooting techinque ( from imblearn.over_sampling import SMOTE)

Model Building ::

Applied Logistic regression , XGboost and Random forests by tuning hyper parameters yeilds better F1 score of 0.51



