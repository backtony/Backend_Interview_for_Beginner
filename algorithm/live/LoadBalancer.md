
## LoadBalancer 설계

server가 여러 대 있고 ratio 비율이 주어졌을 때, 비율별로 라우팅하는 코드를 작성하시오.

```kotlin
class LoadBalancer() {
    fun routeRequest(serverConfigs: List<ServerConfig>): ServerConfig {
        var cumulativeSum = 0 // 총 누적값
        
        // 구간별 누적값
        val cumulativeRatios = serverConfigs.map {
            cumulativeSum += it.ratio
            cumulativeSum
        }
        
        // 구간 안에 들어오는 랜덤값 추출
        val randomValue = Random.nextInt(cumulativeRatios.last())
        val serverIdx = cumulativeRatios.indexOfFirst { randomValue < it }

        return serverConfigs[serverIdx]
    }
}
```
