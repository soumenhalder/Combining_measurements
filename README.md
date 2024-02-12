# Introduction
Combining measurements is an essential tool for experimental physicist. Things get harder when the measurements are correlated. The proper way of combining measuremets are described in this repository.

# References
* Statistical Methods for Data Analysis in Particle Physics (Luca Lista) - Chapter 6
* Lyons, L., Gibaut, D., Clifford, P.: How to combine correlated estimates of a single physical quantity. Nucl. Inst. Methods A270, 110–117 (1988)
* A. Valassi, Combining correlated measurements of several different physical quantities. Nucl. Instr. Meth. A 500, 391 (2003)
   * This paper gives the general picture. This repository basically reproduced the results of this paper (a jupyter notebook and its pdf conversion).  I have attched this paper here.


# The inputs

Suppose we have,
* $n$ experimental results, denoted as $y_{i}$ = {$y_{1}$, $y_{2}$, $y_{3}$ ...  $y_{n}$}
* Covariance matrix of the measurements $M_{ij} =$ cov($y_{i}$,$y_{j}$) is a $n\times n$ matrix
* $N$ observables, $X_{\alpha}$ = {$X_{1}$,$X_{2}$, $X_{3}$ ... $X_{N}$}

So it's obvious $n = \sum^{N}_{\alpha=1} n_{\alpha} \geq N$

* The link between measurement $y_{i}$ and the observables $X_{\alpha}$ is denoted by a $n \times N$ matrix,

$ 
  U_{i \alpha} = 
\begin{cases}
    1, & \text{if } y_{i} \text{ is a measurement of} X_{\alpha}\\
    0, & \text{if } y_{i} \text{ is a not measurement of} X_{\alpha}
\end{cases}
 $
 
# The desired outputs

* **Observable Estimation:** $\hat{x}_{\alpha}  = \lambda_{\alpha i} y_{i}$ as estimation of the observable $X_{\alpha}$
* **Covariance matrix of measured observables:**  as cov($\hat{x}_{\alpha}$,$\hat{x}_{\beta}$) = $\lambda_{\alpha i} M_{ij} \lambda_{\beta j} $ = $(\lambda M \lambda^{T})_{\alpha \beta}$ 

------------ -----------
* The ref. says $\lambda= (U^{T} M^{-1} U)^{-1} (U^{T} M^{-1})$ , or in index notation $\lambda_{\alpha i} =           \sum^{N}_{\beta = 1} (U^{T} M^{-1} U)_{\alpha \beta}^{-1} (U^{T} M^{-1})_{\beta i}$.

* Puting that in covariance matrix expression we get, 
  cov($\hat{x}_{\alpha}$,$\hat{x}_{\beta}$)= $(U^{T} M^{-1} U)_{\alpha \beta}^{-1}$

-------------------------

* **Decomposition of covariance matrix to statistical and systematics:** Suppose the covariance of measurements can be written as sum of statistical and systematic uncertainty like $M_{ij} = M^{\text{stat}}_{ij} + M^{\text{sys}}_{ij}$. The covariance matrix of observables can also be decomposed as, 


$$\text{ cov}(\hat{x}_{\alpha},\hat{x}_{\beta}) = (\lambda M^{\text{stat} }   \lambda^{T})_{\alpha \beta} +  (\lambda M^{\text{sys} }   \lambda^{T})_{\alpha \beta}$$

# How to use the code
The code is just a python fucntion. We have to put the inouts in proper format. 
    
* Measurements in python `list`  
* The link between measurement and observables is U, to be given as `np.array`
* Put total covariance matrix as `np.array`
* Next two input is optional. If you want to decompose statistical ans systematic uncertainty then put last two input as `np.array` in the order of Statistical and Systematics component of Covariance matrix 
 
