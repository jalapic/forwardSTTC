### R Code for implementing a forward-only version of Cutts & Eglen's STTC algorithm

An adaptation of the algorithm described here by Cutts & Eglen - http://www.ncbi.nlm.nih.gov/pubmed/25339742


Also available in code here: https://github.com/sje30/sjemea

```
### Demonstration of Forward STTC


# load one of the .dll files
dyn.load("run_sttc2_64.dll")

# Generate some sample data
set.seed(102)
v1 <- cumsum(sample(rexp(10),100,T))
v2 <- cumsum(sample(rexp(10),100,T))
v1
v2

#parameters: start time, end time, DT
START = 0 
END = 90
DT = 0.5

# run function to calculate forward STTC
corr = .C("run_sttc2", as.integer(length(v1)), as.integer(length(v2)), 
          as.double(DT), rec.time = range(c(START, END))
          , coeff = double(1), as.double(v1), 
          as.double(v2))

corr$coeff  #0.08872965

```


Note - care has to be taken to ensure that the choice of DT is not too large such that too high a proportion of the sample period is tiled with the windows of DT.  Data should not be uniform but occur in a bursting fashion.
