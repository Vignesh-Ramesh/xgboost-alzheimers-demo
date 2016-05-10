---
title: "eXtreme Gradient Boosting for Alzheimer's Disease CSF Biomarker Discovery"
author: "Justin Taylor"
date: "May 10, 2016"
output: 
  html_document:
    code_folding: hide
    toc: true
    toc_float: true
    theme: "simplex"
    highlight: "textmate"
    
---

Load the `AlzheimerDisease` data set from the AppliedPredictiveModeling package.  



# Data {.tabset}  


```r
data(AlzheimerDisease)
```

## Inspection  

Dimensions: 333, 130  

Number of rows = Number of labels: TRUE   

Variable names:  

```r
colnames(predictors)
```

```
##   [1] "ACE_CD143_Angiotensin_Converti"   "ACTH_Adrenocorticotropic_Hormon" 
##   [3] "AXL"                              "Adiponectin"                     
##   [5] "Alpha_1_Antichymotrypsin"         "Alpha_1_Antitrypsin"             
##   [7] "Alpha_1_Microglobulin"            "Alpha_2_Macroglobulin"           
##   [9] "Angiopoietin_2_ANG_2"             "Angiotensinogen"                 
##  [11] "Apolipoprotein_A_IV"              "Apolipoprotein_A1"               
##  [13] "Apolipoprotein_A2"                "Apolipoprotein_B"                
##  [15] "Apolipoprotein_CI"                "Apolipoprotein_CIII"             
##  [17] "Apolipoprotein_D"                 "Apolipoprotein_E"                
##  [19] "Apolipoprotein_H"                 "B_Lymphocyte_Chemoattractant_BL" 
##  [21] "BMP_6"                            "Beta_2_Microglobulin"            
##  [23] "Betacellulin"                     "C_Reactive_Protein"              
##  [25] "CD40"                             "CD5L"                            
##  [27] "Calbindin"                        "Calcitonin"                      
##  [29] "CgA"                              "Clusterin_Apo_J"                 
##  [31] "Complement_3"                     "Complement_Factor_H"             
##  [33] "Connective_Tissue_Growth_Factor"  "Cortisol"                        
##  [35] "Creatine_Kinase_MB"               "Cystatin_C"                      
##  [37] "EGF_R"                            "EN_RAGE"                         
##  [39] "ENA_78"                           "Eotaxin_3"                       
##  [41] "FAS"                              "FSH_Follicle_Stimulation_Hormon" 
##  [43] "Fas_Ligand"                       "Fatty_Acid_Binding_Protein"      
##  [45] "Ferritin"                         "Fetuin_A"                        
##  [47] "Fibrinogen"                       "GRO_alpha"                       
##  [49] "Gamma_Interferon_induced_Monokin" "Glutathione_S_Transferase_alpha" 
##  [51] "HB_EGF"                           "HCC_4"                           
##  [53] "Hepatocyte_Growth_Factor_HGF"     "I_309"                           
##  [55] "ICAM_1"                           "IGF_BP_2"                        
##  [57] "IL_11"                            "IL_13"                           
##  [59] "IL_16"                            "IL_17E"                          
##  [61] "IL_1alpha"                        "IL_3"                            
##  [63] "IL_4"                             "IL_5"                            
##  [65] "IL_6"                             "IL_6_Receptor"                   
##  [67] "IL_7"                             "IL_8"                            
##  [69] "IP_10_Inducible_Protein_10"       "IgA"                             
##  [71] "Insulin"                          "Kidney_Injury_Molecule_1_KIM_1"  
##  [73] "LOX_1"                            "Leptin"                          
##  [75] "Lipoprotein_a"                    "MCP_1"                           
##  [77] "MCP_2"                            "MIF"                             
##  [79] "MIP_1alpha"                       "MIP_1beta"                       
##  [81] "MMP_2"                            "MMP_3"                           
##  [83] "MMP10"                            "MMP7"                            
##  [85] "Myoglobin"                        "NT_proBNP"                       
##  [87] "NrCAM"                            "Osteopontin"                     
##  [89] "PAI_1"                            "PAPP_A"                          
##  [91] "PLGF"                             "PYY"                             
##  [93] "Pancreatic_polypeptide"           "Prolactin"                       
##  [95] "Prostatic_Acid_Phosphatase"       "Protein_S"                       
##  [97] "Pulmonary_and_Activation_Regulat" "RANTES"                          
##  [99] "Resistin"                         "S100b"                           
## [101] "SGOT"                             "SHBG"                            
## [103] "SOD"                              "Serum_Amyloid_P"                 
## [105] "Sortilin"                         "Stem_Cell_Factor"                
## [107] "TGF_alpha"                        "TIMP_1"                          
## [109] "TNF_RII"                          "TRAIL_R3"                        
## [111] "TTR_prealbumin"                   "Tamm_Horsfall_Protein_THP"       
## [113] "Thrombomodulin"                   "Thrombopoietin"                  
## [115] "Thymus_Expressed_Chemokine_TECK"  "Thyroid_Stimulating_Hormone"     
## [117] "Thyroxine_Binding_Globulin"       "Tissue_Factor"                   
## [119] "Transferrin"                      "Trefoil_Factor_3_TFF3"           
## [121] "VCAM_1"                           "VEGF"                            
## [123] "Vitronectin"                      "von_Willebrand_Factor"           
## [125] "age"                              "tau"                             
## [127] "p_tau"                            "Ab_42"                           
## [129] "male"                             "Genotype"
```

Variable types:  


```r
sapply(predictors, class) %>% table
```

```
## .
##  factor integer numeric 
##       1       2     127
```

Head of selected variables:  


```r
head(predictors[,1:5])
```

```
##   ACE_CD143_Angiotensin_Converti ACTH_Adrenocorticotropic_Hormon
## 1                      2.0031003                       -1.386294
## 2                      1.5618560                       -1.386294
## 3                      1.5206598                       -1.714798
## 4                      1.6808260                       -1.609438
## 5                      2.4009308                       -0.967584
## 6                      0.4311565                       -1.272966
##          AXL Adiponectin Alpha_1_Antichymotrypsin
## 1  1.0983867   -5.360193                 1.740466
## 2  0.6832816   -5.020686                 1.458615
## 3 -0.1452763   -5.809143                 1.193922
## 4  0.6832816   -5.115996                 1.280934
## 5  0.1908902   -4.779524                 2.128232
## 6 -0.2223611   -5.221356                 1.308333
```


```r
ad_matrix <- as.matrix(sapply(predictors, as.numeric))
```

The `label` parameter for `xgboost` should be $0$ or $1$ for binary classification.  


```r
diagnosis <- parallel::mclapply(diagnosis, function(x) (
  if (x == "Control") (0) else 1
)) %>% unlist; head(diagnosis)
```

```
## [1] 0 0 0 0 0 1
```

## Preview  


```r
DT::datatable(apply(ad_matrix, 2, round, 3), extensions = c('Buttons', 'Responsive'),
              options = list(dom = 'Bfrtip', buttons = c('copy', 'csv', 'excel', 'pdf', 'print')))
```

```
## Error in html_screenshot(x): Please install the webshot package (if not on CRAN, try devtools::install_github("wch/webshot"))
```

## Splitting
Simple splitting with 60/40 train/test spread.  


```r
set.seed(1983)
train_index <- createDataPartition(diagnosis, p = .6, list = FALSE, times = 1)
```

----------------------------------------------------------------------------  


# Train Model  


```r
model_params <- list(objective = "binary:logistic", eta = 0.01, max.depth = 3, eval_metric = "auc")
```


```r
model <- xgboost::xgboost(data = ad_matrix[train_index,], label = diagnosis[train_index], 
                          max.depth = 6, eta = 1, nthread = 2, nround = 8, 
                          objective = "binary:logistic")
```

```
## [0]	train-error:0.070000
## [1]	train-error:0.015000
## [2]	train-error:0.000000
## [3]	train-error:0.000000
## [4]	train-error:0.000000
## [5]	train-error:0.000000
## [6]	train-error:0.000000
## [7]	train-error:0.000000
```

```r
#model_cv <- xgb.cv(params = xgb_params, data = ad_matrix, nrounds = 100, nfold = 5, label = diagnosis)
# plot(model_cv$train.auc.mean)
```

----------------------------------------------------------------------------  


# Feature Importance {.tabset}

## Table  


```r
importance <- xgb.importance(colnames(predictors), model = model); 
DT::datatable(importance)
```

```
## Error in html_screenshot(x): Please install the webshot package (if not on CRAN, try devtools::install_github("wch/webshot"))
```

## Plot  


```r
#install.packages('Ckmeans.1d.dp')
library(Ckmeans.1d.dp)
xgb.plot.importance(importance)
```

![plot of chunk plotFeatureImportance](/figure/./xgboost-alzheimers-demo/plotFeatureImportance-1.png)

----------------------------------------------------------------------------  


# Testing Model {.tabset}

## Predictions


```r
predictions <- predict(model, ad_matrix[-train_index,])
predictions <- as.numeric(predictions > 0.5)
table(predictions)
```

```
## predictions
##   0   1 
## 107  26
```

```r
table(diagnosis[-train_index])
```

```
## 
##   0   1 
## 101  32
```

## Confusion Matrix  


```r
confusionMatrix(predictions, diagnosis[-train_index])
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction  0  1
##          0 96 11
##          1  5 21
##                                          
##                Accuracy : 0.8797         
##                  95% CI : (0.812, 0.9296)
##     No Information Rate : 0.7594         
##     P-Value [Acc > NIR] : 0.0003953      
##                                          
##                   Kappa : 0.6483         
##  Mcnemar's Test P-Value : 0.2112995      
##                                          
##             Sensitivity : 0.9505         
##             Specificity : 0.6562         
##          Pos Pred Value : 0.8972         
##          Neg Pred Value : 0.8077         
##              Prevalence : 0.7594         
##          Detection Rate : 0.7218         
##    Detection Prevalence : 0.8045         
##       Balanced Accuracy : 0.8034         
##                                          
##        'Positive' Class : 0              
## 
```


```r
error <- mean(predictions != diagnosis[-train_index])
```

Test Error: 0.1203008

---------------------------------------------------------------------------- 

# References

Craig-Schapiro, R., Kuhn, M., Xiong, C., Pickering, E. H., Liu, J., Misko, T. P., … Holtzman, D. M. (2011). Multiplexed Immunoassay Panel Identifies Novel CSF Biomarkers for Alzheimer’s Disease Diagnosis and Prognosis. PLoS ONE, 6(4), e18850. http://doi.org/10.1371/journal.pone.0018850  

Tianqi Chen, Tong He and Michael Benesty (2016). xgboost: Extreme Gradient Boosting. R
  package version 0.4-3. https://CRAN.R-project.org/package=xgboost
  
Max Kuhn. Contributions from Jed Wing, Steve Weston, Andre Williams, Chris Keefer, Allan
  Engelhardt, Tony Cooper, Zachary Mayer, Brenton Kenkel, the R Core Team, Michael Benesty,
  Reynald Lescarbeau, Andrew Ziem, Luca Scrucca, Yuan Tang and Can Candan. (2016). caret:
  Classification and Regression Training. R package version 6.0-68.
  https://CRAN.R-project.org/package=caret
  
Max Kuhn and Kjell Johnson (2014). AppliedPredictiveModeling: Functions and Data Sets for
  'Applied Predictive Modeling'. R package version 1.1-6.
  https://CRAN.R-project.org/package=AppliedPredictiveModeling
  

---------------------------------------------------------------------------- 



# Session Info


```r
sessionInfo()
```

```
## R version 3.2.3 (2015-12-10)
## Platform: x86_64-redhat-linux-gnu (64-bit)
## Running under: Fedora 23 (Twenty Three)
## 
## locale:
##  [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
##  [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
##  [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
##  [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                 
##  [9] LC_ADDRESS=C               LC_TELEPHONE=C            
## [11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  base     
## 
## other attached packages:
## [1] Ckmeans.1d.dp_3.4.0             caret_6.0-68                   
## [3] ggplot2_2.1.0                   lattice_0.20-33                
## [5] dplyr_0.4.3                     magrittr_1.5                   
## [7] DT_0.1.56                       xgboost_0.4-3                  
## [9] AppliedPredictiveModeling_1.1-6
## 
## loaded via a namespace (and not attached):
##  [1] Rcpp_0.12.4        nloptr_1.0.4       formatR_1.4       
##  [4] plyr_1.8.3         class_7.3-14       methods_3.2.3     
##  [7] iterators_1.0.8    tools_3.2.3        lme4_1.1-12       
## [10] rpart_4.1-10       digest_0.6.9       evaluate_0.9      
## [13] gtable_0.2.0       nlme_3.1-128       mgcv_1.8-9        
## [16] Matrix_1.2-3       foreach_1.4.3      DBI_0.4-1         
## [19] parallel_3.2.3     SparseM_1.7        e1071_1.6-7       
## [22] stringr_1.0.0      cluster_2.0.3      knitr_1.13        
## [25] MatrixModels_0.4-1 htmlwidgets_0.6    stats4_3.2.3      
## [28] grid_3.2.3         nnet_7.3-11        data.table_1.9.6  
## [31] R6_2.1.2           minqa_1.2.4        reshape2_1.4.1    
## [34] car_2.1-2          splines_3.2.3      scales_0.4.0      
## [37] codetools_0.2-14   htmltools_0.3.5    MASS_7.3-45       
## [40] pbkrtest_0.4-6     assertthat_0.1     colorspace_1.2-6  
## [43] labeling_0.3       quantreg_5.21      stringi_1.0-1     
## [46] munsell_0.4.3      chron_2.3-47       CORElearn_1.47.1
```


