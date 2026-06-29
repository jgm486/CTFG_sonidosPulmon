# # CTFG - Clasificación de enfermedades respiratorias con deep learning

Complemento al Trabajo Fin de Grado (CTFG) del Grado en Ingeniería Informática de
la Universidad de Almería. Continúa un TFG previo sobre clasificación multiclase
de seis enfermedades respiratorias a partir de sonidos pulmonares, aplicando ahora
aprendizaje profundo (MLP, LSTM y GRU) y comparándolo con el mejor modelo clásico
del trabajo anterior (SVM con núcleo RBF), bajo el mismo protocolo de validación
cruzada por paciente.

**Autor:** José Miguel García Martín
**Directoras:** Gracia Ester Martín Garzón y Gloria Ortega López

## Resumen del trabajo

Se entrenan y evalúan tres modelos de aprendizaje profundo sobre un subconjunto
balanceado de 60 pacientes (10 por clase), con validación cruzada por paciente de
10 folds fijos:

- **MLP** sobre las 41 características acústicas agregadas del TFG (referencia).
- **LSTM** sobre los coeficientes MFCC dispuestos como secuencia temporal.
- **GRU** sobre la misma representación secuencial.

El resultado principal es que el aprendizaje profundo no mejora al enfoque clásico
en este problema: el MLP se acerca a la SVM-RBF pero queda por debajo, y las redes
recurrentes rinden peor, con un sesgo de predicción hacia la clase Heart Failure.
La aportación del trabajo es una comparación controlada y honesta, no una cifra
más alta.

## Estructura del repositorio

| Archivo | Descripción |
|---|---|
| `notebooks/extraer_mfcc_secuencia.ipynb` | Extrae la matriz de 13 coeficientes MFCC por ventana y genera el tensor de secuencias. |
| `notebooks/entrenar_modelos.ipynb` | Entrena y evalúa los tres modelos con validación por paciente y agregación por voto mayoritario. |

## Datos

El trabajo utiliza dos bases de datos públicas, que **no se incluyen** en este
repositorio. Para reproducir los experimentos hay que descargarlas de sus fuentes
oficiales:

- **ICBHI Respiratory Sound Database:** https://bhichallenge.med.auth.gr/
- **Fraiwan et al. (Mendeley Data):** https://data.mendeley.com/datasets/jwyy9np4gv/3

## Requisitos

- Python 3.10 o superior
- Jupyter (Notebook o JupyterLab)
- Bibliotecas principales: TensorFlow/Keras, NumPy, librosa, scikit-learn

Instalación de dependencias:

```
pip install tensorflow numpy librosa scikit-learn jupyterlab
```

## Uso

1. Descargar y colocar los datos según se indica en la sección anterior.
2. Abrir los cuadernos con Jupyter y ejecutar las celdas en orden:
   - Primero `extraer_mfcc_secuencia.ipynb`, que genera la representación
     secuencial de MFCC a partir del audio.
   - Después `entrenar_modelos.ipynb`, que entrena los tres modelos y produce las
     métricas y las matrices de confusión.

Las semillas están fijadas a 42 para garantizar la reproducibilidad.
