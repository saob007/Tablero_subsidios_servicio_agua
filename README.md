# Informe Visual y Tablero de Análisis de Subsidios, Consumo y Facturación del Servicio de Agua en Sincelejo (2020).

## Resumen

El objetivo de este proyecto fue diseñar e implementar un informe visual para analizar la cobertura, consumo, facturación y subsidios del servicio de agua potable y alcantarillado en Sincelejo durante el año 2020. Para ello, se desarrolló un tablero de control estático en Looker Studio, basado en datos públicos proporcionados por la Secretaría de Planeación de la Alcaldía Municipal.

El conjunto de datos utilizado contiene información detallada sobre los servicios contratados, las mediciones del consumo de agua, los valores facturados a los usuarios y el respaldo económico otorgado por la alcaldía mediante subsidios. Dado que la base de datos solo abarca el año 2020, el tablero se diseñó como un informe estático sin análisis temporal dinámico.

El tablero diseñado en este proyecto facilita la visualización de patrones clave en el acceso y uso del servicio, permitiendo identificar la distribución del consumo según zonas geográficas, la proporción de usuarios con servicio activo o inactivo, así como el impacto de los subsidios según estratos socioeconómicos. Entre los principales hallazgos se destaca que la mayoría de los subsidios se concentran en los estratos más bajos, asegurando acceso al servicio a poblaciones vulnerables, mientras que el consumo de agua presenta variaciones significativas entre distintas zonas de la ciudad. Este informe visual proporciona una herramienta de análisis accesible y estructurada para evaluar la eficiencia en la distribución de los recursos y el impacto del subsidio en la comunidad, contribuyendo a una mejor toma de decisiones en la gestión del servicio de agua potable y alcantarillado.


## Entendimiento de la problemática del negocio

La Secretaría de Planeación de la Alcaldía Municipal de Sincelejo, como entidad responsable de la gestión de subsidios para el servicio de agua potable y alcantarillado, dispone de datos públicos sobre la cobertura del servicio, consumo de agua, facturación y apoyo financiero otorgado a los usuarios. Esta información, publicada dentro del marco de transparencia y acceso a datos abiertos, constituye la base de este proyecto.

El análisis busca comprender la distribución de los subsidios, la relación entre consumo y facturación, así como el impacto del respaldo económico en los distintos estratos socioeconómicos de la ciudad. A través del tablero de control visual, se facilita la identificación de patrones clave en el uso del servicio y la eficiencia en la asignación de los subsidios, proporcionando información relevante para la toma de decisiones en la planeación y sostenibilidad del sistema de agua en Sincelejo.

## Entendimiento de los datos

El conjunto de datos proporcionado para acceso público contiene registros detallados sobre los subsidios otorgados al servicio de agua potable y alcantarillado en Sincelejo durante el año 2020, que esta comprendido por 19.999 registros y 33 campos (características). Estos campos recopilan información de identificación única de viviendas y establecimientos beneficiados, con variables clave como el tipo de servicio contratado (acueducto y/o alcantarillado), la zona de presión del suministro, el estado del servicio (activo o inactivo), el estrato socioeconómico del usuario, el consumo medido en metros cúbicos, el valor facturado, el monto subsidiado y el porcentaje de cobertura del subsidio según el consumo.

La Figura 1 muestra la distribución de los registros del año 2020 en función de la estratificación social.

**Figura 1. Distribución de los registros por estratos socioecnómicos**
<p align="center">
    <img src="assets/img/img1.png" alt="Distribución de los registros" width="700">
</p>
Se observa que la mayor parte de los subsidios se concentran en los estratos más bajos, con un 49.84% en el estrato 1 y un 28.68% en el estrato 2. A medida que aumenta el nivel socioeconómico, la proporción de subsidios disminuye significativamente, con menos del 1% en los estratos 5 y 6. Esto indica que el programa de subsidios está focalizado en los sectores más vulnerables, alineándose con políticas de equidad social para garantizar el acceso a los servicios básicos a quienes más lo necesitan.

***NOTA:*** Como parte de la preparación de datos, se eliminaron columnas innecesarias, se verificaron valores nulos y registros duplicados y se realizó un formateo de algunas variables al tipo de dato correcto.

## Modelado y Evaluación

Con base en el análisis exploratorio de datos y el estudio de las correlaciones entre variables, se formuló antes del modelado analítico, el supuesto inicial de baja predictibilidad de las características operativas de los fondos sobre su rentabilidad mensual. El gráfico de calor a continuación, muestra la importancia de las características del modelo Random Forest.

**Figura 3. Correlación de las variables**
<p align="center">
    <img src="assets/img/img4.png" alt="Importancia de las características" width="700">
</p>

A pesar de haber identificada la poca existencia de correlaciones entre la rentabilidad mensual y las variables predictoras, se demostró que la hipótesis de que ningun modelo podría ajustarse correctamente a los datos para realizar predicciones aceptables, era parcialmente incorrecta una vez se probaron los algortimos de modelado. Aunque las variables operativas tengan muy baja correlación individual con la rentabilidad mensual de los FIC, el modelo de Random Forest logró modelar relaciones complejas entre estas variables y el objetivo. Esto sugiere que hay información útil en las variables, aunque no sea obvia con modelos simples como los de regresión lineal.

Se seleccionó un modelo de bosques aleatorios (Random Forest) como opción ganadora, el cual se encuentra compuesto por 100 árboles de decisión para determinar el peso de incidencia de cada carcaterística operativa sobre la rentabilidad mensual de los FIC. El gráfico a continuación muestra que el valor unitario de las operaciones de inversión (valor_unidad_operaciones), el valor del cierre diario del fondo (valor_fondo_cierre_dia_t) y la cantidad de proyectos en los que ha participado (numero_proyectos) contityen los dos factores cláves al momento de determinar la rentabilidad mensual, con un peso conjunto de más del 60% de incidencia. 

El gráfico de barras horizontales muestra la importancia de las características del modelo Random Forest.

**Figura 4. Importancia de las variables en el modelo Random Forest**
<p align="center">
    <img src="assets/img/img3.png" alt="Importancia de las características" width="700">
</p>

En cuanto al desempeño, el modelo explicó aproximadamente el 84.73% de (R2) la variabilidad de la rentabilidad, indicado que tiene un buen desempeño. Por otro lado, en promedio, las predicciones del modelo tienen un error de ±29.62% de la rentabilidad (MSE = 0.087763 equivalente a RMSE = 0.2962). Aunque el R2 es alto, un error promedio (RMSE) de aproximadamente 29.62% puede ser significativo en el contexto de rentabilidad, ya que podría hacer que las predicciones sean imprecisas en escenarios donde se necesitan estimaciones más ajustadas. Por lo tanto, en fúturos proyectos internos de creación de horizontes financieros no es recomedable la utilización de un modelo analítico basado solamente en variables operativas


## Conclusión

- Los fondos de inversión colectiva (FIC) de tipo general tienen, por mucho, el mayor número de registros operativos. Este segmento es claramente el más activo dentro del mercado en el año 2024.
-  Los FIC de mercado monetario, inmobiliarios y bursátiles parecen estar infrautilizados o tener una base de clientes más reducida. Esto resulta en una oportunidad para las administradoras que busquen diversificar su oferta o atraer nuevos inversionistas.
-  Las sociedades fiduciarias parecen ofrecer mayor estabilidad y consistencia en los retornos mensuales, lo que podría ser atractivo para inversores conservadores.
-  Los comisionistas de bolsa reflejan un perfil más arriesgado, con mayores posibilidades de obtener altos retornos, pero también con un mayor riesgo de pérdidas significativas.
- La falta de correlación significativa en el análisis inicial no implicó ausencia de información útil en las variables. Random Forest, al ser un modelo no lineal y basado en árboles, pudo detectar interacciones complejas y patrones no evidentes en los datos.
- Se realizaron segundas validaciones cruzadas sobre el modelo ganador Random Forest para verificar que el desempeño aceptable sobre los datos de prueba no se debiese a simple azar, se encontró que incluso con 10 subjconjunto de pruebas cruzadas, el modelo siguió desempeñandose muy bien con un R2 medio de 0.847 y un MSE de 0.087 siendo incluiso ligeramente superior al primer modelo Random Forest desarrollado. En este sentido, se confirma que el modelo Random Forest es el que mejor se ajustó correctamente a los datos y se escogió como base para estudiar el peso de las variables predictoras sobre la rentabilidad mensual. No obstante, en futuras investigaciones, se debe analizar un poco más a fondo si puede llegar a existir un sobre ajuste díficil de detectar con solo realizar validaciones cruzadas.
- En escenarios fúturos de investigación se recomienda utilizar técnicas adicionales como SHAP o LIME para entender cómo las variables más importantes (como valor_unidad_operaciones, valor_fondo_cierre_dia_t) están influyendo en las predicciones. Esto puede dar insights adicionales sobre las relaciones subyacente. Si es posible, añadir más variables operativas o del contexto macroeconómico donde se ven envueltos los FIC para estudiar si es posible mejorar aún más el modelo.
