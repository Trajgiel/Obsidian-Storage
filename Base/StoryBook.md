2022-08-14 17:16
Tags: #StoryBook
__
# StoryBook
История - это отображение компоненты с конкретными пропсами
```js
npx storybook init //установить StoryBook в проект
```
```js
yarn storybook //запустить StoryBook
```
```tsx
import React from 'react';  
import { ComponentStory, ComponentMeta } from '@storybook/react';
import {action} from "@storybook/addon-actions";
  
import { Button } from './Button';  
  
export default {              //по дефолту создаётся компонент в StoryBook
	title: 'Example/Button',  //имя папки (Example) и в ней раздел (Button)
	component: Button,        //компонента которую мы используем
	argTypes: {               //описываем свойства нашей компоненты
	    backgroundColor: {
		    description: 'button color',   //описание пропса
			control: 'color',              //выбрать цвет кнопки
			table: {category: 'Styles'}    //раздел в котором буден настройка
		},
		onClick: {
			description: 'button clicked inside form',
			table: {category: 'Events'}
		},
	},
	args: {    //значение (пропсы) будет пренадлежать всем историям
		example: '1',
	},
	decorators: [ HOK ]      //тут хок который пернёт компоненту
} as ComponentMeta<typeof Button>;  

//на основе компоненты (Button), создаём образец (Template)
const Template: ComponentStory<typeof Button> = (args) => <Button {...args} />;  

//создаём историю, привязываем пустой объект наших пропсов (args)
export const Primary = Template.bind({});  
Primary.args = {        //наша история в StoryBook
  primary: true,        //отправляем в неё аргументы
  label: 'Button',
  onClick: action('Button clicked')   //при клике выдаст текст и данные
};   

export const Large = Template.bind({});  
Large.args = {  
  size: 'large',  
  label: 'Button',  
};  
  
export const Small = Template.bind({});  
Small.args = {  
  size: 'small',  
  label: 'Button',  
};
```

__
### Links
[[Install React]]