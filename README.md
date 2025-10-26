<!-- ───────────────────────────────────────────────────────────────────────────── -->
<!-- 🎌 PORTADA POKÉMON (SIN CAMBIOS)                                            -->
<!-- ───────────────────────────────────────────────────────────────────────────── -->
<p align="center">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png" width="80" alt="Pikachu">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/6.png"  width="80" alt="Charizard">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/65.png" width="80" alt="Alakazam">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/143.png" width="80" alt="Snorlax">
</p>

<h1 align="center">🎮🧪 Poke-Laboratorio 7: Ensambles de Votación — <i>¡Atrapa el mejor modelo!</i> 🧠⚡</h1>

<p align="center">
  <a href="#indice"><img alt="Índice Interactivo" src="https://img.shields.io/badge/Índice-Interactivo-ff4757?style=for-the-badge&logo=readme&logoColor=white"></a>
  <img alt="Python 3.10+" src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img alt="scikit-learn" src="https://img.shields.io/badge/scikit--learn-Ensambles-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white">
  <img alt="PokéAPI" src="https://img.shields.io/badge/PokéAPI-Data-EE1515?style=for-the-badge">
  <img alt="Made with ❤️" src="https://img.shields.io/badge/Made%20with-❤️%20by%20Trainers-ff6b81?style=for-the-badge">
</p>

<p align="center">
  <img src="https://svgur.com/i/12Xo.svg" alt="" width="75%">
</p>

<!-- ───────────────────────────────────────────────────────────────────────────── -->
<!-- 📑 ÍNDICE INTERACTIVO                                                        -->
<!-- ───────────────────────────────────────────────────────────────────────────── -->
<h2 id="indice">📚 Índice Interactivo</h2>

<details open>
  <summary><b>📌 Navega por el README</b> </summary>

- 🏁 <a href="#-poke-laboratorio-7-ensambles-de-votación-¡atrapa-el-mejor-modelo">Portada</a>
- 🎯 <a href="#introducción-y-objetivos">Introducción y Objetivos</a>
- 🧑‍🏫 <a href="#entrenadores">Entrenadores</a>
- 🗺️ <a href="#parte-1-construcción-del-dataset-descarga-etiqueta-y-muestra-estratificada">Parte 1. Dataset</a>
- 🤖 <a href="#parte-2-modelos-individuales-knn-regresión-logística-árbol-y-svm">Parte 2. Modelos individuales</a>
- 🏆 <a href="#parte-3-ensambles-de-votación-dura-suave-y-ponderada">Parte 3. Ensambles</a>
- 📁 <a href="#-estructura-del-repositorio">Estructura del repositorio</a>
- 🎲 <a href="#curiosidades-poké">Curiosidades Poké</a>

</details>

---

## *Introducción y Objetivos*

> 🎒 **Misión del entrenador:** Explorar la PokéAPI, construir un CSV canónico, definir *PowerScore* y la etiqueta `strong`, y preparar el terreno para combinar modelos como si armaras tu equipo de la Liga.  
> 💡 **Tip:** Piensa cada clasificador como un líder de gimnasio con estilo propio. La clave es la sinergia.

En este Pokeproyecto tratamos a la PokéAPI como una Pokédex para programadores (consulta directa al "Profesor Oak" de los datos) y transformamos ese universo en un CSV canónico donde cada fila es un Pokémon listo para entrar a combate (height, weight, base_experience, type_main). Con las estadísticas oficiales calculamos un PowerScore y definimos la etiqueta strong usando el percentil 75 (criterio objetivo para decidir quién está listo para la Liga Pokémon y quién necesita más entrenamiento en la Ruta 1). Para evitar que nuestros resultados dependan de si abundan Gyarados o Onix, construimos una muestra de 500 usando muestreo estratificado jerárquico por type_main $\times$ strong (representatividad por tipos como Fuego, Agua, Planta, Eléctrico, Hada y Acero, y equilibrio entre fuertes y no fuertes). Con esa base entrenamos varios clasificadores que se comportan como equipos de gimnasio con estilos distintos (KNN que decide por "vecindario" como si comparara con tu cuadrilla de sparring, Regresión Logística que ofrece probabilidades tan claras como un Centro Pokémon bien administrado, Árbol de Decisión que abre caminos como si usara Corte para dividir el bosque, y SVM que busca el mejor margen como un ataque de precisión tipo Rayo). Después los coordinamos con tres formas de votación que simulan estrategias reales de un entrenador (votación dura por mayoría como cuando varios líderes de gimnasio levantan la mano, votación suave promediando probabilidades como una consulta al Alto Mando, y votación ponderada que asigna "MTs" de confianza a quien mejor rinde en validación). La pregunta que guía todo es simple y emocionante: si estuviéramos eligiendo nuestra alineación para desafiar al Campeón, ¿conviene depender de un solo Pikachu carismático o combinar a Charizard, Alakazam y Snorlax para cubrir debilidades, resistencias y estilos de combate?

Entonces el objetivo de este laboratotio es construir un dataset reproducible desde la PokéAPI (CSV canónico con variables visibles y etiqueta strong basada en PowerScore), fijar una muestra de 500 mediante muestreo estratificado jerárquico por type_main × strong (representatividad por tipo y menor varianza), entrenar una familia diversa de clasificadores bajo el mismo pipeline de preprocesamiento (comparabilidad garantizada como si todos aprendieran los mismos movimientos con MT), implementar y explicar tres votadores desde cero (dura, suave y ponderada como tácticas complementarias de entrenador) y, tras compararlos en igualdad de condiciones, generar el archivo de predicciones con el formato oficial para evaluación externa (generalización consistente del ensamble elegido lista para “retar” al Alto Mando).

<p align="center">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/133.png" width="60" alt="Eevee">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/196.png" width="60" alt="Espeon">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/197.png" width="60" alt="Umbreon">
</p>

## *Entrenadores:*

<p align="left">
  <img src="https://img.shields.io/badge/👥%20Equipo-Trainers-8e44ad?style=for-the-badge">
</p>

| Entrenador         | Equipo/Tipo emblema                      | Rol en el equipo                                           | Movimientos clave (Aportes)                                                                                                                                                                             |
| :--------------------------------- | :--------------------------------------- | :--------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| *Abril Minerva Estrada Montaño*  | Rotom (Eléctrico/Truco de datos)         | Maestra de la Pokédex (Adquisición y curación de datos)    | Invoca la PokéAPI para capturar el universo, limpia y normaliza entradas, forja el *CSV canónico, calcula **PowerScore* y etiqueta *strong* sin fugas de información.                             |
| *Erick José Fabián Sandoval*     | Alakazam (Estrategia/Control de muestra) | Arquitecto del Terreno de Batalla (Muestreo y preparación) | Diseña el *muestreo estratificado jerárquico* por *type_main × strong, ajusta cuotas por estrato, codifica **type_main* con coherencia entre splits y deja la muestra de 500 lista para entrenar. |
| *Alanis González Sebastian*      | Metagross (Modelo base/Precisión)        | Líder de Gimnasio de Modelado (Modelado base)              | Entrena y sintoniza *KNN, **Regresión Logística, **Árbol* y *SVM* con el mismo pipeline (imputación/escala/codificación), compara accuracies y documenta estabilidad y trade-offs.              |
| *Melisa Ashareth Arano Bejarano* | Dragonite (Coordinación del equipo)      | Campeona de Ensambles y Reporte (Ensambles y narrativa)    | Implementa *votación dura, **suave* y *ponderada* (pesos por validación), elige el ensamble ganador, arma el *CSV de competencia* con el formato oficial y redacta el informe final.            |

<p>
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/479.png"  width="50" alt="Rotom">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/65.png"   width="50" alt="Alakazam">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/376.png"  width="50" alt="Metagross">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/149.png"  width="50" alt="Dragonite">
</p>

---

<!-- ╔══════════════════════════════════════════════════════════════════════╗ -->
<!-- ║                         PARTE 1 — DATASET                           ║ -->
<!-- ╚══════════════════════════════════════════════════════════════════════╝ -->
<h1 id="parte-1-construcción-del-dataset-descarga-etiqueta-y-muestra-estratificada">
  🗺️💾 <i>Parte 1. Construcción del dataset: descarga, etiqueta y muestra estratificada</i>
</h1>

> 🎒 **Misión del entrenador (Parte 1):** Capturar datos de la PokéAPI, normalizarlos y construir un **CSV canónico** con variables visibles y etiqueta `strong` basada en *PowerScore*.  
> 🗡️ **Pelea Pokémon:** Preparar el campo con una **muestra estratificada** (tipo × strong) de 500 que represente el metajuego.  
> 🧭 **Estrategia:** *Exploración → Limpieza → Etiquetado → Estratificación → Cuotas por estrato.*

<div style="height:8px;background:linear-gradient(90deg,#ff7675,#74b9ff,#55efc4,#ffeaa7);border-radius:8px;margin:10px 0;"></div>

<p align="right">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png" width="48" alt="Bulbasaur">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/4.png" width="48" alt="Charmander">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/7.png" width="48" alt="Squirtle">
</p>

El recorrido arranca como lo haría cualquier entrenador con su Pokédex recién entregada por el Profesor Oak: consultamos sistemáticamente la ruta pública de la PokéAPI (https://pokeapi.co/api/v2/pokemon/\{id\} x), avanzando ID por ID como si exploráramos ruta por ruta hasta cubrir el mapa completo. No capturamos "al azar" ni hacemos una parada temprana en el Safari (evitamos muestras ad-hoc); más bien, registramos cada ejemplar válido con el mismo cuidado con que un Líder de Gimnasio revisa su alineación. Con esos hallazgos consolidamos un CSV canónico donde cada fila es un Pokémon listo para batalla con sus rasgos visibles (height, weight, base_experience, type_main) y sus seis estadísticas base oficiales (hp, attack, defense, special_attack, special_defense, speed) que solo se usan para definir la etiqueta. A partir de esas seis cifras calculamos un power_score como suma directa (como si agregáramos IVs/EVs para juzgar potencial) y establecemos la etiqueta binaria strong con un umbral objetivo en el percentil 75 del universo (equivalente a decir: "este Pokémon está por encima del estándar de la Liga"). Esta decisión evita fugas de información (las estadísticas que fabrican la etiqueta no entran en el vector de entrada) y vuelve la idea de "fuerte" objetiva y reproducible. Para mantener trazabilidad al estilo de una Pokédex bien organizada, el CSV final conserva al menos trece columnas en orden lógico (identificador/nombre, las cuatro visibles, las seis estadísticas, power_score y strong). Además, el pipeline entiende alias razonables de nombres (por ejemplo, "altura" por height o "tipo" por type_main), normalizando encabezados como un Centro Pokémon que deja todo en perfecto estado antes del siguiente combate.

Con el "mapa" completo ya cartografiado, no entrenamos directamente sobre todo el bosque de datos. Para que las métricas no dependan de si el entorno está plagado de Oscuros (y para comparar con justicia entre subpoblaciones), fjamos una muestra de trabajo de 500 Pokémon mediante muestreo estratificado jerárquico en el producto type_main $\times$ strong (primero calculamos power_score y strong en el universo, luego formamos los estratos por combinación de tipo elemental con clase fuerte/no fuerte, y por último asignamos cuotas hasta sumar exactamente 500, ajustando estratos muy pequeños para no perder cobertura). Ese muestreo es como construir un equipo competitivo que respeta resistencias y debilidades por tipo: preserva la diversidad esencial del "metajuego" y evita que un solo arquetipo domine la evaluación. El resultado se materializa en un segundo CSV (por ejemplo, pokemon_samples_500.csv) que funciona como base de modelado. Con este diseño reducimos varianza muestral, impedimos dominancias de tipos mayoritarios y mejoramos la lectura por subpoblaciones (tanto strong = 1 como strong = 0 quedan representados dentro de cada tipo elemental en la medida en que lo permite el universo), lo que nos prepara para retar a la Liga con un análisis que de verdad cubre todas las rutas.

<details>
  <summary>🧺 Sprites de muestra (IDs aleatorios)</summary>
  <p>
    <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/37.png"  width="48" alt="Vulpix">
    <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/92.png"  width="48" alt="Gastly">
    <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/120.png" width="48" alt="Staryu">
    <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/200.png" width="48" alt="Misdreavus">
    <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/304.png" width="48" alt="Aron">
  </p>
</details>

---

<!-- ╔══════════════════════════════════════════════════════════════════════╗ -->
<!-- ║                 PARTE 2 — MODELOS INDIVIDUALES                      ║ -->
<!-- ╚══════════════════════════════════════════════════════════════════════╝ -->
<h1 id="parte-2-modelos-individuales-knn-regresión-logística-árbol-y-svm">
  🤖⚙️ <i>Parte 2. Modelos individuales (KNN, Regresión Logística, Árbol y SVM)</i>
</h1>

> 🎒 **Misión del entrenador (Parte 2):** Entrenar KNN, Logística, Árbol y SVM con el **mismo pipeline** para comparabilidad justa.  
> 🗡️ **Pelea Pokémon:** Elegir el **mejor movimiento** de cada líder (vecindad, probabilidad, cortes, margen) y registrar su desempeño.  
> 🧭 **Estrategia:** *Imputación → Escalado → One-hot → CV estratificada → Métricas y estabilidad.*

<div style="height:8px;background:linear-gradient(90deg,#74b9ff,#a29bfe,#fd79a8);border-radius:8px;margin:10px 0;"></div>

<p>
  <img src="https://img.shields.io/badge/KNN-Vecindarios-0984e3?style=for-the-badge"> 
  <img src="https://img.shields.io/badge/Regresión%20Logística-Probabilidades-00b894?style=for-the-badge"> 
  <img src="https://img.shields.io/badge/Árbol-Decisión-6c5ce7?style=for-the-badge"> 
  <img src="https://img.shields.io/badge/SVM-Margen%20Máximo-d63031?style=for-the-badge">
</p>

<p>
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/16.png"  width="44" alt="Pidgey (KNN)">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/113.png" width="44" alt="Chansey (Logística)">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/185.png" width="44" alt="Sudowoodo (Árbol)">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/26.png"  width="44" alt="Raichu (SVM)">
</p>

Con la muestra estratificada ya lista (como tener el mapa de Kanto desbloqueado), armamos el vector de entrada con las cuatro señales visibles que cualquier Entrenador puede observar a simple vista: height, weight, base_experience y la codificación explícita de type_main (el "tipo" del Pokémon). La variable objetivo es strong. Las estadísticas que sirven para definir esa etiqueta (hp, attack, defense, special_attack, special_defense, speed) y el propio power_score no se usan para entrenar (principio de cero fugas, igual que no mirarías la guía del Alto Mando antes del combate). Dividimos la muestra de 500 en entrenamiento y validación, y dejamos el test externo del profesor completamente ciego hasta el final (como si fuera el combate por la Liga Pokémon).

Entrenamos cuatro familias de clasificadores con estilos de combate complementarios (cada uno a lo "líder de gimnasio"). KNN pelea por vecindad (mira a los "Pokémon del pasto de al lado"), así que necesita buen escalamiento $y$ elegir con cuidado el $k$ que equilibre sesgo y varianza (ni Pidgey 1 vs 1, ni traer a todo el enjambre). Regresión Logística dibuja una frontera lineal y da probabilidades claras (como un Centro Pokémon que te dice exactamente cuánta vida te queda), lo que la vuelve base sólida para la votación suave. Árbol de Decisión abre caminos con Corte y ramifica el bosque en decisiones (captura interacciones sin escala, pero si lo dejas crecer como Hiedra Seca puede sobreajustar, así que controlamos profundidad). SVM busca el máximo margen (un ataque de precisión tipo Rayo), y rinde bien con kernel lineal o RBF siempre que escales y sintonices bien c (y y si usas RBF). Para cada modelo registramos su accuracy de validación y escribimos una lectura cualitativa: cuándo brilla y cuándo se complica (KNN sensible a escala, Logística estable y bien calibrada, Árbol con el clásico trade-off de profundidad, SVM potente pero exigente con hiperparámetros). El objetivo aquí no es coronar a "un Pikachu invencible", sino reunir un elenco diverso que tenga sentido combinar más adelante.

Todos los modelos viajan dentro de pipelines de scikit-learn (como equipar MTs antes del combate): imputación mediana para numéricas, escalamiento estándar cuando corresponde y one-hot para type_main. Así garantizamos que el mismo preprocesamiento se aplique en validación y luego en el test externo (consistencia de gimnasio a gimnasio). De paso hacemos una EDA mínima en consola: balance de clases, correlaciones sencillas entre numéricas y la etiqueta, y tasas de strong por tipo elemental (sirve como mirar la Pokédex por tipo para entender el "metajuego"). Para estimar rendimiento individual usamos validación cruzada estratificada con tres particiones y reportamos media y desviación estándar de accuracy por modelo. Y, para evitar "legendarios prohibidos", mantenemos una lista negra que corta la ejecución si alguien intenta colar AdaBoost, Gradient Boosting, Random Forest, XGBoost o similares (reglas de torneo claras antes de retar al Campeón).

---

<!-- ╔══════════════════════════════════════════════════════════════════════╗ -->
<!-- ║                 PARTE 3 — ENSAMBLES DE VOTACIÓN                     ║ -->
<!-- ╚══════════════════════════════════════════════════════════════════════╝ -->
<h1 id="parte-3-ensambles-de-votación-dura-suave-y-ponderada">
  🏆🤝 <i>Parte 3. Ensambles de votación: dura, suave y ponderada</i>
</h1>

> 🎒 **Misión del entrenador (Parte 3):** Combinar a los líderes (modelos) para reducir varianza y cubrir debilidades: **dura** 🧱, **suave** 💧 y **ponderada** ⚖️.  
> 🗡️ **Pelea Pokémon:** Simular la reunión del Alto Mando: cada voto/probabilidad cuenta según el esquema; elegir el equipo campeón.  
> 🧭 **Estrategia:** *Reentrenar en cada fold → Votar → Medir media±σ de accuracy → Elegir el ensamble más estable.*

<div style="height:8px;background:linear-gradient(90deg,#fdcb6e,#00cec9,#e17055);border-radius:8px;margin:10px 0;"></div>

<p>
  <img src="https://img.shields.io/badge/Dura-🧱%20Mayoría-2d3436?style=for-the-badge">
  <img src="https://img.shields.io/badge/Suave-💧%20Probabilidades-0984e3?style=for-the-badge">
  <img src="https://img.shields.io/badge/Ponderada-⚖️%20Pesos-6ab04c?style=for-the-badge">
</p>

<p>
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/62.png"  width="44" alt="Poliwrath">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/121.png" width="44" alt="Starmie">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/208.png" width="44" alt="Steelix">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/282.png" width="44" alt="Gardevoir">
</p>

Imagina que cada clasificador base es un Líder de Gimnasio con su propio estilo (Roca, Agua, Eléctrico, etc.). Los métodos de ensamble por votación funcionan como una reunión del Alto Mando: se escuchan todas las opiniones y, con un criterio claro, se decide a quién mandamos primero al combate. Formalmente, si tenemos $M$ modelos ${h_1, \ldots, h_M}$ que predicen una etiqueta binaria $y \in\{0,1\}$ para una entrada $x$, la combinación busca una decisión final más robusta que la de cualquier "gym leader" actuando en solitario.

Votación dura (majority voting) es la clásica escena donde varios entrenadores levantan la mano: cada $h_j$ emite una etiqueta $h_j(x) \in\{0,1\}$ y se gana por mayoría simple

$$
\hat{y}= \begin{cases}1, & \text { si } \sum_{j=1}^M h_j(x)>\frac{M}{2} \\ 0, & \text { en otro caso. }\end{cases}
$$

En términos prácticos apilamos las predicciones en una matriz de tamaño $M \times n$ (M modelos por n ejemplos) y marcamos 1 cuando el conteo de "votos a favor" supera $M / 2$. Es tan interpretable como contar medallas, pero no distingue cuán convencido estaba cada líder: un voto de Misty "tibia" pesa igual que uno de Lt. Surge "segurísimo". Si hay modelos mucho más confiables que otros, esta ceguera a la intensidad puede quedarse corta.

Votación suave (soft voting) consulta no solo el "sí/no", sino cuánta confianza reporta cada entrenador. Cada modelo que puede estimar probabilidad entrega $p_j(y=1 \mid x)$ y decidimos por el promedio:

$$
\hat{y}= \begin{cases}1, & \text { si } \frac{1}{M} \sum_{j=1}^M p_j(y=1 \mid x) \geq 0.5 \\ 0, & \text { en otro caso. }\end{cases}
$$

Esto es como pedir el diagnóstico del Centro Pokémon antes de entrar a la Liga: si varios modelos están "moderadamente seguros", esa información se acumula y suele estabilizar el desempeño. En nuestro pipeline solo entran al "panel suave" los clasificadores con predict_proba (por ejemplo, Regresión Logística o LDA), evitando hacks que inventen probabilidades donde no existen.

Votación ponderada (weighted voting) es la versión en la que el Profesor Oak, al revisar nuestros combates de práctica, decide dar más voz a quienes mejor rindieron. Asignamos un peso $w_j$ a cada modelo según su exactitud en validación (y normalizamos para que la suma sea 1), promediando de forma ponderada las probabilidades:

$$
\hat{y}= \begin{cases}1, & \text { si } \frac{\sum_{j=1}^M w_j p_j(y=1 \mid x)}{\sum_{j=1}^M w_j} \geq 0.5 \\ 0, & \text { en otro caso. }\end{cases}
$$

Intuitivamente, es como equipar con MTs clave a los miembros que mejor han performado en cada gimnasio. Si en un fold algún peso "se rompe" (caso límite), recurrimos a repartirlos de manera uniforme como red de seguridad.

El principio que sostiene a los tres votadores es el típico de la sinergia de tipos: si los clasificadores cometen errores de forma no perfectamente correlacionada (uno cubre la debilidad del otro), la combinación reduce la varianza del sistema y mejora la generalización, igual que un equipo con Charizard, Alakazam y Snorlax cubre más amenazas que un Pikachu en solitario. Para comparar con justicia, usamos validación cruzada estratificada con el mismo preprocesamiento y particiones para los tres esquemas: en cada fold reentrenamos los modelos base, instanciamos el votador correspondiente (dura, suave o ponderado) y medimos la accuracy en el subconjunto de validación. Al final reportamos media y desviación estándar por votador, lo que nos da una lectura de estabilidad (si alguno fluctúa demasiado entre folds, se documenta). Con esa evidencia elegimos el ensamble final: el que combina la mayor exactitud validada con la mejor estabilidad, listo para desafiar al campeón sin depender de la suerte del primer turno.

---

#  Estructura del repositorio

PokeLab 7/
├── data/
│   ├── pokemon_samples_500.csv
│    ├── pokemon_full.csv
│   └── pokemon_predictions.csv
├── notebooks/
│   └── ML_Lab7_Snorlax.ipynb
├── docs/
│   ├── Lab_ML_P7.pdf
│    └── Cuestionario.pdf
└── README.md

<p align="center">
  <img src="https://svgur.com/i/12Xo.svg" alt="" width="65%">
</p>

<!-- ───────────────────────────────────────────────────────────────────────────── -->
<!-- 🎲 CURIOSIDADES POKÉ (versión latino, más ganchos)                           -->
<!-- ───────────────────────────────────────────────────────────────────────────── -->
<h2 id="curiosidades-poké">🎲 PokeCuriosidades </h2>

<details>
  <summary><b>👀 Toca para desplegar curiosidades que sí atrapan</b></summary>

- ⚡ **Pikachu**: su nombre mezcla *pika* (sonido de chispa en japonés) y *chu* (chillido de ratón). Literal: “ratón eléctrico”. El branding perfecto desde el nombre.
- 🧪 **Mew**: no estaba planeado. Lo metieron casi al final al liberar espacio de depuración en Rojo/Azul… y terminó provocando la primera gran leyenda urbana de Kanto.
- 🧬 **Ditto**: es el “comodín” de la crianza. Puede reproducirse con casi cualquiera compatible; por eso, si criaste competitivamente alguna vez, seguro usaste un Ditto.
- 🌊 **Wailord**: enorme pero “ligero”. Mide 14.5 m y pesa ~398 kg; su cuerpo esponjoso explica esa densidad rarísima pensada para flotar como dirigible marino.
- 🪄 **Shedinja**: 1 punto de vida y cara de “invencible”. Su habilidad **Wonder Guard** bloquea todo lo que no sea súper eficaz. Si no llevas cobertura, te barre gratis.
- 💾 **MissingNo.**: el glitch más famoso. Un índice fuera de rango en Rojo/Azul que duplicaba objetos y rompía sprites. Ícono de speedruns y de la cultura de bugs.
- 🥢 **Farfetch’d**: viene de un dicho japonés sobre “un pato que trae su propio puerro”, algo tan conveniente que parece puesto para servir… o para comérselo.
- 🧱 **Shuckle**: récord de daño teórico. Con los buffs y objetos correctos puede registrar el golpe más alto posible del juego. Lento, sí; pero matemáticamente letal.
- 🕯️ **Litwick**: guía a la gente… mientras le roba el calor del cuerpo. La línea evolutiva es adorable y al mismo tiempo una de las más siniestras del Dex.
- ⏳ **Yamask**: carga una máscara con su antiguo rostro humano. Cuando la mira, llora. Unova trae de los lores más oscuros de toda la franquicia.
- 🥊 **Primeape**: su furia no termina ni al morir. La Dex menciona que su espíritu sigue enojado; perfecto para esa vibra de “sweep” de enojo perpetuo.
- 🧩 **Porygon**: es software hecho Pokémon. Porygon2 es “actualización estable” y Porygon-Z es “build corrupta”. Ciencia de datos pero con forma de mon.
- 🌟 **Shiny odds**: ver un shiny “a la antigua” era 1/8192; desde Gen VI pasó a 1/4096 (sin amuleto ni cadenas). Aun así, toparte con uno sigue sintiéndose lotería.
- 🎣 **Magikarp**: el meme del débil… que salta montañas pequeñas, según el Dex. Su biografía es una oda al “del 0 al héroe” cuando evoluciona a Gyarados.
- 🧨 **Voltorb**: parece una Poké Ball por algo. El lore sugiere que nació cuando la energía de una Ball se mezcló con un Pokémon. De ahí su diseño “demasiado” simple.

<p>
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png"  width="52" alt="Pikachu">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/151.png" width="52" alt="Mew">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/132.png" width="52" alt="Ditto">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/321.png" width="52" alt="Wailord">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/292.png" width="52" alt="Shedinja">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/0.png"   width="52" alt="MissingNo placeholder">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/83.png"  width="52" alt="Farfetch’d">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/213.png" width="52" alt="Shuckle">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/607.png" width="52" alt="Litwick">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/562.png" width="52" alt="Yamask">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/57.png"  width="52" alt="Primeape">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/137.png" width="52" alt="Porygon">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/129.png" width="52" alt="Magikarp">
  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/100.png" width="52" alt="Voltorb">
</p>

</details>

<p align="right"><a href="#indice">⬆️ Volver al índice</a></p>
