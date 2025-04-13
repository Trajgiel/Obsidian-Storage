2022-08-31 11:28
Tags: #SASS
__
# SASS
`yarn add sass`

---
```scss
@import "./common/styles/variablies";

.title {  
    text-align: center;  
    margin-bottom: 50px;  
    span {  
        background-color: $bgSecondColor;  
        line-height: 1.8;   
        color: rgba(33,37,41,var(--bs-text-opacity));  
        padding: 0.2rem 0.7rem;  
    }  
    h2 {  
        font-size: 2.50rem;  
        margin-top: 0;  
        line-height: 1.2;  
    }
    &, ::after, ::before {  
	  box-sizing: border-box;  
	}  
}
```
& - родительский элемент

---
src/common/styles/variablies.scss
```scss
$texColor: #212529;  
$bgColor: #fff;  
$bgSecondColor: #f5df4e;
```
---
src/common/styles/mixins.scss
```sccs
@mixin text($color, $fontSize) {
	color: $color;
	font-size: $fontSize;
}
```
```scss
@import "./common/styles/mixins";

.title {
@include text(red, 16px)
}
```
__
### Links
[[Base/CSS/CSS]]