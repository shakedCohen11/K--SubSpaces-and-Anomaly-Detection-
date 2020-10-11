# K-SubSpaces and Anomaly Detection
The repository contains part of my project for the course:
Selected Topics in Images Processing, [Prof. Stanley Rotman](http://www.ee.bgu.ac.il/~srotman/)

cool image

The goal of the project is to implement the k-SubSpaces algorithm, use it as a pre-processing tool for anomaly detection (primarily the RX algorithm) in hyperspecteral images, 
and compare it to k-means algorithm as a pre-processing tool for anomaly detection.  

The diffrence between the 2 algorithms is in the use of high dimentinal data.

## Spoiler

We created new approaches for using the segmented image created by the algorithm for anomaly detection with the RX algorithm as the base:

We created 2 different approaches for applying the RX algorithm on the segmented data:  

 1. The direct cluster approach - applying RX algorithm on each cluster independently using the cluster mean and covariance.
    ![code](https://latex.codecogs.com/gif.latex?%5Cforall%20x%20%5Cin%20S%20%5Csubseteq%20X%20%2C%20%5Cquad%20r%28x%29%3D%28x-m_s%29%5ET%20%5CPhi_S%5E%7B-1%7D%20%28x-m_s%29)    
   Where X is the hyperspectral image, S is the cluster (associated with the subspace), 𝑚_𝑠 is the cluster mean, and 𝜙_𝑆^(−1) is the inverse covariance matrix of the cluster.

 2. The indirect cluster approach - applying RX algorithm on each cluster independently using the original mean of the image and the local clusters covariance.         
   ![code](https://latex.codecogs.com/gif.latex?%5Cforall%20x%20%5Cin%20S%20%5Csubseteq%20X%20%2C%20%5Cquad%20r%28x%29%3D%28x-m_x%29%5ET%20%5CPhi_S%5E%7B-1%7D%20%28x-m_x%29)   
   Where 𝑋 is the hyperspectral image, 𝑆 is the cluster (associated with the subspace), 𝑚_𝑥 is the neighbors mean, and 𝜙_𝑆^(−1) is the inverse covariance matrix of the cluster

We created 2 different approaches for normalizing the RX score acording to the segmented data:

1. Cluster Normalization: normalizing the RX scores according to each cluster separately, this allows for a bigger dynamic range.
   Let’s represent the cluster 𝑆 scores as 𝑅_𝑠 then the normalized scores are:                                                                                                    
    ![code](https://latex.codecogs.com/gif.latex?R_%7Bs-normalized%7D%3D%5Cfrac%7BR_s%20-%20min%28R_s%29%29%7D%7Bmax%28R_s%29-min%28R_s%29%7D)                                        and the scores of the whole image is:		                                                                                                                                      
    ![code](https://latex.codecogs.com/gif.latex?R_%7Bimage%7D%3D%5Ccup_s%20R_%7Bs-normalized%7D) 

2. Whole data Normalization: normalizing the RX scores according to the whole of the data, this allows for getting stronger anomalies only.
Let’s represent the cluster 𝑆 scores as 𝑅_𝑠 then the image scores are:                                                                                                           ![code](https://latex.codecogs.com/gif.latex?R_%7Bimage%7D%3D%5Ccup_s%20R_%7Bs%7D)                                                                                             and the normalized scores are:                                                          
![code](https://latex.codecogs.com/gif.latex?R_%7Bimage-normalized%7D%3D%5Cfrac%7BR_%7Bimage%7D%20-%20min%28R_%7Bimage%7D%29%29%7D%7Bmax%28R_%7Bimage%7D%29-min%28R_%7Bimage%7D%29%7D)



## Repo Usage
This project was mostly based on implementing the K-SubSpaces algorithm, running multiple experiments and performing exploratory data analysis. 
These are organized in the following folders:
- [docs](docs): Contains the full project report as well as a presentation (for quick read)
- [code](code): Contains the experiments (.m, .mlx), functions (.m) and scripts (.m) used in the project.

## Datasets Used
The data used for this project can be found here:
[RIT Target Detection Blind Test](http://dirsapps.cis.rit.edu/blindtest/)
 
Hyperspectral Toolbox for MATLAB (contains useful operators, transformations and algorithms):
[HyperToolbox](https://github.com/isaacgerg/matlabHyperspectralToolbox)


## License
[MIT Open Source](https://choosealicense.com/licenses/mit/)

Feel free to use this work as long as you refrence this repo.

