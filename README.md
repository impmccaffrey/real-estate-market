# MLS Real Estate Data Exploration and Forecasting

This project explores real estate data trends and makes some prediction for future outcomes. Of particular interest is predicting active listings by month.

## Motivation
 It is at the present *very* difficult to purchase a house in the market I am interested in, which in my case are the exurbs of the Boston metro. Housing inventory seems to be nonexistent. It's a bad sign when you open Zillow in the morning to find every house has already been clicked on, and no new ones are being added.
 
 I'm mainly motivated by gathering some data on when I expect the housing inventory to pick, and by what magnitude will it increase by. I don't need to pick the time of year when prices are lowest. Instead, I want some idea of when the feeding frenzy might relax.
## Getting Started
This was developed with `jupyterlab v2.2.9` and `Python 3.8`.

Install the prerequisite Python packages by running in your terminal `pip -r requirements.txt`

Create your personal `zipcodes.csv` file, per the [instructions](#Data-Files) below in this readme.

Start by running [download-mls-data](download-mls-data.ipynb) notebook to get the data.

Then run the [fb-prophet-forecast](fb-prophet-forecast.ipynb) notebook to create your market predictions.

The R packages can be installed inside of the notebook.
## Data Files
Most of the data files are provided by [Realtor.com Research Data](https://www.realtor.com/research/data/). The inventory data dates back to July 2016 on a monthly basis.

The other data file you will need is `zipcodes.csv`. You will need to create this yourself. The schema is:
| Zipcode | City                |Rank
| --------| -----------         | ---
| 90210   | Beverly Hills, CA   | 2
| 03301   | Concord, NH         | 1
| 10017   | New York, NY        | 2

Where Rank is a an at this time unused ranking I gave the various zipcodes based on how desirable I think living in them in. It is unused but I have created in case I wish to implement certain weighted scores in the future.

This purpose of `zipcodes.csv` is to provide a filter on the original MLS dataset. Thus, the novelty here is to predict housing trends _only in the regions you are interested in_. From a modeling persepective, it makes sense if these are geographically adjacent. Think of it like creating your own personal county.

### Errata
I've noticed an error in the source Realtor.com data, notably that `postal_code` has the leading 0 stripped of it, for postal_codes that begin with 0.

## TODO
- [ ] Import the .csv files into a database
- [ ] Manage an ETL to append only the _new_ data into the appropriate DB table. I want to save the oldest data in case Realtor.com's csv files have a fixed row limit.
- [ ] Fix the data errata like stripping 0s from zipcodes upon data import