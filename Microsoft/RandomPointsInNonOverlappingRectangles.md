# RandomPoints In Non-Overlapping Rectangles

## Approach:
Create a TreeMap, find the area of rectangles and store the cumulative sums of areas of rectangles with their index.
Now in the pick function generate a random number beetween 1 to totalAreaSum and find a ceiling key in the map for that and you get the index of the rectangle from the map, now generate random X and Y value of the point between the rectangle.

- **Time Complexity:** $O(nlogn)$, to add all the values in the treeMap
- **Space Complexity:** $O(n)$, to store n triangles with cumulative sum areas with their index

```java
class Solution {
    int[][] rs;
    TreeMap<Integer, Integer> map;
    int sum;

    public Solution(int[][] rects) {
        rs = rects;
        int n = rects.length;
        map = new TreeMap<>();
        sum = 0;

        for(int i = 0; i<n; i++){
            int[] rect = rects[i];

            sum += (rect[2] - rect[0] + 1) * (rect[3] - rect[1] + 1);
            map.put(sum, i);
        }
    }
    
    public int[] pick() {
        Random random = new Random();
        int j = map.ceilingKey(random.nextInt(sum) + 1);
        int i = map.get(j);

        int point[] = new int[2];
        point[0] = random.nextInt(rs[i][2] - rs[i][0] + 1) + rs[i][0];
        point[1] = random.nextInt(rs[i][3] - rs[i][1] + 1) + rs[i][1];
        
        return point;
    }
}
```