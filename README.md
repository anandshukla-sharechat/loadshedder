# loadshedder

 This library is used to shed excess load on the basis of cpu utilisation. You can use instance of prometheus GaugeVec & CounterVec to plot CPU utilisation & sheddings metric

## NewSheddingStat : 
    use this function to create an instance of shedding stat.

 

## GinUnarySheddingInterceptor : 
    use this function as middleware. It needs sheddingStat, cpu threshold and probe API (for disabling load shedding for live & readiness check api endpoint)


## Example :
    In main.go add these lines 


    sheddingStat := loadshedder.NewSheddingStat(loadSheddingMetrics *prometheus.CounterVec, cpuMetrics *prometheus.GaugeVec) // returns object of *SheddingStat type
    router.Use(loadshedder.GinUnarySheddingInterceptor(shedderEnabled bool, cpuThreshold int64, probeAPI string, sheddingStat *SheddingStat))
