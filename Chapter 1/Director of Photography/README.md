# [Director of Photography](https://www.facebookrecruiting.com/portal/coding_puzzles/?puzzle=870874083549040)


![Director of Photography](img/director_of_photography.png)


```python

def getArtisticPhotographCount(N: int, C: str, X: int, Y: int) -> int:
  # Write your code here
  art_photo_count = 0
  
  A_indices = []
  B_indices = []
  P_indices = []
  
  distance = range(X, Y+1)
  
  for i, s in enumerate(C):
    if s == "P":
      P_indices.append(i)
    if s == "B":
      B_indices.append(i)
    if s == "A":
      A_indices.append(i)
      
  
  for a in A_indices:
    artistic_PA = [p for p in P_indices if p <= a and a-p in distance]
    artistic_AB = [b for b in B_indices if b >= a and b-a in distance]
    
    art_photo_count += len(artistic_PA) * len(artistic_AB)
    
    artistic_AP = [p for p in P_indices if p >= a and p-a in distance]
    artistic_BA = [b for b in B_indices if b <= a and a-b in distance]
     
    art_photo_count += len(artistic_AP) * len(artistic_BA)
    
  return art_photo_count
```

Bellow one does not work, but offers a good starting point:

```python
# Write any import statements here
import itertools

def getArtisticPhotographCount(N: int, C: str, X: int, Y: int) -> int:
  # Write your code here
  res = 0
  for i, j, k in itertools.combinations(range(N), 3):
    if X <= abs(i-j) <= Y and X <= abs(j-k) <= Y \
        and C[i]+C[j]+C[k] in ('PAB', 'BAP'):
      res += 1
  return res

```
