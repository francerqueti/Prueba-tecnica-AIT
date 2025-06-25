# Prueba-tecnica-AIT
Este proyecto contiene el desarrollo de la prueba técnica basada en los archivos entregados.

**ANAERÓBICOS**
Antes de comenzar con las actividades específicas, se aplicaron los requisitos de las instrucciones generales a ambas hojas:
Se configuró la región de la hoja de cálculo en Argentina. 
Se ordenaron los precios (columna D) de mayor a menor. Para esto se seleccionó el rango de datos y luego en Datos>Ordenar intervalo>Opciones avanzadas>Ordenar por columna D> de la Z a la A
Se revisaron cuestiones vinculadas al formato. Se re-configuró el tamaño de las filas para que todas tengan el mismo alto. Tambien se copio el formato de las columnas del modelo suministrado. Se eliminó el formato de las celdas que quedaron obsoletas luego de ordenarlos de mayor a menor. 
Ahora bien, para la primera parte de la actividad (separar el código del producto de su descripción), se añadió una columna (A), nombrada “Código” a la izquierda de la columna (B) “Producto”.
Para extraer únicamente el número de código de cada producto (columna B), se utilizó la función =LEFT(cadena; num_caracteres), con el objetivo de obtener una cantidad específica de caracteres desde el inicio de la celda que contenía el “producto” (en columna B). En este caso, se extrajeron los primeros 6 caracteres, ya que el código tenía una longitud fija de 6 dígitos.
Para extender la fórmula hasta el final de la base de datos de manera automática la función LEFT se anidó con la función ARRAY FORMULA, la cual permite extender una fórmula automáticamente a un rango de celdas sin necesidad de copiarla manualmente. Finalmente se aplico: =ARRAYFORMULA(LEFT(B5:B232;6)).
Se copiaron los resultados obtenidos y se pegaron solo como valores (Ctrl,Mayus,v) en la columna A (CODIGO), para eliminar las fórmulas utilizadas.
Se les otorgó formato numero (personalizado ######)
Para la segunda parte de la actividad, (separar la descripción del producto sin el código), se creó la columna (C) , nombrada “Descripción”. 
Asimismo, para esta parte se utilizaron celdas auxiliares para realizar los cálculos pertinentes que luego fueron eliminadas. 
Se detectó que el código y la descripción del producto se encontraban separados por una cantidad excesiva de espacios. Por eso, primero se utilizo TRIM para eliminar los espacios innecesarios. 
Se copiaron y pegaron solo los valores y se eliminó la columna auxiliar.
Luego el objetivo era extraer la descripcion del producto. Para esto fue necesario aplicar =MID(cadena; caracter_inicio; num_caracteres). Sin embargo, dado que cada producto tiene diferentes cantidades de caracteres, se aplicaron 2 funciones previas. Primero =LARGO(cadena) en columna D para saber cuantos caracteres tiene el texto del que se extraería la información. Y luego =SEARCH(“ “, cadena) en columna E para hallar a donde estaba el primer espacio (luego del numero del codigo) lo que permitirá conocer en qué numero de carácter empezaba la descripción del producto (valor obtenido +1). Teniendo esta información se aplico la funcion =MID(cadena; valor obtenido de search +1; valor obtenido del largo del texto - valor obtenido de search)
Al igual que la anterior esta función se anidó con ARRAY FORMULA, para extender el procedimiento al resto de las celdas. Finalmente en C5 se aplicó: ARRAYFORMULA(MID(B5:B23; E5:E232+1; D5:D232-E5:E232)
Por último se copiaron los resultados obtenidos en columna C, se copiaron como valores y se eliminaron las columnas auxiliares D y E.
El mismo procedimiento fue realizado en ambas hojas de cálculo (L-199% y L-199).

**FORD**
Para este caso tambien se comenzo aplicando las instrucciones generales:
Se configuró la región en Argentina
Se ordenaron los precios (columna D) de mayor a menor. 
Se revisó el formato general de la hoja de calculo.
Para eliminar todos los espacios de los codigos se utilizó la funcion SUBSTITUTE(texto a buscar; “ “; “”). De esta manera, la función busca todos los espacios y los sustituye por nada. 
Para el caso de los precios, siguiendo el modelo, se creo una columna (C) en donde el precio se encuentra en formato texto. 
Luego se aplicó =IF(RIGHT(C#;4)="0000"; VALUE(C#) / 10000; VALUE(C#)). Con esta funcion anidada se cumplimentó con varios requsitos: primero identificar aquellos números terminados en "0000" con RIGHT, en caso de encontrarlos se transformaban en números con VALUE y se dividen por 10000. En caso de que no sea un numero terminado en "0000", se transforma en numero. 
De esta manera en la columna D se encuentran números (formato número) que no terminan en "0000".
Se extendió el mismo procedimiento al resto de la columna. 
Se copiaron y pegaron solo valores.
Para añadir “,” en los últimos dos digitos se utilizo la opcion “Aumentar decimales” en la barra de tareas. 
La última actividad requirió una herramienta especial. Se utilizó la siguiente pagina: https://gchq.github.io/CyberChef/ para reconocer los simbolos codificados. 
Una vez que se obtuvieron estos simbolos se aplicó =SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(A#; "╝"; ""); "┤"; ""); "▄"; ""); "▒"; ""). De esta manera, esta función permite reemplazar los simbolos previamente identificados por nada (“”).


**HURL**
Se descargó el archivo CSV.
Se importó el archivo a una nueva hoja de cálculo en Google Sheets.
Para transformar el formato CSV en XLS,  se utilizó la herramienta "Dividir texto en columnas". Se seleccionó la columna que contenía todos los datos en bruto>Datos> Dividir texto en columnas> Como separador, se seleccionó: Coma.
Se duplicó la hoja y se nombró a cada una Hurl.CSV (Base original) y Hurl (Base trabajada). 
*Nota: para trabajar el archivo online google sheets no permite que sea un archivo xls. Tiene que ser xlsx. Cuando sea descargado se podrá transformar en el archivo solicitado. 
Luego, al igual que con los casos anteriores, se aplicaron las instrucciones generales:
Se cambió la región de la hoja de cálculo a Argentina
Se ordenaron los datos de mayor a menor según la columna de precio (F) 
Se añadió una fila para el encabezado de cada columna. 
Se otorgó el formato correspondiente siguiendo el modelo. Se aplicó el botón “colores alternos” para obtener el efecto deseado
Con el objetivo de corregir los precios suministrados por la base de datos en la columna F, teniendo en cuenta que tenía “2 dígitos de más”, se aplicaron dos funciones. 
En algunos casos, los valores en la columna F estaban en formato texto con punto decimal. Para corregir esto y asegurar que todos los datos de la columna sean números, se utilizó la función anidada =INT(VALUE(SUBSTITUTE(F#; "."; ",")) * 100). 
- substitute se utiliza para reemplazar el punto del texto por una coma para identificar los decimales
- con value se busca transformar el formato texto en número
- se lo multiplica por *100 porque siguiendo el modelo en la columna G no se observan decimales, esta fórmula permite correr los decimales dos lugares
- por último se utiliza int para asegurar que el resultado sea un número entero y eliminar decimales residuales. 
Ahora bien se agregó la columna G para colocar aquí el PRECIO FINAL. Teniendo en cuenta que los datos de la columna F tenían dos dígitos de más, se utilizó: INT(F# / 100). Esta función, combinada con la división permite volver a correr los decimales dos lugares y forzar a que al ser números enteros, terminen en ,00 tal como muestra el modelo. 
Todos los resultados fueron copiados (Ctrl+c) y pegados especial solo valores (Ctrl+Mayus+v) para eliminar las formulas del archivo.

**RASA**
En primer lugar para transformar el archivo TXT en XLS se descargó el archivo y se importó en una hoja de cálculo.
La base txt. suministrada no contenía un separador de columnas explícito, por lo que se utilizó la opción de Google sheets "separación automática"
Asi mismo se comprobó esta separación con la herramienta por ancho de columna de excel microsoft.
Se ajustó la configuración regional en Argentina. 
Se eliminaron los simbolos "→" (previamente decodificado), "伃" y "厲" con la funcion anidada =SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(B2 ; "→" ; "") ; "伃" ; "") ; "厲" ; ""). Se copiaron los valores y se pegaron. 
Se agregó la columna C (Articulo y descripcion) para almacenar la información de la columna A y la columna B. Para esto se utilizó +A# & " " & B#. Y se extendió la formula hacia el resto de la columna. Luego se copiaron los valores y se pegaron. 
Ahora bien, para resolver las consignas restantes (codigo numerico y precios) se decidieron los criterios explicados a continuación
Dado que en la consigna se requería que:
- El código sea un número entero
- El precio tuviera un formato similar al del archivo modelo
Y que, analizando la base, la única columna que presentaba valores enteramente numéricos era la originalmente ubicada en la columna F (formato texto, con 24 dígitos numéricos). Las demás columnas contenían datos alfanuméricos, por lo tanto, no podían ser consideradas como códigos numéricos enteros.
En un primer momento se interpretó esta columna como el codigo, pero esto implicaba que no existía una columna que representara el precio. A su vez, si se tomaba dicha columna como precio bruto, los valores resultantes eran excesivamente grandes y poco realistas al dividir por 100 (como es habitual en conversiones de precios almacenados sin coma decimal).
Tras consultar con la reclutadora y confirmar que el archivo modelo era correcto, se decidió considerar que esta columna contenía ambos campos unidos (código + precio).
Para resolverlo:
- Se dio formato de texto al valor de 24 dígitos.
- Se extrajeron los primeros 14 caracteres con =LEFT(celda; 14)
Luego se copiaron y pegaron los valores y se les aplico formato numerico personalizado para poder conservar los 0 en aquellos codigos con 0 a la izquierda
- Los últimos 10 caracteres se interpretaron como el precio bruto. Para extraerlo se utilizó =RIGHT(celda; LARGO(celda)-14)
Se copiaron y se pegaron los valores
Este segundo valor fue transformado en numero con dos decimales.
Este procedimiento fue asumido como razonable dado que:
- El modelo mostraba un código de 14 caracteres y un precio separado.
- La base no contenía los datos separados explícitamente.
- No se identificaron columnas alternativas que cumplieran con ambos requisitos.
  
Se subieron los archivos a GitHub
El archivo **README** fue redactado en GitHub
