## Introduction

_Last modified: May 29th, 2020_

Privacy budgeting is a concept taken from the world of differential privacy whereby a data owner can allocate a certain amount of information that a data scientist querying on private data should be able to make. More specifically, it is a number that measures how much information could theoretically be leaked from a private dataset by the work that's being requested.

In other words, a data scientist may decide to use a dataset that has 10,000 rows of data, each with 10 columns. If the data scientist writes code to compute against the entire dataset (a total of 100,000 unique datapoints), this has a far higher amount of potential privacy leakage than the same code running against 2,000 rows and across 5 columns of data (a total of 10,000 unique datapoints). Even though the data being used in the training is kept private and all training happens under the compute control of the data owner, it's theoretically possible to leak information from any ML model, regardless of the privacy techniques being used. This is precisely why we need to measure privacy leakage - allowing a data compliance officer the ability to make an informed decision.

### Metrics

Other than the measureable amount of privacy leakage, there are many other potential metrics that we will likely want to use to allow a data compliance officer to be well informed in their responsibilities. This is not a complete list and will likely change over time - our current ideas for useful metrics for measuring privacy leakage are:

#### The percentage measuring the privacy leakage of the current data request, versus the entire allotted privacy budget for a given user or group
You could measure this statistic mathematically as:

```
c = current_spend
b = overall budget

x = c / b
```

While rather simplistic in its calculation, this would allow the data owner the ability to measure the perceived importance of the current request to the data scientist. If the data scientist is looking to make multiple requests, they will need to be careful about how quickly they spend their alloted privacy budget. Otherwise, they will need to request to renegotiate their privacy budget with the data owner, or simply request less data.

#### Measuring how "average" a request is against all other requests in the past
This would simply allow a data compliance officer to see how normal the current data request is, compared to requests they've approved in the past. While this is still a relative metric, it may be important for allowing the data compliance officer to get a quick overview of the size of the request.