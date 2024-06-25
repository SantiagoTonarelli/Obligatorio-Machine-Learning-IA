#TODO: borrar esto una vez resultas las preguntas.

## Dudas a consultar

Para el preprocesamiento y extraccion de features, esta bien usar lo del lab 2 no? Esa parte no requiere diferentes implementaciones, podemos usar la funcion para extraer las Haar features existente.

<br>

Para los Clasificadores, tenemos que implementar todos los mencionados? Lo mismo del lab 2 pero agregando el resto de los clasificadores?

<br>

Luego de implementarlos, se espera que los entrenemos en paralelo para compararlos y elegir el mejor? Eso ya seria la Evaluacion y Seleccion, no? Se espera que usemos las tres tecnicas?

<br>

Para las tablas, entonces tenemos que crear una por cada clasificador que implementamos, sin importar si es el que elegimos? Y tienen que reflejarse las metricas en graficas por ejemplo?

<br>

Para resumir, primero creamos los clasificadores y despues los entrenamos y hacemos las predicciones con el set de datos de test. Luego aplicamos las tecnicas Holdout, etc nuevamente para ver si mejora la prediccion inicial. Luego usamos las metricas para evaluar cual consideramos mejor para elegir como modelo final. Esto es correcto?

<br>

Archivos de Aulas? Kaggle?


# Notas clase:
- Lo mas importante es el diario de experimentacion.
- Que este todo visible, lo que salio mal y bien.
- Fundamentacion de modelo: "me quedo con este modelo porque..." Justificar por que elegimos X modelo como el mejor. Como lo entrene, le tengo mas confianza, no tiene porque ser el que fue mejor. 
- No es relevante probar con muchos datos, pero si explorar las caracteristicas.
- Seleccionar features con AdaBoost es mejor porque hay interacciones entre features. En cambio el SelectPercentile es cada una con el target (igual no es que este mal).
- Probar con el detector del astronauta.
- Metodologia. Resultados bien ordenados. Entender el paso a paso. Conclusiones.
- El unico tiempo relevante podria ser el de prediccion. Pero es una etapa posterior. Empezar a optimizar luego de que funcione.
- Al cv se le puede pasar un split. Shuffle_splitter es un splitter en que podemos hacer una division en train y test y eso se lo podemos pasar a cross-validation. Ej: lab de pinguinos en Aulas.
- Para el Gradient Boosting conviene fijar el lr o estimators porque dependen. Igual puede que sea de los que demoren mas. En ese caso conviene hacer una busqueda con menos datos y buscar los hiperparametros y despues afinar con mas datos. Si algunos hiperparametros no cambian, se pueden quitar.
- SGClassifier - regresion logistica con estocastic descent.
- El dataset test del lab 2 es dificil, por lo que las metricas pueden dar mal en general. El otro dataset tiene unas 8.000 imgs para testear en Kaggle. 
- Tip: Una cascada de 2 pasos mejora mucho el false-positive rate.
- Para Kaggle se tiene que subir el ID (numero en el nombre del archivo) y la prediccion. Ver ej notebook de Aulas.

<br>

# IMPORTANTE:
- Check notebook de ejemplo (estan en este repo dentro de */examples*).

<br>

## Seudo-codigo para implementar el algoritmo de cascada
```
def cascada(lista_modelos, dato):
    prediction = 1 # Es rostro.
    for modelo in lista_modelos:
        if modelo.predict(dato) == 0: # Si hay un modelo que lo rechaza, paro.
            prediction = 0 # No es rostro.
            break
    return prediction
```

<br>

- Datos T.
- M1 = AdaBoost(n1) n1 = 5
- T1 = [M1.predict(T) = 1]
- M2 = AdaBoost(n2) n2 = 10

Lo ideal seria poder tomar otra muestra de datos independientes, tomar los que sobreviven y entrenar el 2do con esos.
El primero es un filtro que es importante para el train del 2do.
