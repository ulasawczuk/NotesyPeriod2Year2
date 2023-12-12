Expand shallowest unexpanded node

**Implementation**
*frontier* is a FIFO queue, i.e new successors go at end

![[Screenshot 2023-11-02 at 8.19.31 PM.png]]

**Complete:** yes if b is finite
**Optimal:** yes if identical step costs
**Time:** $O(b^{d+1})$
**Space:** $O(b^{d+1})$
