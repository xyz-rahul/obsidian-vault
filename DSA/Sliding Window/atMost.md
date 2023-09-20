
class Solution {

private int atMost(int[] nums, int k){

  
  

int res = 0;

int distinct = 0;

//map<element, frequency>

Map<Integer, Integer> map = new HashMap<>();

for(int i=0,j=0;j<nums.length;j++){

  

map.putIfAbsent(nums[j], 0);

//new element

if(map.get(nums[j])==0) distinct++;

map.put(nums[j], map.get(nums[j])+1);

  

while(distinct>k){

map.put(nums[i], map.get(nums[i])-1);

//element removed subarray

if(map.get(nums[i])==0) distinct--;

i++;

}

  

if(distinct<=k) res += j-i+1;

}

  

return res;

}

public int subarraysWithKDistinct(int[] nums, int k) {

  

return atMost(nums,k) - atMost(nums,k-1);

}

}