[1]: http://rosettacode.org/wiki/Priority_queue

# [Priority queue][1]

```ruby
class PriorityQueue {
    has tasks = []
 
    method insert (Number priority { _ >= 0 }, task) {
        tasks.len ... priority -> each { |n|
            tasks[n] = []
        }
        tasks[priority].append(task)
    }
 
    method get      { tasks.first { !.is_empty } -> shift }
    method is_empty { tasks.all   {  .is_empty } }
}
 
var pq = PriorityQueue()
 
[
    [3, 'Clear drains'],
    [4, 'Feed cat'],
    [5, 'Make tea'],
    [9, 'Sleep'],
    [3, 'Check email'],
    [1, 'Solve RC tasks'],
    [9, 'Exercise'],
    [2, 'Do taxes'],
].each { |pair|
    pq.insert(pair...)
}
 
say pq.get while !pq.is_empty
```

#### Output:
```
Solve RC tasks
Do taxes
Clear drains
Check email
Feed cat
Make tea
Sleep
Exercise
```