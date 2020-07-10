# semTools Measurement Invariance
This line of code is an example to get the deprecated semTools Measurement Invariance output back.

In the good old days semTools used to have this simple function for Measurement Invariance:
```
semTools::measurementInvariance(
  model = your_model, 
  data = your_data, 
  group = "your_group"
)
```

Since the old approach was deprecated to add flexibility you now have to do the following to produce the same result:
```
test.seq <- c("loadings","intercepts","means","residuals")

meq.list <- list()

for (i in 0:length(test.seq)) {
  if (i == 0L) {
    meq.label <- "configural"
    group.equal <- ""
  } else {
    meq.label <- test.seq[i]
    group.equal <- test.seq[1:i]
  }
  
  meq.list[[meq.label]] <- 
    semTools::measEq.syntax(
      configural.model = your_model,
      data = your_data,
      ID.fac = "auto.fix.first",
      group = "your_group",
      group.equal = group.equal,
      return.fit = TRUE
  )
}

semTools::compareFit(meq.list)
```

The new approach probably looks more complicated to the most of us. But if you simply copy and paste the code above and **change your_model, your_data, and your_group** you are good to go.

The added R script contains a reproducible example of the new approach using the Holzinger and Swineford (1939) dataset.



This was first published by [Michael Clark](https://m-clark.github.io/posts/2019-08-05-comparing-latent-variables/#supplemental-measurement-invariance).
