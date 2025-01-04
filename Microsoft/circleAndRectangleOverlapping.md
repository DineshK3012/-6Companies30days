# Circle And Rectangle Overlapping

## Approach:
Find the nearest point on the rectangle which is closer to the circle and check if the distance between that point and circle center is smaller than the radius of the circle or not, if yes then overlapping otherwise not overlappaing

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)


```java
class Solution {
    public boolean checkOverlap(int radius, int xCenter, int yCenter, int x1, int y1, int x2, int y2) {
        int nearestX = Math.max(x1, Math.min(x2, xCenter));  
        int nearestY = Math.max(y1, Math.min(y2, yCenter));
        
        int distance = (xCenter - nearestX) * (xCenter - nearestX)  + (yCenter - nearestY) * (yCenter - nearestY);
        
        return distance > radius * radius ? false : true; 
    }
}
```