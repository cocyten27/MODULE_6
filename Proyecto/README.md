Conteo de Vegetación con IA — Proyecto Final Módulo 6
Dr. Francisco J. Rodríguez

Integrantes del equipo:

Héctor Hugo Domínguez Jaime
Sergio Raúl Bonilla Alejo
César Geovanni Machuca Pereida
Proyecto final del Módulo 6: pipeline de visión por computadora para contar plantas en parcelas agrícolas a partir de fotos de dron o celular. El objetivo del sistema es estimar la densidad de vegetación (especialmente en etapas de emergencia, donde las plantas son pequeñas y dispersas), primero con procesamiento clásico de color y, en fases posteriores, con un modelo entrenado.

Este README está escrito para que una IA o una persona pueda entender el proyecto y continuar el trabajo sin re-descubrir nada. Léelo completo antes de modificar código.

El pipeline completo tiene 4 fases:

Fase 1 (hecha)        Fase 2 (hecha)              Fase 2–3 (proceso)          Fase 3 (proceso)
Fotos de dron     ->  Cortar en tiles          ->  Dataset YOLO (por vuelo) -> Conteo con el modelo
conteo clásico        descartar tiles vacíos       entrenar YOLO26 + val     entrenado (infer.py)
por color             generar manifest.csv         mAP
Fase	Script / archivo	Qué hace
1	conteo_vegetacion.html	Prototipo 100% navegador: conteo clásico por color (Excess Green Index) + componentes conexas
2	tile_pipeline.py	Corta fotos grandes en tiles etiquetables y descarta tiles de suelo vacío
2–3	convert_polygon_to_bbox.py	Convierte etiquetas de polígono (Roboflow) a cajas YOLO
2–3	prepare_dataset.py	Arma el dataset YOLO (split train/valid por vuelo + data.yaml)
2–3	train.py	Entrena un modelo YOLO26 sobre el dataset y reporta mAP
3	infer.py	Cuenta plantas en fotos nuevas con el modelo entrenado (dedup por IoU global)
