2023-02-17 14:39
Tags: #CSS 

---
`grid-template-columns` - используется для определения количества и ширины колонок
- grid-template-columns: 200px auto 100px
- grid-template-columns: 100px 50px 100px
- grid-template-columns: repeat(3, 80px)
![[grid-template-columns.png]]

`grid-template-rows` - используется для определения количества и высоты строк
- grid-template-rows: 200px auto 100px
![[grid-template-rows.png]]

---

`grid-template-areas` - используется для определения количества пространства, занимаемого ячейкой Грида (grid cell), в терминах колонок и строк, в родительском контейнере
- grid-template-areas: 
	"a a a"
	"b c c"
	"b c c";
![[grid-template-areas.png]]

`grid-area` - определяются названия областей

---

`gap` - задаёт отступы между столбцами и строками
- `column-gap` - добавления отступа между колонками
- `row-gap` - добавления отступов между строками

`justify-items`  или `align-items` - используется для позиционирования грид-элементов внутри грид-контейнера вдоль **главной оси** или **поперечной оси**
- `start` - выравнивает по левой стороне области
- `end` - выравнивает по правой стороне области
- `center` - выравнивает по центру области
- `stretch` - заполняет всю ширину области (по умолчанию)

`justify-content` или `align-content` - используется для позиционирования самого грида внутри грид-контейнера вдоль **основной оси** или **поперечной оси** 
- `start` - выравнивает сетку по левой стороне контейнера.
- `end` - выравнивает сетку по правой стороне контейнера.
- `center` - выравнивает сетку по центру контейнера.
- `stretch` - масштабирует элементы чтобы сетка могла заполнить всю ширину контейнера.
- `space-around` - одинаковое пространство между элементами, и полуразмерные отступы по краям.
- `space-between` - одинаковое пространство между элементами, без отступов по краям.
- `space-evenly` - одинаковое пространство между элементами, и полноразмерные отступы по краям.
__
### Links
[[Base/CSS/CSS]]
