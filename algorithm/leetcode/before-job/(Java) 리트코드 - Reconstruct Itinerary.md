[문제 링크](https://leetcode.com/problems/reconstruct-itinerary/)


## Java 풀이
```java
import java.util.*;

class Solution {

    LinkedList<String> answer = new LinkedList<>();

    public List<String> findItinerary(List<List<String>> tickets) {
        Map<String, LinkedList<String>> itinerary = new HashMap<>();
        for (List<String> ticket : tickets) {
            String start = ticket.get(0);
            String destination = ticket.get(1);
            LinkedList<String> next = itinerary.getOrDefault(start, new LinkedList<>());
            next.add(destination);
            itinerary.put(start, next);
        }

        for (String key : itinerary.keySet()) {
            Collections.sort(itinerary.get(key));
        }

        dfs("JFK", itinerary);

        return answer;
    }

    // 연결된 간선 쭉 타고 들어가서 마지막 도착지에 도착해서 return 하면서 그것대로 기록한다.
    private void dfs(String start, Map<String, LinkedList<String>> itinerary) {
        LinkedList<String> graph = itinerary.getOrDefault(start, new LinkedList<>());
        while (!graph.isEmpty()) {
            String next = graph.pollFirst();
            dfs(next, itinerary);
        }
        
        // 이것이 핵심!!
        answer.addFirst(start);
    }

    public static void main(String[] args) {
        List<List<String>> tickets = new ArrayList<>();
        tickets.add(List.of("JFK", "KUL"));
        tickets.add(List.of("JFK", "NRT"));
        tickets.add(List.of("NRT", "JFK"));
        new Solution().findItinerary(tickets);
    }
}
```
