![](./images/itam_logo.png)

M. Sc. Liliana Millán Núñez liliana.millan@itam.mx

Abril 2021

## Proyecto 1

### Contexto

En el [dropbox](https://www.dropbox.com/s/ky7ls87ymi5xx15/WA_Fn-UseC_-Telco-Customer-Churn.csv?dl=0) se encuentran los datos de empresas de telecomunicaciones con características de sus clientes.

Cada renglón representa a un cliente y cada cliente tiene la siguiente información.

* Clientes que abandonaron a la compañía -*churn*-
* Servicios que cada cliente solicitó: teléfono, múltiples líneas, internet, seguridad online, respaldo online, protección de dispositivo, soporte técnico, TV streaming, películas.
* Información de la cuenta del cliente: Por cuánto tiempo ha sido cliente, tipo de contrato, método de pago, estado de cuenta paperless, cargos mensuales, total de cargos.
* Información demográfica de los clientes: género, rango de edad, si tienen pareja y dependientes.

Una Telco te ha contratado para que realices un modelo para predecir si un cliente hará *churn* o no (abandono). Además, te indica que el modelo no puede tener más de 2% de errores de acuerdo a la etiqueta positiva.

+ Convierte los nombres de columnas a minúsculas

### Preguntas

1. ¿Cuál es la variable target?
* Cuál es la etiqueta positiva
* Qué es TP, TN, FP y FN
* En qué debemos optimizar: minimizar FP o minimizar FN, explica.
* Qué métrica de desempeño deberás optimizar para cumplir con el punto anterior, explica.

-> En caso de haber nulos/vacíos elimina esos registros.

2. Genera el *data profiling* de las variables `totalcharges` y la variable `contract` interpreta la salida.

3. Genera un EDA con 4 gráficas. Recuerda que los detalles son importantes.
* Gráfica de barras horizontales con la proporción de `churn` y no churn. Explica.
* Boxplot con la distribución de la variable `totalcharges` por `contract` y `churn`, incluye la media. Explica. El color debe ser la variable `churn`.
* Boxplot con la distribución de la variable `monthlycharges` por `contract` y `churn`, incluye la media. Explica. El color debe ser la variable `churn`.
* FacetGrid con boxplot con la distribución de la variable `monthlycharges` por `paymentmethod` y `churn`, incluye la media. Explica. Las columnas deben ser la variable `paymentmethod`.

### Preprocesamiento
  + Cambia las variables `gender`, `seniorcitizen`, `partner`, `phoneservice`, `paperlessbilling` y `churn` a variables binarias con valor posible 0 para el caso `No` y 1 para el caso `Yes`.
  + Transforma las variables a una codificación de one hot encoding: `multiplelines`, `internetservice`, `onlinesecurity`, `onlinebackup`, `deviceprotection`, `techsupport`, `streamingtv`, `streamingmovies`, `contract`, `paymentmethod`.

### Modelado

+ Utiliza un `random.seed` `210418`
+ Utiliza el 25% de los datos para prueba
+ Utiliza un árbol para seleccionar las variables que aportan mayor información a la predicción.
  + Utiliza un `random_state` `5432`
  + Utiliza los siguientes hiperparámetros:
    + Profundidad: 5, 7, 11
    + Definición de hoja: 7, 9, 11, 13
    + Ganancia de información: gini y entropía
    + Cross validation: 5
  + Dados estos hiperparámetros ¿cuántos modelos generarás?
  + ¿Cuáles son las 3 variables que aportan más información? ¿Qué porcentaje tiene cada una?
+ Elimina de tu set de variables las que aportan menos del 1% de información y ahora realiza un Random Forest con los siguientes hiperparámetros -no vuelvas a generar un X_train, X_test split ya que estarías generando data leakage- ¿por qué?
  + Utiliza un `random_state` de `7654`
  + Profundidad: 11, 13, 15
  + Número de árboles: 500, 800, 1000
  + Definición de hoja: 11, 13
  + Ganancia de información: gini y entropía
  + Cross validation: 5
+ Dados estos hiperparámetros ¿cuántos modelos generarás?
+ Del mejor modelo ¿cuál es la variable raíz? ¿cuánto aporta de información? Explica.
+ ¿Cuáles son los hiperparámetros del mejor modelo?
+ Genera la curva ROC, cuánto tiene de AUC? Interpreta.
+ Genera la curva Precision-Recall, ¿cuánto `recall` tienes para un `precision` de 70%? Interpreta.
+ Genera la tabla de métricas de desempeño
  + ¿Qué punto de corte cumple con las restricciones de negocio? A 6 decimales. Interpreta.
  + ¿Qué porcentaje de `recall` tienes en ese punto? Explica.
  + ¿Qué porcentaje de `precision` tienes en ese punto? Explica.
+ Genera la matriz de confusión asociada a este punto de corte. Explica.

### ¿Qué se entrega?

* Jupyter notebook con el código y explicación
* Entregar por correo a liliana.millan@itam.mx a más tardar el **3 de mayo del 2021** a más tardar a las **23:59:59 CST** con el título `proyecto_1_md` en su correo copiar a su compañero de equipo. Solo envía un miembro del equipo.

En esta ocasión, si el proyecto se entrega después de la fecha y hora, se considera que no se entregó, por lo que la calificación es 0.

-> Si tienes dudas sobre cómo hacer OneHotEncoding, ve a la última parte del notebook `knn.ipynb`.

**Equipos**

![](./images/equipos_p1.png)
