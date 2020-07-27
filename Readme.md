Link to Live Tabluae Dasbaord: https://tabsoft.co/3axmz8j

This is the second version of the Google Serch Trends API. 

Having completed the initial testing of the first version. The next step was to create a series of functions in line with the principles of object-oriented programming. 

Initially was created in a linear format as a proof of concept. Later split the code into five main functions. 

1. create_unique_directory():

The purpose of this function is to create a unique directory based on the current date and time stamp. Executes each time the process is run and used to store the payloads received by the following three functions. 

2. get_interest_over_time(month):

The purpose of this function is to retrieve the interest over time as a time-series data for the main keyword specified in the keyword collection. Either with a time frame of 1 or 2 months. The time frame is specified though the month parameter. The API returns the data in the format of a DataFrame.

3. get_related_queries(month):

The purpose of this function is to retrieve search terms related to the main keyword specified in the keyword collection. Either with a time frame of 1 or 2 months. The time frame is specified though the month parameter. The API returns the data in the format of a data dictionary which is then converted to a DataFrame. The dictionary comes with top keyword and rising keywords. The final DataFrame consists of top keywords portion of the dictionary.

4. get_interest_by_region(month): 

The purpose of the function is to retrieve interest by region within the specified geography for the main keyword specified in the keyword collection. Either with a time frame of 1 or 2 months. The time frame is specified though the month parameter. The API returns the data in the format of a DataFrame.

5. concat_payloads(pd_payload_one, pd_payload_two):

The purpose of this function is the concatenate two DataFrames into one single DataFrame which is then stored in a CSV file. 

The keyword collection is specified as follows. The keyword list collection can take up to 5 keywords.
kw_list = ["covid"]

The time frame is determined by the month parameters and returns the following output in the format required by the Google API.
    if month == 1:
        time_frame = "today 1-m"
    elif month == 3:
        time_frame = "today 3-m"

Besides specifying the time frame we also need to specify the geography through the geo parameter. 
pytrends.build_payload(kw_list, cat=0, timeframe=time_frame, geo='GB', gprop='')

Each function consists of a series of commands that build the payload, execute the payload request modify the structure of the DataFrame, renames columns, adds additional columns to meet the requirements of the data specifications, sorts the data in a specific order and finally returns the DataFrame with just the required columns.

For this particular project, each of the get_ functions is used twice. Once to get 30-days of data and a second time to get 90-days of data. Both DataFrames are passed to the concat_payloads(). The retuned output is then stored in a CSV file. 

The code itself is well commented and each step of the process is printed out on screen for verification along with other specific actions taken such as creating the directory and saving the payloads to CSV file. 