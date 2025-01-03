# Shopping Offers

## Approach -> (DP MEMOIZATION):
Memoizing the whole needs array using a map which stores the minimum cost to fulfil those needs.

- **Time Complexity:** O()
- **Space Complexity:** O()
  

```cpp
class Solution {
public:
    int dot(vector<int> &price, vector<int> needs){
        int sum = 0;
        for(int i = 0; i<needs.size(); i++){
            sum += price[i] * needs[i];
        }

        return sum;
    }

    int helper(vector<int> &price, vector<vector<int>>& special, vector<int> needs, map<vector<int>, int> &mp){
        if(mp.count(needs) == 1){
            return mp[needs];
        }

        int ans = dot(price, needs);
        for(vector<int> offer: special){
            vector<int> newNeeds(needs.size(), 0);

            bool canTake = true;
            for(int i = 0; i<needs.size(); i++){
                if(needs[i] < offer[i]){
                    canTake = false;
                    break;
                }else{
                    newNeeds[i] = needs[i] - offer[i];
                }
            }

            if(canTake){
                ans = min(ans, offer.back() + helper(price, special, newNeeds, mp));
            }
        }

        return mp[needs] = ans;
    }

    int shoppingOffers(vector<int>& price, vector<vector<int>>& special, vector<int>& needs) {
        map<vector<int>, int> mp;

        return helper(price, special, needs, mp);
    }
};
```