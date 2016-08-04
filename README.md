# eXtreme Gradient Boosting for Alzheimer’s Disease CSF Biomarker Discovery
Justin Taylor 

We use predictors from a Washington University study to predict Alzheimer's disease status with a gradient-boosted tree model. The data can be found in the AppliedPredictiveModeling package. The caret and xgboost packages were used to train a model and make predictions.  


To view the compiled report, clone this repository. 

```
git clone https://github.com/taylo5jm/xgboost-alzheimers-demo
```

View `xgboost-alzheimers-demo.html` in a browser, or use Jekyll and navigate to the listening port on localhost.  

```
Rscript -e "servr::jekyll()"
```

# References

[1] Craig-Schapiro, R., Kuhn, M., Xiong, C., Pickering, E. H., Liu, J., Misko, T. P., … Holtzman, D. M. (2011). Multiplexed Immunoassay Panel Identifies Novel CSF Biomarkers for Alzheimer’s Disease Diagnosis and Prognosis. PLoS ONE, 6(4), e18850. http://doi.org/10.1371/journal.pone.0018850  

[2] Tianqi Chen, Tong He and Michael Benesty (2016). xgboost: Extreme Gradient Boosting. R
  package version 0.4-3. https://CRAN.R-project.org/package=xgboost
  
[3] Max Kuhn. Contributions from Jed Wing, Steve Weston, Andre Williams, Chris Keefer, Allan
  Engelhardt, Tony Cooper, Zachary Mayer, Brenton Kenkel, the R Core Team, Michael Benesty,
  Reynald Lescarbeau, Andrew Ziem, Luca Scrucca, Yuan Tang and Can Candan. (2016). caret:
  Classification and Regression Training. R package version 6.0-68.
  https://CRAN.R-project.org/package=caret
  