# Bulls And Cows

## Approach
Using hashmap to store the frequency of each character in the secret, and finding the bulls first (decreasing the frequency of that character if found bull) and then cows

- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(n)$

```java
class Solution {
    public String getHint(String secret, String guess) {
        HashMap<Character, Integer> map = new HashMap<>();
        for(char ch: secret.toCharArray()){
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }

        int x = 0, y = 0; //x -> bulls, y -> cows
        for(int i = 0; i<guess.length(); i++){
            if(guess.charAt(i) == secret.charAt(i)){
                x++;

                char ch = guess.charAt(i);
                int f = map.get(ch);
                if(f == 1){
                    map.remove(ch);
                }else{
                    map.put(ch, f-1);
                }
            }
        }

        for(int i = 0; i<guess.length(); i++){
            if(guess.charAt(i) != secret.charAt(i)){
                char ch = guess.charAt(i);

                if(map.containsKey(ch)){
                    y++;

                    int f = map.get(ch);
                    if(f == 1){
                        map.remove(ch);
                    }else{
                        map.put(ch, f-1);
                    }
                }
            }
        }

        return x + "A" + y + "B";
    }
}
```