---
title: Clustering Methods
draft: false
socialImage: og-image.png
socialDescription:
date: 2025-01-01
tags:
  - methods
---
**The post provided by:** Miquel De Cáceres, Sebastian Schmidtlein, Susan Wiser
(taken from the old VCWG website: [link](https://sites.google.com/site/vegclassmethods/statistical-analyses/classification-methods?authuser=0))
## Hierarchical cluster models

In a hierarchical cluster model, the membership of the plot observation to a given lower level cluster conditions its membership to upper level clusters. Hierarchical models are build using two main strategies. **Agglomerative** techniques construct the classification from the bottom to the top. They begin with clustering of the most similar sites and aggregate these into larger clusters until there is a single cluster containing all sites. **Divisive** techniques construct the classification from the top to the bottom. They begin with all sites in a single cluster that is successively divided until individual sites are separated.

### Divisive hierarchical methods

**TWINSPAN**

Divisive hierarchical methods can be further divided between monotetic and polytetic approaches. The former create divisions on the basis of a single character, whereas the latter use all the time the whole set of characters. Classification trees are an example of monotetic divisive methods.

One can obtain a polytetic division by means of ordinations. For example, one can run principal components analysis or correspondence analysis and divide the set of plot observations depending on whether they have low or high values on the first ordination axis. Then, the same procedure can be repeated for each of the groups.

One of the most popular hierarchical divisive techniques in community ecology, Two-Way INdicator SPecies ANalysis (TWINSPAN, Hill 1974, 1979), uses this approach. The TWINSPAN algorithm starts with a an ordination of sites along the first axis of correspondence analysis (CA, Hill 1973). Sites are then divided into two clusters by splitting the first CA axis near its middle. Site classification is refined using a discriminant function that emphasizes species preference to one or the other half of the dichotomy. This process is repeated in the same way for the two clusters. A limitation of the original algorithm was that the number of clusters of the final classification cannot be set manually, but increases in powers of two (2 -> 4 -> 8 ->32 etc) except when a cluster is too small to be further splitted. TWINSPAN was recently modified by Rolecek et al (2007) to allow any number of terminal clusters. The proposed modification does not alter the logic of the TWINSPAN algorithm, but it may change the hierarchy of dividisions in the final classification. Thus, unsubstiantated division of homogeneous clusters are prevented, and classifications with any number of terminal clusters can be created.

Another suggested modification was made by Carleton et al. (1996), who replaced the role of CA by canonical correspondence analysis (CCA), which gave a COnstrained INdicator SPecies ANalysis (COINSPAN).

**Recursive partitioning**

One way to obtain a hierarchy of nested vegetation units is by recursive partitioning. In this strategy, the clusters obtained at one clustering level are subsequently divided to form clusters at the next level of the hierarchy. For example, ISOPAM (Schmidtlein et al. 2010) (see description below) can be used as a divisive hierarchical method or as a partitioning method.

### Agglomerative hierarchical methods

Agglomerative hierarchical methods are bottom-up approaches that generate clusters by sequentially merging pairs of clusters that are closest to each other. Depending on how "closeness" between clusters is defined several options are possible. All of them are referred to as the Sequential Agglomerative Hierarchical Non-overlapping (SAHN) model. The most used variants are:

- **Complete linkage clustering** (Maximum or Furthest-Neighbor Method): The dissimilarity between 2 groups is equal to the greatest dissimilarity between a member of cluster i and a member of cluster j. This method tends to produce very tight clusters of similar cases.
- **Single linkage clustering** (Minimum or Nearest-Neighbor Method): The dissimilarity between 2 clusters is the minimum dissimilarity between members of the two clusters. This method produces long chains which form loose, straggly clusters.
- **Ward's method**: Cluster membership is assigned by calculating the total sum of squared deviations from the mean of a cluster. The criterion for fusion is that it should produce the smallest possible increase in the error sum of squares.
- **Average linkage clustering**: The dissimilarity between clusters is calculated using average values. The average distance is calculated from the distance between each point in a cluster and all other points in another cluster. The two clusters with the lowest average distance are joined together to form the new cluster.
- **Centroid linkage clustering**:This variatnt uses the group centroid as the average. The centroid is defi.ned as the center of a cloud of points.

## Partitioning hard clustering

The purpose of partitioning methods is to provide a classification of objects into distinct clusters, where each object can only belong to a single cluster and every cluster must have at least one element. This kind of classification is often referred to as a **hard or crisp partition**.

The classificatory algorithm is usually **iterative**: an initial partition is improved step by step in the analysis until no further improvement can be achieved. Assume that the “goodness” of the partition is measured by function _J_, whose value is to be decreased as much as possible in order to achieve further optimization of the result. Function _J_ is usually referred to as the **objective function**. The general paritioning algorithm would be as follows (from Podani 2000):

1. Specify an initial partition into _k_ clusters and compute the value of _J_.
2. Change the partition so as to decrease the value of _J_ as much as possible, leaving _k_ unchanged (that is, empty or new clusters cannot appear as a result of this change).
3. If no reduction of _J_ is possible, the analysis stops with the actual partition as the final result. Otherwise we continue the iterations in step 2.

The different procedures vary in defining the goodness function _J_ and in the operations allowed in step 2 to modify the actual partition. A fundamental property of the above general algorithm is that the result may often be only a **local optimum**, i.e., not necessarily the best classification of the given objects into _k_ groups according to the _J_ criterion. This problem can be circumvented by performing the iterations from tens of different initial partitions and retaining the “best” result. Unfortunately, we will never be sure that we have reached the absolute (global) optimum; to obtain this all the possible partitions should be checked, which is an unaccomplishable task for large numbers of objects and clusters.

### K-means: partitioning around centroids

In K-means, the objective function to minimize is the **total error sum of squares** (TESS). In this sense, K-means is very similar to Ward's agglomerative clustering method. An important feature of K-means is the the fact that it uses **centroids** as cluster prototypes. The centroid of a cluster is the point whose coordinates are the **means**, calculated over all objects that belong to the cluster, on each variable of the attribute space.

Although there exist many variants, the commonest way that implementations of K-means use to minimize TESS is by subdividing step 2 of the general algorithm into two substeps:

- 2a. Compute cluster centroids and use them as new cluster prototypes.
- 2b. Assign each object to the nearest prototype.

K-means partitioning may be computed from either a table of raw data or a distance matrix, because the total error sum of squares is equal to the sum (over groups) of the mean squared within-group distances (see Legendre & Legendre 1998). This fact is rather ignored by many practitioners of K-means, due to the fact the implementation of K-means in most programs follows the raw data mode. The advantage of using K-means from a raw data table is that it is much more efficient when the number of objects to classify is large. On the other hand, the disadvantage is that the only distance function available is the Euclidean distance. When the Euclidean distance is not suitable for the data at hand, one has three options:

1. Transform the raw data matrix in order to emulate a distance function with better properties (Legendre & Gallagher 2001).
2. Computed a distance matrix using the desired distance function and run it through a metric or nonmetric scaling procedure to obtain a new table of coordinates, which can be entered to K-means.
3. Computed a distance matrix using the desired distance function and use a K-means implementation that works with distance matrices.

### K-medians: partitioning around medians

K-medians clustering (Jain & Dubes 1981) is a variation of k-means clustering where instead of calculating the **mean** for each cluster to determine its centroid, one instead calculates the **median**. This has the effect of minimizing error over all clusters with respect to the 1-norm distance metric (Manhattan distance), as opposed to the square of the 2-norm distance metric (the Euclidean distance, which K-means does). Computationally it is much more complex than K-means. It relates to the **k-median problem** which is the problem of finding k centers such that the clusters formed by them are the most compact. Formally, given a set of data points, the k centers are to be chosen so as to minimize the sum of the distances from each point to the nearest center.

### K-medoids: partitioning around medoids (PAM)

Partitioning around medoids (PAM, Kaufman & Rousseeuw 1990) creates spheroid clusters in the attribute space. PAM operates on a distance matrix and searches for a predefined number of **medoids**. The medoid of a cluster is the object, among those belonging to the cluster, that is central in the sense that minimizes dissimilarity to the other group members. Unlike means, medoids are always real observations. PAM is similar to the more widely used k-means algorithm but tends to be more robust. A modified version of PAM called CLARA (Clustering LARge Applications) to handle large data sets was also proposed by Kaufman & Rousseeuw (1990).

### ISOPAM: Combining isomap ordination and PAM

[ISOPAM](http://www.google.com/url?q=http%3A%2F%2Fcran.r-project.org%2Fweb%2Fpackages%2Fisopam%2Findex.html&sa=D&sntz=1&usg=AOvVaw39EH6oeyqoL3-lkkY6HquY) (Schmitdlein et al 2010) uses Isomap as underlying ordination method and the resulting space is divided into two or more classes using partitioning around medoids (PAM). The parameterization of the ordination as well as the number of axes and classes is iteratively changed and the best classification solution according to predefined criteria is selected. The default selection criterion is based on quantity and quality of indicator species, which are found by the algorithm or can be, at will, predefined. ISOPAM can be used as a divisive hierarchical method or as a partitioning method.

## Partitioning fuzzy clustering

Fuzzy set theory is an extension of classical set theory that was introduced by Zadeh (1965) as a way to model the vagueness or imprecision of human cognitive processes. Informally speaking, a fuzzy set is a set where the membership of its objects is expressed not in a binary (yes/no) way, but through a degree of membership bounded between 0 (i.e. the object does not belong to the set at all) and 1 (i.e. the object belongs completely to the set).

A fuzzy classification is represented by a matrix whose rows are the objects and the columns are clusters, and each value is the degree of membership of the object (row) into the fuzzy cluster (column).

### Fuzzy C-means

The simplest and most widely known fuzzy clustering method is Fuzzy C-means (FCM, Bezdek 1981). Conceptually, FCM is very similar to K-means. It can also be run from either raw data or distance matrices. The optimization function of FCM is the fuzzy analogue of TESS, and is sometimes called the **fuzzy sum of squares**. The steps are very similar to those of K-means, except by the fact that in step 2b a membership function has to be calculated to obtain the membership of each object to each cluster.

An important feature of FCM with respect to K-means is that it needs an additional parameter, called the **coefficient of fuzziness** (_m_). The smaller the _m_, the closer to a hard partition will be the result of FCM. If _m_ is set too high with noisy data, the resulting partition may be completely fuzzy (i.e. where memberships will be 1/_k_ for all objects and clusters) and therefore uninformative. Although some ecological applications of FCM can be found using m = 2.0 (e.g. Equihua 1990, Marsili-Libelli 1990), community data are often very noisy and in many cases the fuzziness coefficient has to be set to a very low value, i.e. between m = 1.1 and m = 1.25 (Podani 1990; Escudero & Pajarón 1994; Olano et al. 1998).

### Fuzzy C-medoids and Fuzzy C-medians

Just like FCM is a fuzzy relative of K-means, there exist a fuzzy relative of the k-medoids algorithm (Krishnapuram et al. 1999).

## Non-partitioning fuzzy clustering

### Noise clustering

The noise clustering method (Davé 1991) is an attempt to make the FCM method more robust to the effect of outliers. The rationale underlying NC is the following: if an object is an outlier, this means that it lies far from all cluster centroids and, therefore, it should have low membership values to all clusters. In order to achieve this, the NC algorithm considers an additional cluster, called **Noise cluster**. This class is represented by an imaginary ‘‘prototype’’ that lies at a constant distance, called the **noise distance**, from all the data points. Even if such a prototype does not really exist, the effect of including the Noise class is that it captures objects that lie farther than the noise distance from all the _k_ ‘‘true’’ centroids. Outlier objects have small membership values to the _k_ true clusters. The smaller the noise distance, the higher will be memberships to the Noise class. In contrast, large values of the noise distance make the NC algorithm equivalent to FCM. In NC, the partition restriction is fulfilled when considering all _k_ true clusters and the Noise class.

### Possibilistic C-means

Possibilistic C-means (Krishnapuram & Keller 1993) is another modification of FCM seeking increased cluster robustness. The partition restriction is eliminated in PCM, which produces independent fuzzy clusters, each cluster corresponding to a dense region in the attribute space. While the FCM and NC membership functions compare the distance from the object to the cluster of interest with the distances to the remaining centres (and to the noise class in the case of NC), in PCM the membership value for a given object to a cluster does not depend on the distances to the remaining cluster centres. Instead, the distance to the cluster of interest is **compared to a reference distance.** The reference distance is a parameter that must be provided for each cluster. All objects lying at a distance smaller than the reference distance will obtain a membership value higher than 0.5. Since cluster variance can be defined as the average squared distance to the centroid, the reference distance of a PCM cluster is in close relation to its variance. Good estimation of this parameter is crucial for the success of the method (De Cáceres et al. 2006). The high mobility resulting from the inadequate initialization of this parameter can lead to a miss of cluster structures when running PCM, even with the correct classification as initial starting configuration. A single PCM run can be regarded as _k_ independent runs of NC, each looking for a single true cluster, and where the noise distance of NC is equal to the square root of the corresponding reference distance of PCM (Davé & Krishnapuram 1997, De Cáceres et al. 2010).

## Other numerical approaches



### COCKTAIL



### REBLOCK



## Discussion topics

### Hierarchical vs. non-hierarchical

The hierarchical structure provides knowledge of the data at different levels, but at the expense of flexibility. According to Mucina (1997), the hierarchical cluster model can be justified only if we assume that the process generating our data has a hierarchical component (as it more or less generally occurs with phylogenetics). However, since the classification of vegetation has a conventional character (Mirkin 1989) one can still use the hierarchical model if it proves useful.

### Fuzzy vs. crisp clustering

Although vegetation scientists accept the vegetation continuum, there is often the need to put every plot observation into a known vegetation type (e.g. Kočí et al. 2003). Adopting a framework where plot records can be transitional may be regarded initially as impractical. However, it is desirable to exclude transitions from the set of plots used to define vegetation types, because this ensures a more distinct characterization of those types (e.g. number and identity of diagnostic species, distinct environmental and geographical range). Since many existing quantitative classification algorithms require that all plots in the data set be assigned to a type, the analyst has to make any decisions about exclusion/inclusion of plots having transitional composition before the analysis is begun. Fuzzy clustering provides a way to identify transitional plots, thus making the defined types more robust and cohesive in composition. Moreover, if a single answer is desired, transitional plot records may be a posteriori assigned to the closest type.

### Centroids, medoids or medians

## Bibliography

- Bezdek, J.C. (1981) _Pattern recognition with fuzzy objective functions_. Plenum Press, New York.
- Carleton, T. J., Stitt, R. H. & Nieppola, J. (1996) Constrained indicator species analysis (COINSPAN): an extension of TWINSPAN. Journal of Vegetation Science, 7, 125-130.Hill, M. O. (1973) Reciprocal averaging: An eigenvector method of ordination. _Journal of Ecology_, 61, 237-249.
- Dale, M. (1995) Evaluating classification strategies. _Journal of Vegetation Science_, **6**, 437–440.
- Dave, R.N. (1991) Characterization and detection of noise in clustering. _Pattern Recognition Letters_, **12**, 657-664.
- Davé, R.N. & Krishnapuram, R. (1997) Robust clustering methods: a unified view. _IEEE Transactions on Fuzzy Systems_, **5**, 270-293.
- De Cáceres, M., Oliva, F. & Font, X. (2006) On relational possibilistic clustering. _Pattern Recognition_, **39**, 2010-2024.
- De Cáceres, M., Font, X. & Oliva, F. (2010) The management of vegetation classifications with fuzzy clustering. _Journal of Vegetation Science_, **21**, 1138-1151.
- Equihua, M. (1990) Fuzzy clustering of ecological data. _The Journal of Ecology_, **78**, 519–534.
- Escudero, A. & Pajarón, S. (1994) Numerical syntaxonomy of the Asplenietalia petrarchae in the Iberian Peninsula. _Journal of Vegetation Science_, **5**, 205-214.
- Hill, M. O., Bunce, R. G. H. & Shaw, M. W. (1974) Indicator species analysis, a divisive polythetic method of classification, and its application to a survey of native pinewoods in Scotland. _Journal of Ecology_, 63, 597-613.
- Hill, M. O. (1979) TWINSPAN - a FORTRAN program for arranging multivariate data in an ordered two-way table by classification of the individuals and attributes. Cornell University, Ithaca, NY.
- Jain, A. K.& Dubes, R. C. (1981) _Algorithms for Clustering Data_. Prentice-Hall.
- Kaufman, L. & Rousseuw, P. J. (1990) _Finding Groups in Data: An Introduction to Cluster Analysis_. New York: Willey & Sons Inc.
- Krishnapuram, R. & Keller, J.M. (1993) A possibilistic approach to clustering. _IEEE Transactions on Fuzzy Systems_, **1**, 98-110.
- Krishnapuram, R., Joshi, A. & Yi, L. (1999) A Fuzzy relative of the k-medoids algorithm with application to web document and snippet clustering. _IEEE International Fuzzy Systems_. pp. 1281-1286.
- Kočí, M., Chytrý, M. & Tichý, L. (2003) Formalized reproduction of an expert-based phytosociological classification: A case study of subalpine tall-forb vegetation. Journal of Vegetation Science, 14, 601-610.
- Legendre, P. & Gallagher, E. (2001) Ecologically meaningful transformations for ordination of species data. _Oecologia_, **129**, 271-280.
- Marsili-Libelli, S. (1990) Fuzzy clustering of ecological data. _Coenoses_, **4**, 95-106.
- Legendre, P. & Legendre, L. (1998) _Numerical Ecology_. Elsevier.
- Mirkin, B. M. (1989) Plant taxonomy and syntaxonomy: a comparative analysis. _Vegetatio_, 82, 35-40.
- Mucina, L. (1997) Classification of vegetation: Past, present and future. _Journal of Vegetation Science_, 8, 751-760.
- Olano, J.M., Loidi, J.J., GonzáLez, A. & Escudero, A. (1998) Relating variation in the understorey of beech forests to Ecological factors. _Folia Geobotanica_, **33**, 77-86.
- Podani, J. (1990) Comparison of fuzzy classifications. _Coenoses_, **5**, 17-21.
- Podani, J. (2000) _Introduction to the exploration of multivariate biological data_. Backhuys, Leiden.
- Rolecek, J., Tichy, L., Zeleny, D. & Chytry, M. (2009) Modified TWINSPAN classification in which the hierarchy respects cluster heterogeneity. _Journal of Vegetation Science_, 20, 596-602.
- Schmidtlein, S., Tichý, L., Feilhauer, H. & Faude, U. (2010) A brute-force approach to vegetation classification. _Journal of Vegetation Science_, 21, 1162-1171.
- Zadeh, L.A. (1965) Fuzzy sets. _Information and Control_, **8**, 338-353.


---
[All Blog Posts](VCWG%20Blog%20Posts.md)
[Home Page](index.md)

