https://leetcode.com/problems/top-k-frequent-elements/description/
``` Java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> frequencyMap = new HashMap<>();
        List<Integer>[] bucket = new List[nums.length + 1];

        for (int num : nums) {
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }

    
        for (var key : frequencyMap.keySet()) {
            var frequency = frequencyMap.get(key);
            if (bucket[frequency] == null) {
                bucket[frequency] = new ArrayList<>();
            }
            bucket[frequency].add(key);
        }

        int[] answer = new int[k];
        int pos = 0;

        for (int i = bucket.length - 1; i >= 0; i--) {
            if (bucket[i] != null) {
                for (int j = 0; j < bucket[i].size() && pos < k; j++) {
                    answer[pos++] = bucket[i].get(j);
                }
            }
        }
        return answer;
    }
}
```
