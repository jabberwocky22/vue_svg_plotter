# Vue_Svg practice
## File structure
>+ root/src/App.vue
>+ root/src/main.js
>+ root/src/components/Input.vue
>> Input.vue contains textarea and excution button, which passes textare value to parent component. 
>+ root/src/components/renderer.vue
>> renderer.vue contains container, error collector and svg render section.
>> Codes for coding reading also located here
***
## How to install

***This project is developed based on Vue 3.11.0 and Node v9.11.1***
>+ After clone, please open terminal and enter in the root folder and run
>>`npm install`
>>to install all dependencies.

>+ After dependencies are installed, please run
>>`npm run serve`
>> which would build a development environment so we could browse in local server.

>+ On terminal, it should tell you the app running on which local host.
>> normally it is `http://localhost:8080/`, copy the url into browser and you shall see the app.

>+ To quit, find the hosting terminal and press
>> `ctrl + c`  
>> enter y to quit
***

## Svg code introduction

***One shape per line***  
***Press run to execute your codes***

>+ Circle  
>> Declare `"c"` at the beginning in order to tell the app it is a circle.  
>> Accepts 3 attributes:
>> ["cx"(centre x),"cy"(centre y),"r"]  
>> example: c 10 10 100  

>+ Rectangle  
>> Declare `"r"` at the beginning in order to tell the app it is a rectangle.  
>> Accepts 4 attributes:
>> ["x", "y", "width", "height"]  
>> example: r 10 10 100 100 

>+ Polygon  
>> Declare `"p"` at the beginning in order to tell the app it is a polygon.  
>> Accepts sets of coordinates attributes and allowing a space between each set:
>> ["x","y" "x","y" ...]  
>> example: y 200,10 250,190 160,210

>+ Line  
>> Declare `"l"` at the beginning in order to tell the app it is a line.  
>> Accepts 5 attributes:
>> ["x1", "y1", "x2", "y2", "stroke"(stroke width)]  
>> example: l 10 10 100 100 3
***

## Error collector
>>***If any error occurs during rendering, it shall give a notice at right top corner***