//////////////Aurora a stellar oddesey\\\\\\\\\\\\\\

Introduction
This project is a part of IIT Dh's Tech fest 'PARSEC'. This project is supposed to predict the solar radiation and goemagnetic storms in the near fututre if past data is given. We would aim only to provide the techincal details of the project [Quest_1] in this README file and explain the scientific terms whenever necessary. If you want to know why we made certain assumptions,choices or if you want to have more details on the project please do check the project report. According to the problem statement of the project, raw and unprocessed data sets were given and Disturbance Storm Index Values(dst) was used to measure the disturbances in the Earth's magnetic field due to geomagnetic storms.
Importing of necessary Modules and Files

Modules needed:

1)pandas-for reading and working data frames.
2)numpy-for the math required in data visualization and training.
3)scikit learn-(sklearn.preprocessing and MinMaxScaler)for using scalers and trainging our model.
4)keras- for training a neural network.
5)tensorflow-to support keras in the backend and other uses in model training.
6)matplotlib-for plotting graphs and other mathematical objects.

We need the following datasets:
1.sunspots_smooth.csv - Smoothed sunspot counts
2.positions_sat.csv - Coordinate positions for ACE and DSCOVR
3.solar_wind.csv - Solar wind data collected from ACE and DSCOVR
satellites 4.labels(dst).csv - Dst values averaged across the four stations

Preprocessing
This is the most crucial step of the project since the data we have been given is raw and we need to process it to turn it into meaningful features.
->Starting off with the very basic step of 'Reading and Loading files' for data analysis.
->After reading in each csv, convert the timedelta columns to an actual timedelta object using pd.to_timdelta.
Then,we adjusted the indices of each dataframe comprising of period and timedelta so as to merge the dataframes easily.
->Analysing the data helps to preprocess the data more efficiently.
1. Period columns were grouped, their max-min values,mean and standard deviations observed.
2. used the describe() feature to check the statistical features of solar_wind data.
->Null values were checked for each feature: It is good to regularly check the count of null values so that we choose are imputing method accordingly.
1. Though the propotion of null values in each feature varied, but overall a huge Null count was recieved.
2. For filling in the null values we can use different methods like imputation,interpolation,ffill etc, for such a large data frame we have chosen ffill.
Data Analysis through Visualisation ->A couple of parameters were visualised through line plot:
1. "bx_gse"
2. "bx_gsm"
3. "bt"
4. "density"
4. "speed"
5. "temperature"
-Here, the temperature data was analysed specially as it had a wide range of data value due to which we might have to use feautue scaling.
->We infered the following from the line charts:

The features 'bx_gse' and bx_gsm are closely related due to the stark resemblance in their respective line plots.
The source column was dropped to find the correlation of other data.
Correlation & Data Visualisation[Contd.]
-> A correlation matrix was plotted against all the features.
1. Speed and temp. were highly anti-correlated with correlation values ranging from [-0.6,-0.4].
2. On the other hand, other features showed their correlation ranging from [-0.2,0.4].
-> Then we plotted the graphs of datas which had the highest correlation with dst for better visualisation of data

Feature Scaling
-> Highly correlated features were shortlisted for festure scaling and next procedures...
1. "bt"
2. "temperature"
3. "bx_gse"
4. "by_gse"
5. "bz_gse"
6. "speed"
7. "density"
8. "sunspots numbers"
-> Subsets of these data were made and monthly/daily data was made hourly so as to aggregate with other features
1. Missing values when made hourly were filled using 'mean'.
2. 'smoothed_ssn' was imputed using forward fill.
3. 'solar_wind' was imputed through interpolation.

-> Standard Scaler was used for Feature Scaling: to merged and fitted the solar_wind and sunspots data

-> Modifying the shape of labels dst by data shifting as we want to predict dst of 1 hour ahead also by creating variables t0 and t1
(we are basically creating two columns t0 and t1 which will predict the dst values with 1 hour gap)
Hence we can do multi-step prediction by providing it both steps.
-List of column names for the labels joining the t0 and t1 columns with the dst dataframe

Splitting the data into training validation and test sets
-> The given data is large in size. So, the data is splitted in three different periods namely, train, test and validation
we have created a new dataframe interim which includes all the rows from the original dataframe "data" except for those whose index values matches with the index of the dataframe "test".

-> Data splits: 3 parts(width=0.75)--> "train_a", "train_b" and "train_c" were created from the existing preprocessed dataset so as to monitor the train, validation and test split counts over hourly timesteps. using plots.

Selection and training of the model

We use a Recurrent neural network called LSTM(Long Short term Memory) model for training because the dataset we have a time variant and for such projects where the signal varies with time LSTMs are best suited.
Analyse the size of features and training data and set the batchsizes,timesteps,epochs and verbose accordingly( here epochs:16, batchsize:32, timesteps:32, verbose:1, neurons:512 ).
Leave the model for training and let it complete the training.
Results
Analyse the loss function(here mse:mean squared error) and the how it decreases with the epochs and save the predictions made.
Plot graphs of actual values and predictions and check how the model is performing.You can use scatterplots,confusion matrices and error analysis through statistical functions for checking results.
As mentioned in the problem statement calculate the RMSE value (for example its close to 1.0006289211972983 ).

Conclusion
Here we can conclude the project by saving the model and its training weights for future use.

Credits
Team Leader- Dev Kaushal
Aniruddh Pandav
Kaustubh Arjun Jadhav
Ajitesh Manan Jha
Maitreyee Kumbhojkar
Richa Rajshekhar