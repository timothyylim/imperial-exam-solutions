```
MILK=COUNT[4],
COUNT[i:0..4] = (when(i>1) glass -> COUNT[i-2]
				|when(i>0) half_glass -> COUNT[i-1]
				|level[i] -> COUNT[i]
				|when(i==0) shop -> COUNT[4]).
				
```


```
RANCID = COUNT[0],
COUNT[i:0..4] = (when (i<4) nextDay -> COUNT[i+1]
				|when (i<4) {glass, half_glass,shop} -> COUNT[0]
				|when (i==4) shop -> COUNT[0]
				|{glass, half_glass} -> ERROR)
				
				
```

```
SHOPPING = (shop -> cloudy -> {beer,milk} -> SHOPPING
			|shop -> rainy -> milk-> SHOPPING
			|shop -> sunny -> beer-> SHOPPING).
```
