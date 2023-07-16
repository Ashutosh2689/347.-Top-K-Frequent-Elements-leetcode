class Solution {
    public int[] topKFrequent(int[] nums, int k) {
    //First we will check for the base case
        if(nums.length == k){
            return nums;
        }
        // using hashmap for frequency count
        HashMap<Integer,Integer> mp = new HashMap<>();
        // updating the frequency
        for(int ch : nums){
            mp.put(ch,mp.getOrDefault(ch,0)+1);
        }
        // resultant arrayof size k
        int[] res = new int[k];
        // now we will use the concept of bucket sort
        List<Integer>[] freq= new List[nums.length+1];
        Arrays.fill(freq,null);
       // adding the element at index equal to its frequency 
        for(Integer x:mp.keySet()){
            int z = mp.get(x);
            if(freq[z] == null){
                freq[z] = new ArrayList<>();
            }
           freq[z].add(x);
        }
        // now we will just add the last k elements in result array 
        // from bucket(freq) array
         int v =0;
        for(int i = freq.length-1;i>=0;i--){
            if(freq[i]!= null && v<k){
                 for(int p: freq[i]){
                    res[v] = p;
                    v++;
                }
            }
        }
        // finally we just return the result
        return res;
    }
}
