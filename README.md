# Data Collection, Preprocessing and Model Training
In this course, I worked primarily on the following: A Data Collector Module that can download data through any API; an Advanced Data Preprocessing Module that can process time series data even when the time has been entered in a haphazard fashion, handle missing data through imputation, and output the data in a specified format; a Time Converter Module that can break the Datetime into different components- year,month,day,hour,minute,second and can facilitate prediction on any of those components, an XGBoost Model Training Module, and a Random Forests Training Module. I also created an AWS sagemaker notebook instance that can collect data from an S3 bucket, pre-process the data and store it in another S3 bucket. Apart from the above, I also presented on the standard steps in Data preprocessing and pattern matching through Regular Expressions.
# Data Collector
The module uses the Python package alpha_vantage to collect stock price timeseries data for a given Symbol, Frequency and output the data to a csv file. The image below shows how the module works. The object of class settings hold all attributes of the time series to be downloaded and the name, format and location of the output file. 
![Collecting Data from Alpha Vantage API](https://github.com/simrita/Simrita-STAT--359/blob/master/Data_Collector.png)
# Data Preprocessor
The module uses the Python packages datetime, dateparser and sklearn for reading dates in a way that mirrors human readibility, converting the dates to a specified format and imputing the missing values through a specified strategy. The Data Preprocessor works as follows
1. The raw data file is loaded into a pandas dataframe
2. The dateparser reads the datetime and converts into the standard format of ('YYYY:MM:DD HH:MM:SS')
3. Multiple entries corresponding to the same datetime are aggregated via mean, and the dataset is sorted by the datetimes
4. The Frequency of the timeseries data is identified by finding the "most frequent successive difference"
5. The complete range of datetimes is constructed using the minimum datetime, the maximum datetime, and the Frequency of the datetimes
6. A new time series dataset is constructed such that the datetime is the complete range of datetimes described above, stock prices for the datetimes present in the original dataset are copied directly from there, while for those datetimes not present in the original dataset, the stock prices for the datetimes not present in the original dataset are imputed. We find that a simple mean imputation works reasonably well most of the times. 
![Inferring Frequency and The complete range of datetimes](https://github.com/simrita/Simrita-STAT--359/blob/master/inferring_frequency.png)
# Time Converter
This module takes as input a preprocessed dataset, and outputs a dataset containing the different components of the datetime 
![Time Converter](https://github.com/simrita/Simrita-STAT--359/blob/master/time_converter.png)
