## Molecular Geometry Recognition with PCA/t-SNE and K-Means Clustering
During the unbiased global minimum search, thousands of initial structures are generated using various algorithms. These initial structures are first optimized using a cheap method to reduce CPU cost. The representative low-lying structures from the initial optimizations are further optimized using an expensive method to achieve higher accuracy. Such low-lying structures are manually picked based on their energetics and structural similarities. While there could be many similar or duplicated structures, it is really time-consuming to manually go through thousands of files to visualize molecular structures, extract energetics, and decide candidates for further optimizations.

In this notebook, I parsed structural and energy data from 5000 Gaussian output files (~4.7 GB) and employed K-means clustering to autoselect representative structures for further optimizations. For each structure, I calculated distances from each atom to four reference points: the molecular centroid (ctd), the closest atom to ctd (cst), the farthest atom to ctd (fct), and the farthest atom to fct (ftf). The first three moments of these four atomic distance sets were calculated to encode molecular shape. Since there are thirteen features including twelve moments and energy, Principal Component Analysis (PCA) and t-distributed stochastic neighborhood embedding (t-SNE) were applied for dimensionality reduction and data visualization. For the current dataset, t-SNE has a much better performance than PCA. The dimension-reduced dataset was partitioned into k clusters using k-means clustering. In the end, representative structures were obtained by selecting structures that are closest to each cluster center from K-means clustering.

## Outline

1. **Parse coordinates and energies from Gaussian output files** <br>

2. **Calculate distances to four reference points (ctd, tst, fct, ftf)** <br>

3. **Obtain first three moments of the distance sets to four reference points to encode molecular shape** <br>

4. **Create a dataframe with moments and energy data** <br>
    
5. **Data exploration and visualization** <br> 

6. **Dimensionality reduction and data visualization using PCA/t-SNE** <br> 
    6a. Function to plot 2D figure <br>
    6b. Use PCA to reduce the dataset down to two dimensions to plot the result <br>
    6c. Use t-SNE to reduce the dataset down to two dimensions to plot the result <br>

7. **K-means clustering and visualization** <br>
    7a. Function to plot Inertia diagram <br>
    7b. Function to plot silhouette score <br>
    7c. Function to plot Voronoi diagram <br>
    7d. K-Means clustering on data reduced via PCA <br>
    7e. K-Means clustering on data reduced via t-SNE <br>

8. **Export coordinates of molecules that are closest to cluster centroids** <br>
