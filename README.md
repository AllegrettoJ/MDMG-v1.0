# Multi-Day-Multi-Group(MDMG) Itinerary Recommendationg
These python codes aim to recommend personalized group tours for different travelling days. We first cluster the users using 2 clustering methods: random & kmeans; and then solve the problem as an integer programming in order to recommend an ideal itinerary to each group. The package we used is pulp.  
The dataset used can be found at https://sites.google.com/site/limkwanhui/datacode#icaps16, which is collected and formed in the following paper.    
1.) Kwan Hui Lim, Jeffrey Chan, Christopher Leckie and Shanika Karunasekera. "Towards Next Generation Touring: Personalized Group Tours". In Proceedings of the 26th International Conference on Automated Planning and Scheduling (ICAPS'16). Pg 412-420. Jun 2016.   
The idea of constrained clustering k-means is from   
2.)Pourrajabi, M.; Moulavi, D.; Campello, R. J. G. B.; Zimek, A.; Sander, J.; Goebel, R. (2014). "Model Selection for Semi-Supervised Clustering". Proceedings of the 17th International Conference on Extending Database Technology (EDBT). pp. 331–342.   
And the source code of cop-kmeans is adopted from https://github.com/Behrouz-Babaki/COP-Kmeans.git

## Included Files
### Code Files  
**tourrecomm.py**: The main code which is used to do the pre-processing (forming tour groups whose members have similar interests; decide the travelling day, budget and startNode/endNode).  
**poi2group.py**: This file is to find the each group's visiting interests from tourrecomm.py, and call the integer progrmming function to do the recommendation.  
**tourrecomm.py**: This file contains the integer progrmming formulation, including obejctive function, decision variables, and constraints.  
**calcinterest.py**: This file is used to calculate the average visiting time for each POI.  
**calcStat.py**: We use this file to do different statistics calculation, such as Cosine similarity, Jaccard similarity.  
### Data Files
**costProfCat-ToroPOI-all.csv**: Sample input data in the form of a cost-profit table, with the following columns/fields: "fromNode", "toNode", "cost", "profit" and "category"  
**userVisits-Toro-allPOI.csv**: Sample input data in the form of user-POI visits, with the following columns/fields: "photoID", "userID", "dateTaken", "poiID", "poiTheme", "poiFreq", "seqID"  
**userInt-URelTime-Toro.csv**: Sample input data in the form of user interest levels, with the following columns/fields: "userID", "Cultural", "Amusement", "Shopping", "Structure", "Sport", "Beach"  
## Results Files
**recommend_POI_Results.csv**: The results of Tour Solution
### Parameters
- 'algo': The method used to do the clustering 
- 'startNode/endNode': The start and end node for the itinerary. We assume all the group has the same start and end node everyday. 
- 'budget': The time budget for one day. The budget is calculated from the real travelling history from userVisits-Toro-allPOI.csv.  
- 'totalPOI': How many POIs user visited (the startnode and endnode are not counted)
- 'totalCost': The total time used for the itinerary, including visiting time and travelling time
- 'totalProfit': The total popularity of the POIs user visited
- 'totalInterest': Each user's total interests for the POIs'category he/she visited
- 'reachEndNode': Whether the ideal itineray is found. If found, reachEndNode = True
- 'totalPopInt': totalPopInt is to calculate both popularity of POIs and each user's preference. The fomulation is totalPopInt = 0.5 * totalProfit + 0.5 TotalInterest. We use 0.5 as the weight between totalProfit and totalInterest.
- 'maxInterest': User's maximum interset of category which is also recommended to the whole Itinerary
- 'minInterest': User's minimum interset of category which is also recommended to the whole Itinerary
- 'tour': The total tour of itinerary, using the '-' to link two POIs  

**results_statistics.csv**: The statistics calculation of each group    
### Parameters
- 'iter': The number of current iteration, there are total 335 loops
- 'groupSize': The number of users in the group
- 'intCosSim': The cosine similarity of each group
- 'intCosSimBin': The cosine similarity of each group using the binary value, that means all the non-zero continues values are converted to 1
- 'topintRatio': Calculate the largest ratio of users in the group
- 'intJaccard': Calculate the Jaccard similarity for each group

**results_average.csv**: The average results for each iteration
