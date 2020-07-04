---
title: Power BI, una introducción para principiantes
author: José Duarte
date: 2020-05-04 20:55:00 +0800
categories: [Power BI, Posts]
tags: [Power BI]
pin: true
---

Recuerdo perfectamente que cuando comencé a tratar de involucrarme en el tema del análisis y la visualización de datos, me sentía abrumado por la cantidad tan grande de herramientas, libros, cursos en línea y tantas otras cosas que no sabía por donde empezar. Agregándole el hecho de que mi campo no era la informática y no tenía ni idea de que era una base de datos, un star schema o siquiera una Query, algunos de los recursos que encontraba resultaban bastante difíciles (más por la terminología y los conocimientos previos que se asumían que por la materia en cuestión). 

Es por esto que decidí escribir este blog para dar una explicación bastante general de las partes que se utilizan en Power BI tratándo de describirlas lo más simple posible y sin utilizar conceptos muy técnicos

## ¿Para qué sirve realmente Power BI y cuáles son sus partes básicas?

Cuando vi por primera vez algunos videos y tutorials en donde se demostraban la capacidades de la herramienta, no lograba decifrar con toda claridad cuál era el objetivo de ésta; ¿Servía para transformar grandes cantidades de datos de forma más rápida que en Excel?, ¿o su verdadera función era hacer gráficos "bonitos"?, ¿O acaso era más sencillo compartir reportes de información comparado con el clásico PDF o Power Point?

Lo cierto es que sirve para todo esto. Algunas de las funciones que me han sido más útiles son:
- acceder a información localizada en diferentes fuentes
- transformar  esta información, crear gráficas que *estén conectadas entre ellas* y permitan interacciones entre ellas (por ejemplo, un filtrado dinámico)
- hacer reportes de forma *automatizada* que permitan refrescar la información del reporte con prácticamente un solo click
- subir el reporte a la nube y compartirlo con otras personas, con la ventaja de que si le hacía cambios al reporte y los subía de nuevo a la nube, no era necesario volver a enviar el reporte, sino que el usuario podía acceder a la nube y ver siempre la versión final

Dicho esto, hay diferentes partes que integran Power BI y cada parte (o incluso la combinación de ellas) realizan las funciones comentadas arriba. Yo dividiría al software en las siguientes partes:

- Power Query
- Power BI Desktop
- Power BI Servicio

Hay varios tutorials y libros que utilizan otra segmentación más minuciosa, pero para los propósitos de esta entrada (que es dar una visión general sin abrumar con detalles) me parece que este nivel de detalle es más que suficiente.

A continuación explico en que consiste cada una de ellas.


## Power Query

Power Query es la parte de Power BI que se encarga de hacer queries y de transformar los datos, y es la parte que más me sorprendió dada la facilidad con la que realizaba algunas de las tareas que en Excel eran mucho más complicadas. 

A grandes rasgos, Power Query se encarga de obtener y transformar la información que se va a utilizar para hacer el reporte. Una de las principales diferencias de usar Power BI para el reporteo en lugar del clásico Excel es que ahora pudes usar información de muchos "lugares" (como por ejemplo bases de datos o servicios web) y no solo de los Excel que tengas en tu computadora. A esta acción de ir a una base de datos (ya sea un excel local, un csv, una hoja de google sheets en internet o tus métricas de FB) y 'jalar'/'sacar' información para analizarla se le llama Query. 

Un ejemplo práctico: Supongamos que tienes una hoja de cálculo en Google Sheets que contiene las ventas de tu empresa y quieres analizarla y hacer gráficas. Lo 'clásico' sería ir a Google Sheets, entrar a la hoja, copiar la información, pegarla en un Excel y empezar a hacer gráficas ahí mismo, y repetir este proceso mes con mes (suponiendo que tu reporte lo quieres hacer mensualmente). Power Query te permite obtener (hacer un query) la información de la hoja de Google Sheets directamente sin necesidad de copiar ni pegar nada, sólo hay que meter el link de la hoja y listo. Cada vez que quieras tomar la información más nueva, basta con hacer click en el botón de "Refresh" y Power Query se encarga del resto. Incluso es posible configurar Power Query para que tome la información de forma automatizada, en un horario y periodicidad establecida (por ejemplo, una vez al día a las 8 a.m.).

Una vez obtenida la información, Power Query también te permite trasformarla. Por transformar información me refiero al hecho de aplicar una serie de pasos que permitan obtener información nueva a partir de información que ya teníamos. Para tener un ejemplo de transformación puedes imaginar un Excel en donde tienes una columna de precios en dólares (información que ya tenemos) y hacer una nueva columna en donde multiplicar la columna de precios en dólares por la tasa de cambio y obtienes precios en pesos (información nueva). 

Esta parte de las transformaciones en Power Query es confusa para las personas que vienen de Excel debido a la forma en la que Power Query aplica sus transformaciones. La diferencia principal radica en que en Excel puedes (y debes) aplicar la transformaciónpor celda, mientras que en Power Query lo haces por filas o por columnas. 

De nuevo un ejemplo, supongamos que tenemos una tabla con 20 precios de productos de Amazon que están en diferentes monedas. En Excel, lo que haría es crear una formula que multiplique el precio en dólares por la tasa de cambio, y después copiaría esta formula al resto de las celdas. Si tuviera en esta columna una celda que estuviera en rublos, pues podría ajustar la fórmula en esta única celda para cambiar el tipo de cambio. Al final, aunque estoy copiando la misma fórmula, tengo 20 fórmulas, una para cada celda (e incluso algunas fórmulas pueden ser diferentes si hay varias monedas). En Power Query solo necesitas una sola fórmula, y *esa fórmula se aplica para toda la columna*, es decir, Power Query toma toda la fila y multiplica todos los valores de la fila por un solo tipo de cambio. A este tipo de operaciones se le llama a veces **operaciones vectorizadas**, que si has tomado Álgebra Matricial te hará sentido, pues cuando multiplicas un vector por un número, en realidad estas automáticamente multiplicando todos los elementos del vector por dicho número. 

Esta forma de trabajar de Power Query es muy práctica, pero requiere de que sepas estructurar bien tu información (es posible ver que en el ejemplo que tratabamos, si tu columna tiene precios en varias monedas, Power Query va a querer aplicarle el mismo tipo de cambio a todas, lo que estaría mal), sin embargo, es una de las principales causas de confusión (y frustración) de los usuarios que vienen de Excel y están acostumbrados a trabajar celda por celda. 

