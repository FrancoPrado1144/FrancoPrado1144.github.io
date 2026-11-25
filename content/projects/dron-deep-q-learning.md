+++
title = "Dron autónomo con Deep Q-Learning"
date = "2026-11-20"
description = "Un dron simulado en PyBullet que aprende con aprendizaje por refuerzo profundo a moverse entre edificios y perseguir a otro dron, evaluado en un modelo 3D de Nueva Córdoba con árboles y viento."
# github = "https://github.com/FrancoPrado1144/..."   # completar cuando el repo sea público
tags = ["python", "pytorch", "reinforcement-learning", "dqn", "pybullet"]
categories = ["inteligencia-artificial"]
featured = true
+++

Proyecto grupal de la facultad: entrenamos un dron en una simulación física para que aprenda a moverse entre edificios y perseguir a otro dron (el "señuelo"), sin reglas programadas a mano. El comportamiento surge del aprendizaje por refuerzo.

<video autoplay loop muted playsinline controls preload="metadata" poster="/images/projects/dron-nueva-cordoba-poster.jpg" style="width:100%;border-radius:12px;">
  <source src="/videos/dron-nueva-cordoba.mp4" type="video/mp4">
</video>

*Evaluación final en Nueva Córdoba, con cuatro cámaras: primer plano, vista cenital, vista en ángulo y primera persona. El dron azul se acerca al señuelo amarillo hasta mantenerse a menos de 0,30 m durante 10 segundos seguidos.*

## El problema

En cada paso de la simulación, el dron tiene que decidir hacia dónde moverse para esquivar edificios, mantenerse estable y alcanzar al objetivo. Escribir esas reglas a mano es muy difícil, así que planteamos el problema como un entorno de aprendizaje por refuerzo: el agente prueba acciones y recibe recompensas según qué tan bien cumple la tarea.

## El modelo

El agente es una red Q, un perceptrón multicapa en PyTorch. Recibe 88 valores que describen la situación del dron (su estado, sus sensores de distancia y dónde está el objetivo) y devuelve un valor por cada una de las 7 acciones posibles. En cada paso, el dron ejecuta la acción con el valor más alto.

![Esquema de la red neuronal: 88 entradas, dos capas ocultas de 128 neuronas y 7 salidas](/images/projects/dron-red-neuronal.svg)

## Cómo aprende

Usamos **Double DQN**, con memoria de repetición y red objetivo. El dron junta experiencia volando, la guarda en una memoria y aprende de lotes de experiencias tomadas al azar. Al principio explora casi siempre al azar y, a medida que aprende, aprovecha cada vez más lo que ya sabe.

![Ciclo de entrenamiento: observar, elegir acción, simular, recompensa, guardar y aprender](/images/projects/dron-ciclo-entrenamiento.svg)

El modelo final (la corrida 29) es el resultado de una serie de experimentos documentados en una bitácora. Fuimos ajustando la recompensa (por ejemplo, medir la distancia rodeando los edificios en lugar de en línea recta), los sensores (sumamos rayos inclinados para detectar bordes de azoteas) y los hiperparámetros de entrenamiento.

## Resultados

Una vez entrenado, el modelo se evaluó sin volver a entrenarlo, siguiendo a un señuelo que se mueve por las calles:

- **En la ciudad de entrenamiento:** siguió al señuelo con éxito en el **73 % de 100 escenarios** fijos y reproducibles.
- **En Nueva Córdoba:** un sector real alrededor de Plaza España, modelado por el equipo a escala 1:30, con árboles contra los que se puede chocar y viento con ráfagas. Ahí el dron nunca había volado y logró el seguimiento en **10 de 30 escenarios (33 %)**. La caída muestra cuánto pesan el viento, los árboles y las calles irregulares, y marca por dónde seguir mejorando el modelo.

## Lo que aprendí

- A diseñar funciones de recompensa y a iterar sobre ellas comparando corridas de entrenamiento.
- A llevar una bitácora de experimentos para saber qué cambió de una corrida a otra.
- A evaluar con conjuntos de escenarios fijos e intervalos de confianza, y no con un solo episodio que salió bien.
- A generar videos de evaluación desde varias cámaras para entender el comportamiento del agente.

## Tecnologías

Python · PyTorch · PyBullet (gym-pybullet-drones) · NumPy · Pandas · Jupyter Notebook
