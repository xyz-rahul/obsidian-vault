
```java
private int atMost(int[] nums, int k) {
    int res = 0;
    int distinct = 0;
    Map<Integer, Integer> map = new HashMap<>();

    for (int i = 0, j = 0; j < nums.length; j++) {
        map.putIfAbsent(nums[j], 0);

        // If the current element is not yet in the map, increment the distinct count.
        if (map.get(nums[j]) == 0) {
            distinct++;
        }

        // Increment the count for the current element in the map.
        map.put(nums[j], map.get(nums[j]) + 1);

        // Adjust the window's left boundary to maintain 'k' distinct elements.
        while (distinct > k) {
            // Decrement the count for the element at the left boundary.
            map.put(nums[i], map.get(nums[i]) - 1);

            // If the count becomes 0, decrement the distinct count.
            if (map.get(nums[i]) == 0) {
                distinct--;
            }

            // Move the left boundary of the window.
            i++;
        }

        // If distinct elements are less than or equal to 'k', update the result.
        if (distinct <= k) {
            res += j - i + 1;
        }
    }

    return res;
}

```