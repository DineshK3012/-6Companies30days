# [Run Length Encoding](https://www.geeksforgeeks.org/problems/run-length-encoding/1)

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$


```java
class Solution {
    public static String encode(String str) {
        if(str.length() == 0){
	        return "";
	    }
	    
        StringBuilder output = new StringBuilder(str.charAt(0) + "");
        int count = 1;
        for(int i = 1; i<str.length(); i++){
            if(str.charAt(i) == str.charAt(i-1)){
                count++;
            }else{
                output.append(count).append(str.charAt(i));
                count = 1;
            }
        }
        output.append(count);
        
        return output.toString();
    }
}
```