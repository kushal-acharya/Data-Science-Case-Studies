# Project Title : New York Taxi Demand Prediction

Inline-style:
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png)

## Problem Statement
In this case study, we will try to predict the number of pickups for yellow taxi at any given region of New York city for the next ten minutes time interval given historically collected data and data from previous time step.

The problem is a time-series forecasting problem.

The prediction results can be then transferred to taxi drivers through Smartphone app. The drivers then can subsequently move to the locations where the predicted number of pickups are high.

## Constraints

**Latency**
Some latency is acceptable, in the order of a few seconds.

**Interpretability**
The model need not be interpretable as long as the drivers are getting highly accurate results. Accuracy is of more importance than interpretability.

## Source of Data
The datasets used for this case study was collected by the NYC Taxi and Limousine Commission (TLC) and can be obtained from the following url :

https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page

For this case study we use the data of Jan 2015 and Jan 2016. We will try to predict pickups for Jan 2016 and check our prediction accuracy against the original data.

## Features in the dataset:
<table border="1">
	<tr>
		<th>Field Name</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>VendorID</td>
		<td>
		A code indicating the TPEP provider that provided the record.
		<ol>
			<li>Creative Mobile Technologies</li>
			<li>VeriFone Inc.</li>
		</ol>
		</td>
	</tr>
	<tr>
		<td>tpep_pickup_datetime</td>
		<td>The date and time when the meter was engaged.</td>
	</tr>
	<tr>
		<td>tpep_dropoff_datetime</td>
		<td>The date and time when the meter was disengaged.</td>
	</tr>
	<tr>
		<td>Passenger_count</td>
		<td>The number of passengers in the vehicle. This is a driver-entered value.</td>
	</tr>
	<tr>
		<td>Trip_distance</td>
		<td>The elapsed trip distance in miles reported by the taximeter.</td>
	</tr>
	<tr>
		<td>Pickup_longitude</td>
		<td>Longitude where the meter was engaged.</td>
	</tr>
	<tr>
		<td>Pickup_latitude</td>
		<td>Latitude where the meter was engaged.</td>
	</tr>
	<tr>
		<td>RateCodeID</td>
		<td>The final rate code in effect at the end of the trip.
		<ol>
			<li> Standard rate </li>
			<li> JFK </li>
			<li> Newark </li>
			<li> Nassau or Westchester</li>
			<li> Negotiated fare </li>
			<li> Group ride</li>
		</ol>
		</td>
	</tr>
	<tr>
		<td>Store_and_fwd_flag</td>
		<td>This flag indicates whether the trip record was held in vehicle memory before sending to the vendor,<br\> aka “store and forward,” because the vehicle did not have a connection to the server.
		<br\>Y= store and forward trip
		<br\>N= not a store and forward trip
		</td>
	</tr>

	<tr>
		<td>Dropoff_longitude</td>
		<td>Longitude where the meter was disengaged.</td>
	</tr>
	<tr>
		<td>Dropoff_ latitude</td>
		<td>Latitude where the meter was disengaged.</td>
	</tr>
	<tr>
		<td>Payment_type</td>
		<td>A numeric code signifying how the passenger paid for the trip.
		<ol>
			<li> Credit card </li>
			<li> Cash </li>
			<li> No charge </li>
			<li> Dispute</li>
			<li> Unknown </li>
			<li> Voided trip</li>
		</ol>
		</td>
	</tr>
	<tr>
		<td>Fare_amount</td>
		<td>The time-and-distance fare calculated by the meter.</td>
	</tr>
	<tr>
		<td>Extra</td>
		<td>Miscellaneous extras and surcharges. Currently, this only includes. the $0.50 and $1 rush hour and overnight charges.</td>
	</tr>
	<tr>
		<td>MTA_tax</td>
		<td>0.50 MTA tax that is automatically triggered based on the metered rate in use.</td>
	</tr>
	<tr>
		<td>Improvement_surcharge</td>
		<td>0.30 improvement surcharge assessed trips at the flag drop. the improvement surcharge began being levied in 2015.</td>
	</tr>
	<tr>
		<td>Tip_amount</td>
		<td>Tip amount – This field is automatically populated for credit card tips.Cash tips are not included.</td>
	</tr>
	<tr>
		<td>Tolls_amount</td>
		<td>Total amount of all tolls paid in trip.</td>
	</tr>
	<tr>
		<td>Total_amount</td>
		<td>The total amount charged to passengers. Does not include cash tips.</td>
	</tr>
</table>

## Performance metrics

This is a time-series regression problem, thus we will use the following errors as performance metrics.

1. Mean Absolute percentage error.
2. Mean Squared error.

Here, we will focus more on Mean Absolute Percentage Error as we want the relative error in the number of pickups that we predict. Let's take an example to understand why relative error is more desirable than raw numerical error.

For this let's take two scenarios.

Scenario 1

------------
Total predicted pickups  -> 100
Actual/Correctly predicted pickups -> 94
Error -> 6

Percentage Error = 6%

Scenario 2

---------------

Total predicted pickups  -> 10
Actual/Correctly predicted pickups -> 4
Error -> 6

Percentage Error = 60%

Here, in both the cases the number of errors are same. In the first case predicting 6 extra pickups among 94 correctly predicted pickups is fine, as it doesn't impact the  overall experience/expectation of the cab driver but in the second scenario predicting that there are 10 pickups only to find 4 pickups is a very high discrepancy and affects the end user experience much.

Thus, we want to minimize the percentage / relative error not the absolute numerical error itself.


I have documented/commented the notebook to the best of my ability so that it will be easier for anyone to go through it.

**Note**

The notebook uses dask dataframe instead of pandas for faster computation. Similarly, install required libraries in your environment if you encounter any error.
