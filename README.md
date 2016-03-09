### Code for implementing the forward-only version of Cutts & Eglen's STTC algorithm


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
END = 100
DT = 2

# run function to calculate forward STTC
corr = .C("run_sttc2", as.integer(length(v1)), as.integer(length(v2)), 
          as.double(DT), rec.time = range(c(START, END))
          , coeff = double(1), as.double(v1), 
          as.double(v2))

corr$coeff  # 0.4433919
```
