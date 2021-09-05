# Clustering_Documents
###### Project Goal:
**Clustering documents with respect to their wordId. Here we are using Jaccard distance to check the similarity between two documents.
###### Here we have used the following libraries.
1. Pandas
2. Numpy
3. Matplotlib.pyplot
4. Seaborn
5. %matplotlib.inline.


Then we have created a dictionary "D", where keys are docID and values are list of wordID present in that document.

Now we form another dictionary "dic", which contains docID as keys, and it takes a values as a list of length = number of elements in vocab + 1, (where the zero-th place will be a garbage value and we will not consider it).
If a docID contains a certain wordID, then the wordID-th place in the list will be 1, the the other values will be zero.
Loosely, we are making a list, where if a Document contains a certain word then the index of the word in the list will contain 1 as value, and if the word is not present in the document then the corresponding index will contain 0 in the list.

Then we are defining Jaccard distance function in "jaccard_distance", which will take two list as input and will return their jaccard distance.

Then we compute a nested dictionary, namely "jaccard_matrix". Where each document will form a key, and corresponding to each key we have another dictionary as value. In this dictionary the keys will be each document and its value will be the corresponding jaccard distance. Here we are storing the jaccard distance between each document pairs. Basically we are forming the jaccard distance matrix in the form of dictionary to save space.

Now we will define "cluster_func1", which will take the centroids in the form of list and then form the corresponding clusters. It will give a dictionary as an output, where the keys will be the centroids and the list of elements of the corresponding cluster as the value.

Now we will initialize centroids. Usually in k-means we initialize centroids randomly, but here we will follow a heuristic way. At first we will take the sum of the values of the jaccard matrix corresponding to each docID. Then we will take the highest k- values. And then choose the corresponding keys as initial centroids. Now we are following this way so that the centroids are fairly far from each other. 

Then we will form initial clusters using the previous cluster function "cluster_func1" on this centroids.

Now we will update our centroids and then form the clusters corresponding to them iteratively. 

In each loop, from every cluster, we are updating the centroid by setting up a threshold. At first, for cluster we are taking the element of the cluster and corresponding to those elements we are taking the previous "dic" dictionary and we are adding up the values for those elements. Then we are dividing each element in that list with the number of elements in that specific cluster. 
Now the values of this list will lie between 0 to 1. Then we will set a threshold and accordingly replace the values less than the threshold by 0 and greater than the threshold by 1. This can be said as a dummy centroid. Then we choose the nearby(by jaccard distance) document of this dummy centroid and take it as the new centroid. continuing this process, we will get our all the k centroids, and then again we calculate the new clusters and again evaluate the new centroids iteratively. 

Now we will calculate the inertia of the clusters corresponding to each k and finally plot it on a elbow graph and from that decide upon the most optimized k.

**output link** : https://drive.google.com/drive/folders/1G2BtwC2RhaXqItABfzX1VPjsL4UDuSmr?usp=sharing
