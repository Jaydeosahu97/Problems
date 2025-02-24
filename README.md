# Problems
LRU Cache

class LRUCache {

    private List<Node> nodes;
    private Map<Integer, Node> nodeMap;
    private int capacity;

    private class Node {
        private Integer key;
        private Integer value;

        public Node(Integer key, Integer value) {
            this.key = key;
            this.value = value;
        }

        public Integer getKey() {
            return key;
        }

        public void setKey(Integer key) {
            this.key = key;
        }

        public Integer getValue() {
            return value;
        }

        public void setValue(Integer value) {
            this.value = value;
        }

        @Override
        public boolean equals(Object o) {
            if (o == null || getClass() != o.getClass())
                return false;
            Node node = (Node) o;
            return Objects.equals(key, node.key) && Objects.equals(value, node.value);
        }

        @Override
        public int hashCode() {
            return Objects.hash(key, value);
        }
    }

    public LRUCache(int capacity) {
        this.nodes = new LinkedList<>();
        this.nodeMap = new HashMap<>();
        this.capacity = capacity;

    }

    public int get(int key) {
        if (this.nodeMap == null || this.nodeMap.get(key) == null)
            return -1;
        Node result = this.nodeMap.get(key);
        this.nodes.remove(result);
        this.nodes.addFirst(result);
        return result.getValue();
    }

    public void put(int key, int value) {
        if (!this.nodeMap.containsKey(key) && this.nodeMap.size() == this.capacity) {
            Node last = this.nodes.removeLast();
            this.nodeMap.remove(last.getKey());
            Node newNode = new Node(key, value);
            this.nodeMap.put(key, newNode);
            this.nodes.addFirst(newNode);
        } else if (this.nodeMap.containsKey(key)) {
            Node existing = this.nodeMap.get(key);
            this.nodes.remove(existing);
            existing.setValue(value);
            this.nodes.addFirst(existing);
            this.nodeMap.put(key, existing);
        } else {
            Node newNode = new Node(key, value);
            this.nodeMap.put(key, newNode);
            this.nodes.addFirst(newNode);
        }

    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */


Longest Increasing Subsequence

class Solution {
    public int lengthOfLIS(int[] nums) {
        int n=nums.length;
        int dp[]=new int[n];
        Arrays.fill(dp,1);
        for(int i=1;i<n;i++)
        {
            for(int j=0;j<i;j++)
            {
                if(nums[i]>nums[j] && dp[i]<=dp[j])
                {
                    dp[i]=dp[j]+1;
                }
            }
        }
        int max=0;
        for(int i=0;i<n;i++)
        {
            max=Math.max(max,dp[i]);
        }
        return max;
    }
}
