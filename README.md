# TFM-desgaste

# SAM-LoRA — Detección de desgaste en roscas métricas M10×1.5

Módulo del TFM *"Estrategia inteligente para la detección del desgaste en imágenes BLMD"* (Máster en Inteligencia Artificial, UNIR). Implementa un pipeline de segmentación y clasificación de desgaste en herramientas de rosca mediante fine-tuning eficiente de SAM con adaptadores LoRA y una cabeza de segmentación personalizada.

---

## Trabajo relacionado en el grupo TFM

Este módulo forma parte de un proyecto grupal donde cada miembro implementa una estrategia diferente sobre el mismo problema:


Daniel Alcalde Martin Calero — PatchCore (detección de anomalías sin supervisión)

Jordi Peiro Castello — Comparativa multi-modelo (U-Net, MIL)

Miguel Gonzalez Sanchez — SAM + LoRA (Analiza Geometría)

---

## Contexto

Las herramientas de corte de rosca métrica M10×1.5 sufren desgaste progresivo que, si no se detecta a tiempo, compromete la calidad dimensional de la pieza y genera rechazos en línea. Este módulo aborda ese problema desde visión por computador: dada una imagen BLMD de la cresta de la rosca, el sistema segmenta la región de interés, extrae el coeficiente de variación (CV) de esa área y lo contrasta con los parámetros geométricos ISO para emitir un diagnóstico en dos niveles —herramienta operativa o desgastada.

El enfoque técnico se apoya en tres decisiones clave. Primero, usar SAM (ViT-B) como backbone pretrained para no partir de cero con un dataset pequeño. Segundo, congelar los pesos originales y entrenar únicamente los adaptadores LoRA (r=8, alpha=16) en las capas de atención del encoder, lo que reduce drásticamente los parámetros entrenables. Tercero, añadir una cabeza de segmentación propia (`SegHead`) entrenada sobre las máscaras anotadas en Label Studio en formato COCO.


---

## Licencia

Uso académico. El código base de SAM pertenece a Meta AI y se distribuye bajo su licencia Apache 2.0 original.
