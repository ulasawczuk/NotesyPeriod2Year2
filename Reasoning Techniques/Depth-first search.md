Expand deepest unexpanded node

**Implementation**
*frontier* = LIFO queue, i.e put successors at front

![[Screenshot 2023-11-02 at 8.31.58 PM.png]]

**Complete:** no, fails in infinite-depth spaces, spaces with loops
**Optimal:** no
**Time:** $O(b^{m})$
**Space:** $O(bm)$