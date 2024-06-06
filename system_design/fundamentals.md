### Back of the Envelope Estimation:
| Power of 2 | Number of Zeros     | Data |
|------------|---------------------|------|
| 10         | 10^3 - Thousand     | 1 KB |
| 20         | 10^6 - Million      | 1 MB |
| 30         | 10^9 - Billion      | 1 GB |
| 40         | 10^12 - Trillion    | 1 TB |
| 50         | 10^15 - Quadrillion | 1 PB |

### Example: Estimate Twitter QPS and storage requirements
Please note the following numbers are for this exercise only as they are not real numbers from Twitter. <br/>

##### Assumptions:

1. 300 million monthly active users.
2. 50% of users use Twitter daily.
3. Users post 2 tweets per day on average.
4. 10% of tweets contain media.
5. Data is stored for 5 years.

##### Estimations:

Query per second (QPS) estimate:
1. Daily active users (DAU) = 300 million * 50% = 150 million
2. Tweets QPS = 150 million * 2 tweets / 24 hour / 3600 seconds = ~3500
3. Peek QPS = 2 * QPS = ~7000

##### We will only estimate media storage here.
Average tweet size: <br/>
1. tweet_id: 64 bytes
2. text: 140 bytes
3. media: 1 MB

Media storage: 150 million * 2 * 10% * 1 MB = 30 TB per day <br/>
5-year media storage: 30 TB * 365 * 5 = ~55 PB <br/>

