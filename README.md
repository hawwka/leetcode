https://leetcode.com/problems/top-k-frequent-elements/description/
``` Java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> seen = new HashMap<>();
        for (int num : nums) {
            seen.put(num, seen.getOrDefault(num, 0) + 1);
        }
        List<Integer>[] buckets = new List[seen.size() + 1]; // Потому что подсчет частот начинается с 1
        for (var key : seen.keySet()) {
            if (buckets[seen.get(key) - 1] == null) {
                buckets[seen.get(key) - 1] = new ArrayList<>();
            }
            buckets[seen.get(key) - 1].add(key);
        }
        int[] answer = new int[k];
        int pos = 0;
        for (var i = buckets.length - 1; i >= 0; i--) {
            if (buckets[i] == null)
                continue;
            for (var value : buckets[i]) {
                answer[pos++] = value;
                if (pos >= k) {
                    return answer;
                } 
            }
        }
        return answer;
    }
}
```
