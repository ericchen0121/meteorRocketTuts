For example this query: 

```
	
	stats =  AthleteEventStats.aggregate([ 
			{ $match: { "api.SDPlayerId": sdPlayerId, "api.SDGameId": sdGameId } },
		 	{ $project: { _id: 0, api: 1, status: 1, sport: 1, teamId: 1, "stats.statType": "$statType", "stats.stats": "$stats", full_name: 1, position: 1 }}, 
		 	{ $group: { _id: null, allStats: {$addToSet: "$stats"}, api: {$first: "$api"}, status: {$first: "$status"}, sport: {$first: "$sport"}, teamId: {$first: "$teamId"}, full_name: {$first: "$full_name"}, position: {$first: "$position"}} } 
	])

```

I wanted to add a type into an existing object. This projects into a stats object. 
Then I add to a group with {$addToSet }. 

Finally, I actually insert these into a new Collection. 

Now I run the aggregation framework again on that new Collection. Best practice? Hardly, but the workflow is now clean and understandable how to get form point to point. 

