# [Find Beautiful Indexes in an Array](https://leetcode.com/problems/find-beautiful-indices-in-the-given-array-i/description/)

## Approach (Using KMP)
- Used KMP algorithm to find all the indexes of string a and b in string s;
- Then use binary search to find on both the indices array to find the beautiful indices.

---

- **Time Complexity:** $O(n + k)$, where n is the length of string s and k is the length of pattern (a or b);
- **Space Complexity:** $O(n) + O(k) => O(n)$


```java
class Solution {s
     public int[] LPS(String pat){
        int lps[] = new int[pat.length()];
        int length = 0;
        int i = 1;
        while(i < pat.length()){
            if(pat.charAt(i) == pat.charAt(length)){
                length++;
                lps[i] = length;
                i++;
            }else{
                if(length != 0){
                    length = lps[length - 1];
                }else{
                    lps[i] = 0;
                    i++;
                }
            }
        }
        
        return lps;
    }
    
    public ArrayList<Integer> search(String txt, String pat) {
        int lps[] = LPS(pat);
        
        ArrayList<Integer> result = new ArrayList<>();
        int i = 0, j = 0;
        while(i < txt.length()){
            if(txt.charAt(i) == pat.charAt(j)){
                i++;
                j++;
            }else{
                if(j != 0)
                    j = lps[j-1];
                else
                    i++;
            }
            
            
            if(j == pat.length()){
                result.add(i-j);
                j = lps[j-1];
            }
        }
        
        return result;
    }

    public static int lowerBound(ArrayList<Integer> list, int value) {
        int low = 0, high = list.size();
        
        while (low < high) {
            int mid = low + (high - low) / 2;
            if (list.get(mid) < value) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        return low;
    }

    public List<Integer> beautifulIndices(String s, String a, String b, int k) {
        ArrayList<Integer> indexA = search(s, a);
        ArrayList<Integer> indexB = search(s, b);
        List<Integer> ans = new ArrayList<>();

        if(indexA.size() == 0 || indexB.size() == 0){
            return ans;
        }

        for(int index: indexA){
            int r = index + k;
            int l = index - k;

            int x = lowerBound(indexB, l);
            if(x < indexB.size() && indexB.get(x) <= r && Math.abs(indexB.get(x)-index) <= k){
                ans.add(index);
            }
        }

        return ans;
    }
}
```