```python
# Solution 1 (Using Python's MinHeap as MaxHeap) | O(nlogk) time, O(k) space
class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        # Initialize a min heap that'll serve as a max heap by pushing negative values
        maxHeap = []

        # For each point, calculate its distance from the origin and push to the maxHeap
        for (x, y) in points:
            # Multiply by -1 so the bigger the distance, the smaller its value
            dist = -((x * x) + (y * y))

            # If the heap is full, push the distance and pop the farthest point. 
            if len(maxHeap) == k:
                heapq.heappushpop(maxHeap, (dist, x, y))
            # Else, just push the point with its distance
            else:
                heapq.heappush(maxHeap, (dist, x, y))
            
        return [(x, y) for (dist, x, y) in maxHeap]
```