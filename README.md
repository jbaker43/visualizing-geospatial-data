# **Dataset 1: US Wildfires**

# Description

## Dataset Format: Tabular

The wildfire [dataset](http://www.kaggle.com/datasets/rtatman/188-million-us-wildfires) was in the tabular format with items and attributes. It in in the format of an SQLite database. This dataset contained close to 2 million unique fires from that time span. It contains 54 unique columns. While for this project I will not be utilizing all 45 columns, it contained 2 important columns that were used for this which were the longitude and latitude of the fire. That combined with the class of fire allowed my to visualize this dataset.

## Data Type: Items

Since its in the tabular format, it is made up of item-based data points. That is to say that each row, or primary key in this case since it is the format of SQLite, is a unique or individual data point.

## Attribute Types and Semantics

I will not be going over all of the 54 different columns but rather jus the ones that I used. The first column that I used was the GPS coordinates. These are quantitative data points as they represent a numerical point in space and where the fire started. It is easy to see the difference in degrees from two different points. They are not categorical; they have a scale that can be used to determine different attributes about them. The next column I used was the fire class. This is a code assigned by firefighters to categorize the size of fires from class A all the way up to class G. This a categorical type. The other column that I used was the fire size column. This again is a numerical or quantitative column.

## Preprocessing

The first thing that was different for this dataset was the fact that it was in a SQLite database. This is a light and portable &#39;database&#39; file, that to the computer looks like a database but is really a file that you query. Thankfully SQLite3 is in base python so no external packages are needed. From there we need to create a connection to the file and point it to our SQLite file. Once we are connected to the file, we can write a query as if it were a MySQL database. The best part is that you can write a query that will store the results in a data frame. The best part is the speed increase and memory usage over using a .csv. Instead of loading the entire file into memory, you can just query it as if you were connected to a database. This is great for those in between dataset sizes that are too big for RAM but not big enough to justify an entire database. Regardless, we won&#39;t be able to just plot 2 million points on a map and call it a day. It would just be solid and not tell us much. So, I filtered the data frame that we created from the SQLite query down to just the worst or biggest fires, that is class G fires or fires that are greater than 5000 acres in size. That got us down to just under 4000 rows which will be a little easier to see.

## Visualization

To visualize I used plotly express. I used the scatter mapbox plot to display our fire data. Plotly makes it pretty easy to display geospatial data. Considering I could not get geopandas to install, a common problem it seems for windows users, plotly express was a breath of fresh air. I set the lat argument equal to out latitude column and the lon arg to the longitude column. From there I added the hover data of the year the fire happened and the size of the fire. ![](https://i.imgur.com/wP4BEPf.png)

_Figure 1 US Wildfires form 1995-2015_

![](https://i.imgur.com/zvtnAHj.png)

_Figure 2 Alaskan Wildfires_

![](https://i.imgur.com/CFdhPgE.png)

_Figure 3 Wildfires in the north east_

## Analysis

The first thing that I noticed was why there are so many wildfires. In my mind when I think of a wildfire, I imagine a huge raging inferno that is consuming wide swaths of land. That&#39;s why I was so shocked to see that there have been 1.8 million wildfires. However, a wildfire can be quite small. In fact, there really is no lower limit to what constitutes a wildfire. The key is that it is wild. So that was why I had to filter the dataset down to what I think most people would imagine a wildfire to be. With that being said, the next thing that I noticed and was surprised by was the heavy concentration of class g wildfires in Alaska. Turns out it&#39;s a [huge issue](https://www.scientificamerican.com/article/wildfire-is-transforming-alaska-and-amplifying-climate-change/) that I had no idea about. When looking at each fire in Alaska, most of them happened more recently, 2010 to present. This is apparently a new phenomenon driven by climate change. The second interesting discovery was the 4 class g fires that happened in the New Jersey Pinelands National Reserve. There was actually a fair amount of class g fires up and down the east coast which surprised me. Finally, as expected the highest concentration of wildfires was west of the Rocky Mountains in California, and surrounding states. Finally, there are a lot of places that haven&#39;t experienced a class G wildfire. States like Indiana, Ohio, Pennsylvania. However it appears that the Gatlinburg Wildfire was a class g.

# **Dataset 2:**

# Description

## Dataset Format: Tabular

The second [dataset](https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page) I chose was from the New York City taxi commission, or TLC board. I chose an arbitrary month, May of 2016 and looked at it. This was also a tabular dataset in the form of 1.8gb .csv file. Yikes. Regardless my computer has 32gb of ram so it should be able to handle this no problem, albeit a little slow to ingest, and use a fair amount of memory. It contains close to 12 million unique taxi trips taken in the month of May.

## Data Type: Items

Since it&#39;s in the tabular format, it is made up of item-based data points. That is to say that each row is a unique or individual data point.

## ­­Attribute Types and Semantics

The dataset is made up of 19 unique columns. Almost all of them are quantitative data types. The only columns that are not quantitative are the VendorID, RatecodeID, and the store\_and\_fwd\_flag columns which are categorical. You could easily apply a scale to all of the 17 other columns enforcing that they are quantitative.

## Preprocessing

The first thing that I needed to do was to load this entire dataset into a data frame to get a look at it. After doing that I noticed a few things. For this visualization I want to do a density map of people who do not tip their cap driver. To accomplish this the first thing I need to clean up is the coordinates. A lot of entries had 0 for both their latitude and longitude. Thus, I needed to filter this down to trips that had a longitude of anything less than 0. Its less than 0 since we are in the western hemisphere. And then a latitude that was greater than 0. That go us down to 11.6 million rows. Not a big reduction but still noticeable. Next, I needed to filter out anyone who tipped, as well as anyone who paid cash. The reason Is that when someone pays cash a tip is not reported regardless of if they tipped or not. Finally, I needed to filter it down to the rate code of just 1. This means that it was a standard taxi ride. Not a negotiated far or flat fair. Finally, since there are still so many trips and we won&#39;t be able to display them, at least not with my computer, I did a random sample of 10000 rides.

## Visualization

For my visualization, I used plotly express again. This time I used the desity\_mapbox plot. I really wanted to see where these trips originated from not so much where they ended, so I se the lat and lon args to their respective pickup coordinates in the data frame.

![](https://i.imgur.com/M8xRTPv.png)

_Figure 4 All 10,000 Rides_

![](https://i.imgur.com/GU0zspo.png)

_Figure 5 Outside the main entrance to Central Park_

![](https://i.imgur.com/jEnaatP.png)

_Figure 6 Outside of LaGuardia Airport (LGA)_

# Analysis

The first thing that it apparent is that this is not a perfect way of looking at the data. You must go look for trends. If not, it just looks like the entire city never tips their cab drivers. This defiantly not he case. My first thought was that tourist don&#39;t tip as often simply because they don&#39;t know you&#39;re supposed to tip their drivers. So, I started to look in tourist hot spots likes the main entrance to Central Park, LaGuardia Airport, One World Trade, Madison Square Garden, etc. Sure, enough here does appear to be more in these areas. I am not sure if that means I am correct or not, but still, it appears that these areas have more non-tipping fares than others. One explanation for this is that these are all credit card fares. One thing that could be happening is that the rider tips in cash and that would be reported as a $0 tip. We unfortunately have no way of knowing if that is the case or not however and that is just speculation.

# Dataset 3:

# Description

## Dataset Format: Geometry

The third [dataset](#https://www.kaggle.com/datasets/tipsijadav/covid19-ct) I found was a collection of brain tumor progression scans. I chose the geometry category since they are .nii files and are spatial. I must admit I was far outside of my comfort zone on this type of dataset.

## Data Type: Positions

I chose positions since the .nii file type represent a bunch of slices and each slice represents spatial data.

## ­­Attribute Types and Semantics

The dataset contains ct scans from 11 different patients with brain tumors. Each patents has four different scans. A pre and post scan of two types, mask, and scan. I am not aware of the time between the two scans, nor am I aware of the differences in the types of scans.

## Visualization

To visualize the .nill files. I first chose a random patient. I then used the package nilearn and nibabel to plot these .nii files. Using the built in function plotting.plot\_img from the nilearn package, we can plot all four images.

![](Rhttps://i.imgur.com/GDY8HbC.png) 
![](https://i.imgur.com/o1nXxFi.png)

## Analysis

As stated above, I was out of my comfort zone on this dataset. I am about the farthest thing from a doctor and am not pretending to understand how to effectively read a CT image. Regardless though we can clearly see the increase in the size of the tumor grow between the two scans. The biggest challenge I faced for the third dataset was first finding appropriate data, and secondly knowing what to look at. I can see the value of knowing how do this if you were in the medical field, or using these dataset in machine learning to build a model to detect certain things.

##

##

##

## Extra Visualization

For fun I also included a point cloud visualization that I made with the lidar camera on my iPhone. I used the app Polycam to take a point cloud representation of my bedroom/office. I then used Open3d to visualize it in python. You can see this in the pointcloud.py file.

![](https://i.imgur.com/P1C67xh.png)
