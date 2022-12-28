# BOSCH'S ROUTE OPTIMIZATION

Vehicle Route Optimisation Problem is an NPC problem

Since we can’t solve this optimisation problem in Poly-time, the present algorithms don’t always guarantee
the optimal solution and are based on different type of heuristics and objective minimisation.

## Problem formulation
We are optimizing the routes a bus should take to minimize the overall cost, given the bus stop locations and no of people at each stop.

We are trying to find the no of buses that we need to buy based on our constraints. This will depend on the distance travelled cost ( petrol price per unit distance), initial investment in bus (bus price, driver salary, etc) and the returns (say earning per unit distance travelled).

Once we have the route of each bus, by assuming speed one can find the time at which the bus will be present at the node. 

## Sample Data

``` 
data['time_matrix'] = [
      [0, 6, 9, 8, 7, 3, 6, 2, 3, 2, 6, 6, 4, 4, 5, 9, 7],
      [6, 0, 8, 3, 2, 6, 8, 4, 8, 8, 13, 7, 5, 8, 12, 10, 14],
      [9, 8, 0, 11, 10, 6, 3, 9, 5, 8, 4, 15, 14, 13, 9, 18, 9],
      [8, 3, 11, 0, 1, 7, 10, 6, 10, 10, 14, 6, 7, 9, 14, 6, 16],
      [7, 2, 10, 1, 0, 6, 9, 4, 8, 9, 13, 4, 6, 8, 12, 8, 14],
      [3, 6, 6, 7, 6, 0, 2, 3, 2, 2, 7, 9, 7, 7, 6, 12, 8],
      [6, 8, 3, 10, 9, 2, 0, 6, 2, 5, 4, 12, 10, 10, 6, 15, 5],
      [2, 4, 9, 6, 4, 3, 6, 0, 4, 4, 8, 5, 4, 3, 7, 8, 10],
      [3, 8, 5, 10, 8, 2, 2, 4, 0, 3, 4, 9, 8, 7, 3, 13, 6],
      [2, 8, 8, 10, 9, 2, 5, 4, 3, 0, 4, 6, 5, 4, 3, 9, 5],
      [6, 13, 4, 14, 13, 7, 4, 8, 4, 4, 0, 10, 9, 8, 4, 13, 4],
      [6, 7, 15, 6, 4, 9, 12, 5, 9, 6, 10, 0, 1, 3, 7, 3, 10],
      [4, 5, 14, 7, 6, 7, 10, 4, 8, 5, 9, 1, 0, 2, 6, 4, 8],
      [4, 8, 13, 9, 8, 7, 10, 3, 7, 4, 8, 3, 2, 0, 4, 5, 6],
      [5, 12, 9, 14, 12, 6, 6, 7, 3, 3, 4, 7, 6, 4, 0, 9, 2],
      [9, 10, 18, 6, 8, 12, 15, 8, 13, 9, 13, 3, 4, 5, 9, 0, 9],
      [7, 14, 9, 16, 14, 8, 5, 10, 6, 5, 4, 10, 8, 6, 2, 9, 0],
  ]

  data['time_windows'] = [
      (0, 5),  # depot
      (7, 12),  # 1
      (10, 15),  # 2
      (16, 18),  # 3
      (10, 13),  # 4
      (0, 5),  # 5
      (5, 10),  # 6
      (0, 4),  # 7
      (5, 10),  # 8
      (0, 3),  # 9
      (10, 16),  # 10
      (10, 15),  # 11
      (0, 5),  # 12
      (5, 10),  # 13
      (7, 8),  # 14
      (10, 15),  # 15
      (11, 15),  # 16
  ]

  data['num_vehicles'] = 9

  data['demands'] = [0, 1, 1, 2, 4, 2, 5 , 8, 8, 1, 2, 1, 2, 4, 4, 8, 0]

  data['vehicle_capacities'] = [14, 12, 16, 12, 15, 20,12,14,20]

  data['min_capacity'] = [int(0.85*data['vehicle_capacities'][i]) for i in range(data['num_vehicles'])]

```


## Result

```
objective cost:  71

Route for vehicle 2 with min_capacity:13: and max_capacity = 16
Node:0,Time(mintime: 0, maxtime: 0),load:0 -> Node:12,Time(mintime: 4, maxtime: 4),load:2 -> Node:13,Time(mintime: 6, maxtime: 6),load:6 -> Node:15,Time(mintime: 11, maxtime: 11),load:14 -> Node:11,Time(mintime: 14, maxtime: 14),load:15 -> Node:0,Time(mintime: 20, maxtime: 20),load:15 -> Time of the route: 20min

Route for vehicle 4 with min_capacity:12: and max_capacity = 15
Node:0,Time(mintime: 0, maxtime: 0),load:0 -> Node:7,Time(mintime: 2, maxtime: 4),load:8 -> Node:1,Time(mintime: 7, maxtime: 11),load:9 -> Node:4,Time(mintime: 10, maxtime: 13),load:13 -> Node:3,Time(mintime: 16, maxtime: 16),load:15 -> Node:0,Time(mintime: 24, maxtime: 24),load:15 -> Time of the route: 24min

Route for vehicle 6 with min_capacity:10: and max_capacity = 12
Node:0,Time(mintime: 0, maxtime: 0),load:0 -> Node:9,Time(mintime: 2, maxtime: 3),load:1 -> Node:5,Time(mintime: 4, maxtime: 5),load:3 -> Node:6,Time(mintime: 6, maxtime: 7),load:8 -> Node:2,Time(mintime: 10, maxtime: 10),load:9 -> Node:10,Time(mintime: 14, maxtime: 14),load:11 -> Node:0,Time(mintime: 20, maxtime: 20),load:11 -> Time of the route: 20min

Route for vehicle 7 with min_capacity:11: and max_capacity = 14
Node:0,Time(mintime: 0, maxtime: 0),load:0 -> Node:8,Time(mintime: 5, maxtime: 5),load:8 -> Node:14,Time(mintime: 8, maxtime: 8),load:12 -> Node:16,Time(mintime: 11, maxtime: 11),load:12 -> Node:0,Time(mintime: 18, maxtime: 18),load:12 -> Time of the route: 18min

Total time of all routes: 82min
total demand satisfied  53
```