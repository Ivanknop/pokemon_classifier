![who-s-that-pokemon](who-s-that-pokemon.jpg)

***

# ¿Quién es ese Pokémon?
## Análisis y clasificación de los Pokémon hasta 8va generación
Proyecto para la asignatura de **Minería de Datos** de la **Especialización en Inteligencia de Datos orientada a Big Data** 

### ¿Qué son los Pokémon? Una breve introducción 

Pokémon es una franquicia de videojuegos, animes y mangas que cuenta con 28 años y parece no tener fin. La palabra Pokémon es una contracción del japonés Poketto Monsutā, que significa «monstruo de bolsillo»1. Los animales, plantas, espíritus e, incluso, objetos inanimados que aparecen en nuestro mundo, se representa, en este universo, con estas criaturas llamadas Pokémon. Actualmente existen 1025 especies, que se elevan a 1172 al sumar variaciones regionales; Pokémon cuenta con veinte regiones en las que transcurren las diferentes historias según sea la plataforma en que se desarrollan.

Cada especie Pokémon posee una serie de estadísticas, o stats, a saber: Puntos de Salud (PS), Ataque, Defensa, Velocidad, Ataque Especial, Defensa Especial. Además, cada Pokémon tiene tipos que determinan sus fortalezas y debilidades; cada tipo tiene ventajas y/o desventajas sobre otros tipos. Estos son: planta, agua, fuego, tierra, roca, volador, lucha, bicho, eléctrico, veneno, psíquico, fantasma, siniestro, hada, dragón, acero, hielo, normal2. Cada Pokémon puede ser monotipo o tener un segundo tipo.

Adicionalmente, cada Pokémon pertenece a una generación que determina el momento en que fue introducida esa especie al listado general de Pokémon3. Las generaciones interesan porque se han agregado tipos a la lista preexistente y algunos Pokémon recibieron nuevos, cambiando así sus fortalezas y debilidades; también, con las nuevas generaciones, se agregaron evoluciones, preevoluciones y megaevoluciones que amplifican la red de relaciones entre los Pokémon.

Para el asunto central de este trabajo, la evolución Pokémon no es algo significativo; alcanza con explicar que son un punto importante en este mundo porque algunos Pokémon pueden cambiar de especie al crecer. La nueva especie evolucionada suele mantener el o los tipos de su predecesor, quizás agregar uno, y se incrementan las stats significativamente.

El universo íntegro fue creado por un Pokémon singular, al que el fandom se refiere como Dios, llamado Arceus. Él, al igual que otros Pokémon específicos, son catalogados como Legendarios. Por simplificación para el lector, y porque en el archivo que se utiliza de base también está así, todos estos Pokémon que no son del común (singulares, legendarios, pseudolegendarios y ultraentes) serán considerados como Legendarios. Los Pokémon legendarios también poseen la misma cantidad de atributos para las stats y uno o dos tipos; es decir que son clasificables como el resto de los Pokémon.

Dado que el universo Pokémon está en constante crecimiento, este tipo de análisis podría permitir preparar a los jugadores, lectores y televidentes de la franquicia para las nuevas especies que se introduzcan. Entre tantas posibles preguntas, una de ellas es: ¿es posible, con los datos de los Pokémon existentes, deducir la composición de futuras generaciones? Veamos a qué conclusiones arribamos.

***
### Objetivo

Pretendemos aproximamos a una predicción sobre cómo será una siguiente generación. Dado que los datos analizados corresponden a las primeras 8 generaciones y ya existe una 9na, al finalizar este trabajo buscaremos averiguar si nos hemos acercado a este objetivo. El último apartado incluirá el pronóstico, la realidad de la 9na generación y el grado de aproximación entre uno y otro. 

Esperamos sea de interés para fanáticos, o no tanto, de la franquicia.

***

El trabajo se estructura de la siguiente forma:

1. Descripción del dataset, limpieza de datos faltantes y de errores de tipeo.
2. Categorización entre Pokémon Legendarios, Megaevoluciones, Gigantamax y Comunes.
3. Distribución de tipos según cada categoría.
4. Evaluación de los stats para cada tipo y para cada categoría.
5. Árbol de clasificación.
6. Reglas de clasificación.
7. Distribución de tipos por generación.
8. Pronósticos y conclusiones.

***

### Acerca del dataset
El dataset fue descargado de: https://www.kaggle.com/datasets/jaidalmotra/pokemon-dataset 

Consta de 1072 filas de datos que representan 898 especies de pokémon, incluyendo variedades regionales; Las otras 174 filas de datos corresponden a megaevoluciones o versiones gigantamax; estas son una versión ampliada de una especie dada. En el dataset encontraremos todo esto con el mismo identificador numérico, que proviene de la Pokedex, nomenclador del propio universo Pokémon -una suerte de Enciclopedia Pokémon. 

El dataset cuenta hasta la 8va generación; dado que existe una 9na, lausaremos para validar las conclusiones finales.

**Cada dato consta de 13 columnas:**

1.   **Number**: Número según la Pokedex. Es un n° entero.
2.   **Name**: Nombre del Pokémon o de la variación o versión Gigantamax o Megaevolución. Es un string.
3.   **Type1**: Tipo princial, obligatorio. Es un string.
4.   **Type2**: Segundo tipo, es optativo. Es un string.
5.   **Total**: Totalizador del total de stats. N° entero.
6.   **Hp**: Puntos de vida. N° entero.
7.   **Attack**: Ataque. N° entero.
8.   **Defense**: Defensa. N° entero.
9.   **Sp_attack**: Ataque especial. N° entero.
10.   **Sp_defense**: Defensa especial. N° entero.
11.   **Speed**: Velocidad. N° entero.
12.   **Generation**: A qué generación pertenece. N° entero del 1 al 8.
13.   **Legendary**: Si es o no legendario; incluye singulares y ultraentes. Es boolean.

***

Para este trabajo utilizaremos

- Pandas 
- Matplotlib
- Numpy
- Sklearn
- Wittgenstein
