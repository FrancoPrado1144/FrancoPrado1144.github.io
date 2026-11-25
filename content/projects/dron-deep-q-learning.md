+++
title = "Dron autónomo con Deep Q-Learning"
date = "2026-11-01"
description = "Un dron simulado en PyBullet que aprende, con aprendizaje por refuerzo profundo, a moverse por una ciudad y perseguir un objetivo en movimiento."
# github = "https://github.com/FrancoPrado1144/..."   # completar cuando el repo sea público
tags = ["python", "deep-learning", "reinforcement-learning", "dqn", "pybullet"]
categories = ["inteligencia-artificial"]
featured = true
+++

Proyecto grupal de la facultad en el que entrenamos un dron dentro de una simulación física para que aprenda a desplazarse por un entorno urbano y a seguir un objetivo móvil, sin reglas programadas a mano: el comportamiento surge del aprendizaje por refuerzo.

## El problema

El dron tiene que tomar decisiones de movimiento en cada paso de la simulación: esquivar edificios, mantenerse estable y acercarse al objetivo. Definir esas reglas a mano es difícil, así que planteamos el problema como un entorno de aprendizaje por refuerzo, en el que el agente recibe recompensas según lo bien que cumple la tarea.

## Cómo lo resolvimos

- **Simulación:** usamos PyBullet para modelar el dron y una ciudad con edificios como obstáculos.
- **Agente:** implementamos Deep Q-Learning (DQN), donde una red neuronal estima el valor de cada acción posible según el estado del dron y del entorno.
- **Etapa 1, navegación:** el dron aprende a moverse por la ciudad hasta un punto de destino.
- **Etapa 2, persecución:** el objetivo pasa a ser un señuelo en movimiento y el dron tiene que seguirlo.
- **Evaluación en un mapa real:** probamos el modelo en un mapa de Nueva Córdoba modelado por el equipo, más grande y detallado que el entorno de entrenamiento.

## Lo que aprendí

- A diseñar funciones de recompensa y a iterar sobre ellas comparando corridas de entrenamiento.
- A llevar una bitácora de experimentos para saber qué cambió entre una corrida y otra.
- A generar videos de evaluación desde varias cámaras (vista superior, 3/4 y primera persona) para analizar el comportamiento del agente.

## Tecnologías

Python · PyBullet · Deep Q-Learning · Jupyter Notebook
