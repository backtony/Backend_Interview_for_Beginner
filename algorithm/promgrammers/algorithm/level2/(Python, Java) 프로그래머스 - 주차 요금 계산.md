[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/92341)


## 풀이
```python
import math
from collections import defaultdict


def solution(fees, records):
    logs = defaultdict(list)

    for record in records:
        split = record.split()
        time = split[0]
        car = split[1]
        logs[car].append(time)

    answer = []
    for car_num in sorted(logs.keys()):
        times = logs.get(car_num)
        price = calculate_total_price(fees, times)
        answer.append(price)

    return answer


def calculate_total_price(fees, times):
    free_time = fees[0]
    base_amount = fees[1]
    extra_time = fees[2]
    extra_amount = fees[3]
    
    if len(times) % 2 == 1:
        times.append("23:59")

    total_minutes = 0
    for out in range(1, len(times), 2):
        in_minutes = time_to_minutes(times[out - 1])
        out_minutes = time_to_minutes(times[out])
        total_minutes += out_minutes - in_minutes

    if total_minutes <= free_time:
        amount = base_amount
    else:
        amount = base_amount + int(math.ceil((total_minutes - free_time) / float(extra_time))) * extra_amount

    return amount


def time_to_minutes(time):
    split = time.split(":")
    return int(split[0]) * 60 + int(split[1])
```


## Java 풀이
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

class Solution {
    public int[] solution(int[] fees, String[] records) {

        Map<String, List<String>> logs = new HashMap<>();
        for (String record : records) {
            String[] split = record.split(" ");
            String time = split[0];
            String carNum = split[1];
            List<String> timeRecords = logs.getOrDefault(carNum, new ArrayList<>());
            timeRecords.add(time);
            logs.put(carNum, timeRecords);
        }

        List<String> keys = logs.keySet().stream().sorted().collect(Collectors.toList());

        List<Integer> answer = new ArrayList<>();
        for (String carNum : keys) {
            answer.add(calculateTotalPrice(fees, logs.get(carNum)));
        }

        return answer.parallelStream().mapToInt(Integer::intValue).toArray();

    }

    private int calculateTotalPrice(int[] fees, List<String> times) {
        if (times.size() % 2 == 1) {
            times.add("23:59");
        }

        int totalTime = 0;
        for (int out = 1; out < times.size(); out += 2) {
            int inTime = timeToMinutes(times.get(out - 1));
            int outTime = timeToMinutes(times.get(out));
            totalTime += outTime - inTime;
        }

        int baseTime = fees[0];
        int baseAmount = fees[1];
        int extraTime = fees[2];
        int extraAmount = fees[3];

        int amount = 0;
        if (totalTime <= baseTime) {
            amount = baseAmount;
        } else {
            amount = baseAmount + (int) (Math.ceil((totalTime - baseTime) / (double) extraTime)) * extraAmount;
        }

        return amount;
    }

    private int timeToMinutes(String time) {
        String[] split = time.split(":");
        return Integer.parseInt(split[0]) * 60 + Integer.parseInt(split[1]);
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.ceil

class Solution {
    fun solution(fees: IntArray, records: Array<String>): IntArray {
        val cars = records.groupBy { it.split(" ")[1] }.map {
            val minutes = if (it.value.size % 2 != 0) {
                it.value.toMutableList().apply { add("23:59 ${it.key} OUT") }
            } else {
                it.value
            }.windowed(size = 2, step = 2).sumOf { record ->
                record[1].split(" ")[0].split(":").let {
                    it.first().toInt() * 60 + it.last().toInt()
                }.minus(
                    record[0].split(" ")[0].split(":").let {
                        it.first().toInt() * 60 + it.last().toInt()
                    }
                )
            }

            Car(
                id = it.key,
                minutes = minutes
            )
        }

        val baseTime = fees[0]
        val baseAmount = fees[1]
        val perMin = fees[2]
        val perFee = fees[3]
        return cars.sortedBy { it.id }.map { it.fee(baseTime, baseAmount, perMin, perFee) }.toIntArray()
    }

    data class Car(
        val id: String,
        val minutes: Int,
    ) {
        fun fee(baseTime: Int, baseFee: Int, perMinute: Int, perFee: Int): Int {

            if (minutes <= baseTime) {
                return baseFee
            }

            val extraTime = minutes - baseTime
            val extraFee = (ceil((extraTime / perMinute.toDouble())) * perFee).toInt()

            return baseFee + extraFee
        }
    }
}
```
