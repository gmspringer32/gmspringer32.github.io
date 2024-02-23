# Decision Trees

### Entropy

$$
-\sum_{i=1}^{|C|}p_ilog_2(p_i)
$$

This is the negative sum of the probability of an occurance times the log of the probabilty of the probebility. 


The Entropy of the total split on a node is 

$$
Entropy(Class) = \sum_{j=1}^{|A|} \frac{|S_j|}{|S|}Entropy(S_j)
$$

#### Example
