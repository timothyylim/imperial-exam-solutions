```
MILK=COUNT[4],
COUNT[i:0..4] = (when(i>1) glass -> COUNT[i-2]
				|when(i>0) half_glass -> COUNT[i-1]
				|level[i] -> COUNT[i]
				|when(i==0) shop -> COUNT[4]).
				
```
