  <img src="https://github.com/ofrsed/Notes/blob/main/data%20structures%20and%20algorithms/O.png" title="python" alt="python" width="600"  />;

`О большое` - запись для оценки худшего случая, или для ограничения заданной функции сверху. Это позволяет сделать асимптотическую оценку верхней границы скорости роста времени выполнения алгоритма.

# Бинарный поиск (log n)

```
d = [-1, -3, 2, 4, 5, 7, 8, 9]
n = len(d)
 
search_v = 9
left, right = 0, n-1
 
while left <= right:
    middle = (left + right) // 2
    v = d[middle]
    if v == search_v:
        print(v, middle)
        break
    elif v < search_v:
        left = middle + 1
    elif v > search_v:
        right = middle - 1
else:
    print("значение не найдено")
```

NP - полные задачи. Число всех возможных вариантов = n! (факториал)
