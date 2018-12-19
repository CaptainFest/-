# Separating_hyperplane
<a href="url"><img src=https://github.com/CaptainFest/Separating_hyperplane/blob/master/separating_line.png align="center" height="360" width="480" ></a>
## Условие задачи
Имеются два множества точек в декартовой прямоугольной системы координат. Точка с номером i (в условной нумерации) может принадлежать 1-му или 2-му множеству. Какому множеству принадлежит точка заранее известно. 

Необходимо попытаться построить такую прямую линию, которая разделяет группу точек множества 1 и множества 2, то есть такую прямую линию, что все точки из множества 1 лежат строго по одну сторону относительно этой линии, а все точки множества 2 — строго по другую. И ответить на вопрос, возможно ли построение такой прямой, либо же нет.

Не допускается построение такой разделяющей линии, на которой лежит какая-либо точка, то есть прямая линия должна разделять группы точек 1-го и 2-го множеств строго. 

## Формат ввода
В первой строке входных данных записано одно целое число n (1≤n≤300) — количество всех точек.

В последующих n строках записаны координаты звезд.

В i-й из этих строк записано три целых числа — ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20x_%7Bi%7D%2C%5C%2C%20y_%7Bi%7D%2C%5C%2C%20t_%7Bi%7D%5C%2C%20%28-10%5E%7B4%7D%5Cleqslant%20x_%7Bi%7D%2C%20y_%7Bi%7D%20%5Cleqslant%2010%5E%7B4%7D%2C%20t_%7Bi%7D%20%5Cin%20%7B1%2C2%7D%29), разделенных одним пробелом Здесь ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20t_%7Bi%7D%3D1), если точка принадлежит множеству 1, и ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20t_%7Bi%7D%3D2) в противном случае.

Гарантируется, что входные данные не содержат двух звезд с совпадающими координатами. 

## Формат вывода
В единственной строке выходных данных выведите Yes, если существует разделяющая линия, или No, если разделяющей линии не существует. 

## Решение
Решение строится из двух предположений. Два множества можно разделить гиперплоскостью, если их минимальная выпуклая оболочка не пересекается. А также если одна выпуклая оболочка не находилась внутри другой.
<br>
<a href="url"><img src="https://github.com/CaptainFest/Separating_hyperplane/blob/master/case%201.bmp" align="float:left" height="333" width="419" ></a>
<a href="url"><img src="https://github.com/CaptainFest/Separating_hyperplane/blob/master/case%202.bmp" align="float:right" height="333" width="419" ></a>
<br>
Случаи, когда эти свойства не выполняются показаны на картинках.<br>
Итак, решение начинается с построения выпуклых оболочек с помощью метода Джарвиса. Это позволит как сократить количество рассматриваемых точек, так и проверить эти 2 свойства. Далее проверяем пересечение всех полученных отрезков одной выпуклой оболочки с другой. Данную проверку выполняет функция intersect() <br>
Отрезки ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Coverline%7Bp1p2%7D) и ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Coverline%7Bp3p4%7D) пересекаются тогда и только тогда, когда одновременно выполнены следующие 3 условия: <br>
а) пересекаются ограничивающие их прямоугольники
b) ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cbegin%7Bbmatrix%7D%20%5Cbegin%7Bpmatrix%7D%20p3-p1%20%5Cend%7Bpmatrix%7D%20%5Ctimes%20%5Cbegin%7Bpmatrix%7D%20p2-p1%20%5Cend%7Bpmatrix%7D%20%5Cend%7Bbmatrix%7D%20%5Ccdot%20%5Cbegin%7Bbmatrix%7D%20%5Cbegin%7Bpmatrix%7D%20p4-p1%20%5Cend%7Bpmatrix%7D%20%5Ctimes%20%5Cbegin%7Bpmatrix%7D%20p2-p1%20%5Cend%7Bpmatrix%7D%20%5Cend%7Bbmatrix%7D%5Cleqslant%200)
c) ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cbegin%7Bbmatrix%7D%20%5Cbegin%7Bpmatrix%7D%20p1-p3%20%5Cend%7Bpmatrix%7D%20%5Ctimes%20%5Cbegin%7Bpmatrix%7D%20p4-p3%20%5Cend%7Bpmatrix%7D%20%5Cend%7Bbmatrix%7D%20%5Ccdot%20%5Cbegin%7Bbmatrix%7D%20%5Cbegin%7Bpmatrix%7D%20p2-p3%20%5Cend%7Bpmatrix%7D%20%5Ctimes%20%5Cbegin%7Bpmatrix%7D%20p4-p3%20%5Cend%7Bpmatrix%7D%20%5Cend%7Bbmatrix%7D%5Cleqslant%200)
Второй случай требует рассмотрения нахождения точек одного множества в выпуклой оболочке другой. Данное свойство проверяется слудующим образом. Для того, чтобы точка находился внутри выпуклой оболочки, необходимо, чтобы ![equation](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cbegin%7Bpmatrix%7D%20p1-p2%20%5Cend%7Bpmatrix%7D%5Ctimes%20%5Cbegin%7Bpmatrix%7D%20p-p1%20%5Cend%7Bpmatrix%7D) было или всегда неотрицательно, или всегда неположительно. Данная проверка не должна выполняться, если минимальная выпуклая оболочка представляет из себя линию. 
