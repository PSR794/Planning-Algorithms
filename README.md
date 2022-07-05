# **Planning-Algorithms**
## Mission PLanning 
* Implementation of global planning algorithms- Dijkstra's and A* on a road network of California.
* For the A* star algorithm, the heuristic used is Euclidean distance.
### The Pseudo Codes:
  > * **Dijkstra's**
  ><img src="https://i.imgur.com/Bu7WwbO.png" width="300">
  
  > * **A***
  ><img src="https://i.imgur.com/cd4I13g.png" width="300">
  
### RESULTS
 >* For both
 > <img src="https://user-images.githubusercontent.com/64797216/125813787-33912fec-3ba2-4812-8f7b-65eececc51ac.png">

### Resources
* [Motion Planning for Self-Driving Cars(Coursera)](https://www.coursera.org/learn/motion-planning-self-driving-cars/home/week/3)
* [Mobile Sensing and Robotics](https://youtube.com/playlist?list=PLgnQpQtFTOGQJXx-x0t23RmRbjp_yMb4v)

## Occupancy Grid Generation
- Each cell represented by $m^i$, so $p(m^i)$ gives the probability of the cell being occupied.
- From the bayesian filter we have, $bel_t(m) = \eta p(y_t|m)bel_{t-1}(m)$
- Some probability values cannot be calculated due to rounding errors in small values as the range of this function is $[0,1]$
- Hence we change the range by taking the log odds ratio which calculates the logarithmic ratio of success/probability of failure.
- This maps the range of $[$$0,1$$]$ $\to$ $[$$-\infin$ , $+\infin$$]$
- So $Logit(p) = log(\frac{p}{1-p})$
- The final equation we get is $l_{t,i} = logit(p(m^i|y_t)) + l_{t-1,i} - l_{0,i}$
- $l_{t-1,i}$ - previous belief
$l_{0,i}$   - initial belief
- For assigning initial probabilities we use the inverse measurement  module. For this two parameters are defined, $\alpha$ and $\beta$ which defines the affected range of cells by the LiDAR beam, the high/low probability cells and the no information cells are marked by using these two parameters.
- If it is less then it is likely to be empty hence $p = 0.3$
- And if the difference between the distance and measured range is less than a threshold depending on $\alpha$ then it is considered to be occupied.
