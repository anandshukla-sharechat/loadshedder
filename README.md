# loadshedder

 This library is used to shed excess load on the basis of cpu utilisation. You can use instance of prometheus GaugeVec & CounterVec to plot CPU utilisation & sheddings metric. To get the library simply run : 

    go get -u github.com/anandshukla-sharechat/loadshedder@main

## NewSheddingStat : 
    use this function to create an instance of shedding stat.

 

## GinUnarySheddingInterceptor : 
    use this function as middleware. It needs sheddingStat, cpu threshold and probe API (for disabling load shedding for live & readiness check api endpoint)


##    Example :
### In main.go add these lines 


    sheddingStat := loadshedder.NewSheddingStat(loadSheddingMetrics *prometheus.CounterVec, cpuMetrics *prometheus.GaugeVec) // returns object of *SheddingStat type
    router.Use(loadshedder.GinUnarySheddingInterceptor(shedderEnabled bool, cpuThreshold int64, probeAPI string, sheddingStat *SheddingStat))

    
shedderEnabled : boolean flag to enable load shedder or not
cpuThreshold : the threshold beyond which load shedding starts
probeAPI : To disable load shedding for api which is responsible for liveness/readiness probe checks 


    
