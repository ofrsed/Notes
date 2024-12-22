- Установка `pip install matplotlib`
- Импорт `import matplotlib.pyplot as plt`
- Обновление библиотеки `pip install --upgrade matplotlib`

y = np.array([1,2,3,4,5])


matplotlib.use('') - задать бекэнд
print(matplotlib.get_backend()) - получить бекэнд

![image](https://github.com/user-attachments/assets/5bdd2979-3b4b-4cfd-8b8b-0532b0921017)

```
lines = plt.plot(x, y)
plt.setp(lines, linestyle='-.')
```


`plt.show()` - передает управление пользователю

`plt.grid()` - добавить сетку

`plt.plot(X=Индексы, Y, "--",)` - отображает двумерные графики
  - `Y` - Множество точек по координате Y (X - индексы ячеек)
  - "--" - тип линиий
    - "-" - Непрерывная линия (используется по умолчанию)
    - "--" - Штриховая линия
    - "-." - Штрихпунктирная линия
    - ":" - Пунктирная линия
    - "None" или " " - Без рисования линии
  - `"--r"` или `"r--"` или `color='g'` или `color='#0000CC'` или `color=(R,G,B, alphacanal=None)` - указать цвет
  -  "--o" или "--s" - задать маркеры 
    - [markers](https://matplotlib.org/stable/api/markers_api.html)
    - [Grokking Algorithms](https://github.com/ofrsed/ofrsed/blob/main/Grokaem_algoritmy.pdf)
     
    https://matplotlib.org/stable/api/markers_api.html
`plt.plot(X1,Y1, X2, Y2)` / `plt.plot(X1,Y1) ; plt.plot(X2,Y2)` - несколько графиков в одних и тех же осях

