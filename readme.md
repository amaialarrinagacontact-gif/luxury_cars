Luxury Sports Cars SQL Analysis
Descripción del proyecto#

Este proyecto analiza un dataset de coches deportivos de lujo mediante SQL, utilizando un modelo de datos estructurado en capas con el objetivo de transformar datos en bruto en información accionable para la toma de decisiones.

El enfoque del proyecto no es únicamente técnico, sino también analítico: se busca entender cómo se posicionan las marcas dentro del mercado, qué variables influyen en su estrategia y cómo se diferencian en términos de precio, rendimiento y variedad de producto.

Pipeline de datos:

CSV → Staging → Core → Semantic → Analytics

El proyecto ha sido desarrollado utilizando PostgreSQL y se organiza en tres capas principales:

Staging: datos originales importados desde CSV
Core: modelo relacional normalizado con tipado correcto, claves limpias e integridad referencial
Semantic: vistas de negocio diseñadas para facilitar el análisis y reducir la complejidad técnica
Entorno e instalación

El proyecto se ha desarrollado utilizando PostgreSQL.

Descarga oficial:
https://www.postgresql.org/download/

Durante la instalación se incluyeron:

PostgreSQL Server
pgAdmin 4

Configuración utilizada:

Usuario: postgres
Base de datos: luxury_cars

Todas las consultas y transformaciones se ejecutaron desde pgAdmin 4.

Instrucciones de reproducción
Crear la base de datos:
CREATE DATABASE luxury_cars;
Importar el dataset Sport_car_price.csv en la tabla staging_cars.
Ejecutar el pipeline completo:
\i project.sql

Este script ejecuta de forma secuencial:

staging
core
semantic
analysis

Garantizando la reproducibilidad completa del proyecto.

Fuente de los datos

Dataset público obtenido de Kaggle con información sobre coches deportivos de lujo.

Incluye fabricantes como:

Ferrari
Lamborghini
Porsche
Audi
McLaren
Aston Martin
Bentley

Modelo de datos
Staging Layer

Tabla: staging_cars

Contiene los datos originales sin transformar.

Columnas:

make
model
year
engine_size
horsepower
torque
acceleration
price

Core Layer

Modelo relacional normalizado:

brands (dimensión)
cars (entidad principal)
prices (medidas económicas)

Relación:

brands → cars → prices

Principales características:

Eliminación de duplicados
Tipado correcto de datos (NUMERIC, INT)
Claves foráneas para integridad referencial
Limpieza aplicada en el momento de carga
Semantic Layer

Vistas orientadas a negocio:

vw_avg_price_by_brand
vw_brand_performance_summary
vw_most_powerful_cars
vw_brand_positioning

Estas vistas abstraen el modelo técnico y permiten realizar análisis directamente sobre métricas de negocio.

Calidad de datos

Durante el análisis se detectaron problemas en el dataset original:

Precios con formato incorrecto
Ejemplo: 101,200

Solución: eliminación de comas y conversión a NUMERIC

Potencia con símbolos
Ejemplo: 1000+

Solución: eliminación del símbolo y conversión a INT

Tipos de datos inconsistentes

Los valores numéricos estaban almacenados como texto.

Solución:

Conversión en la capa core
Uso de funciones como REPLACE y CAST durante la carga

Además, se realizaron controles de calidad para detectar:

valores nulos
duplicados
inconsistencias de formato

Uso de SQL avanzado

El proyecto incluye el uso de funciones personalizadas en PostgreSQL para encapsular lógica de limpieza de datos, así como CTEs, window functions y subqueries para análisis avanzados.
Preguntas de negocio


El proyecto se centra en responder preguntas relevantes para entender el mercado de coches deportivos de lujo:

¿Qué marcas lideran en precio medio?
¿Qué marcas destacan en potencia y rendimiento?
¿Existe relación entre precio y potencia?
¿Qué marcas apuestan por volumen frente a exclusividad?
¿Cómo evoluciona el precio medio a lo largo del tiempo?
¿Qué modelos se sitúan en el segmento más extremo del mercado?
¿Qué diferencias existen dentro de cada marca en términos de rendimiento?
¿Qué marcas presentan mayor diversidad de producto?
¿Cómo se distribuye el posicionamiento competitivo entre marcas?
¿Qué marcas combinan alto precio y alto rendimiento?
Resultados del análisis

El análisis permite identificar patrones clave en el mercado:

Porsche y Audi presentan mayor variedad de modelos, lo que sugiere una estrategia basada en volumen y diversificación
Ferrari, Lamborghini y McLaren lideran en potencia, posicionándose en el segmento de alto rendimiento
Existe una tendencia creciente en el precio medio en modelos más recientes
El segmento de mayor precio está dominado por marcas de superdeportivos
Algunas marcas muestran coherencia entre precio y potencia, mientras que otras presentan posicionamientos más híbridos
Pregunta de negocio principal

¿Cómo se posiciona Maserati dentro del mercado de coches deportivos de lujo?

Respuesta

El análisis muestra que Maserati ocupa una posición intermedia:

No lidera en precio frente a Ferrari o Lamborghini
No destaca en potencia frente a marcas de alto rendimiento
Presenta menor variedad de modelos que marcas como Porsche

Esto indica que no compite directamente ni en el segmento más exclusivo ni en el de mayor volumen.

Conclusión estratégica

Maserati se sitúa entre:

marcas de alto rendimiento (superdeportivos)
marcas premium con mayor volumen

Este posicionamiento híbrido puede dificultar su diferenciación en el mercado, al no dominar ninguna de las dos estrategias principales.

Conclusiones generales

Este proyecto demuestra:

La capacidad de transformar datos en bruto en un modelo estructurado y analítico
El uso de SQL para generar insights de negocio relevantes
La importancia del modelado de datos en la calidad del análisis

El mercado de coches deportivos presenta dos estrategias dominantes:

Exclusividad y alto rendimiento
Diversificación y volumen

Las marcas se posicionan a lo largo de este eje en función de su propuesta de valor.

Estructura del proyecto
SPORTCAR_SQL/
│
├── analysis/
├── core/
├── semantic/
├── staging/
├── project.sql
├── README.md
├── Sport_car_price.csv

Data Quality Checklist
Validación de valores nulos en columnas clave
Detección y análisis de duplicados por marca y modelo
Conversión de tipos de datos (TEXT → NUMERIC / INT)
Limpieza de formatos en precios y potencia
Verificación de integridad referencial entre tablas
Control de consistencia en joins entre capas
Autora

Amaia Gil