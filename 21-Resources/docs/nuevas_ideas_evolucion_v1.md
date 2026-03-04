# Nuevas Ideas de Evolución (Dashboard y Salud Social)

Este documento recoge ideas extendidas para un posible **Módulo 5 (Dashboard General)**, enfocadas en ofrecer a la gerencia y a los cuidadores una visión global interactiva del estado social de la residencia, basándose en la información que alimenta el Módulo 3.

## 1. Mapa de Relaciones (El Grafo Social)
- **Concepto**: Una visualización de red (nodos y enlaces interactivos) donde cada nodo es un residente.
- **Funcionamiento**: Las líneas conectan a los residentes que han interaccionado positivamente o que comparten grandes afinidades (calculadas por la IA). 
- **Valor Visual**: Permite a la dirección ver clústeres reales ("El grupo de las ex-costureras que juegan juntas", "Los tres veteranos que charlan después de comer").

## 2. Detector de Aislamiento y Bajas Conexiones
- **Problema en Macrorresidencias**: Ciertas personas más tímidas pueden deprimirse sin que el personal note su aislamiento social de inmediato.
- **La Solución (IA Social)**: 
  - La red interactiva (El Mapa de Relaciones) marcará en color "rojo o naranja apagado" aquellos nodos (residentes) que tienen *menos de X interacciones semanales*, o que su "puntuación de conexión" es inferior a la media de la residencia.
  - **Alerta Proactiva**: El sistema envía una notificación a los psicólogos o cuidadores principales: *"Josefa tiene un nivel de interacción bajo esta semana. Trata de presentarle a Marta (Match: 85%) usando esta carta de presentación durante la comida"*.

## 3. Estado General de la Residencia (Overview)
Un pequeño panel de control general, de un vistazo rápido ("Glanceability"):
- **Termómetro Social**: Un indicador del nivel de actividad o de nuevas conexiones formadas en la última semana. 
- **Tablón de Tareas Pendientes (To-Do List)**: Una lista de tareas de cuidado blando o emocional (no tareas médicas de pastillas que van por el otro software).
  - *Ejemplo P. Gerontológico*: "Hacer que Antonio y Carmen se sienten juntos hoy en la sala T.V."
  - *Ejemplo Familiar*: "Subir al menos 2 fotos esta semana del pueblo de Luis" / "Grabar un audio corto hoy para que lo escuche mañana en el buzón".

## 4. Checklist de Información Incompleta (Onboarding Constante)
El "Mapa de Vida" (Módulo 1) requiere información para que el algoritmo sea útil, pero a las familias se les puede olvidar.
- **Recordatorios Inteligentes**: Un indicador de completitud del perfil. "El Mapa de Vida de Juanito está al 35%".
- **Micro-tareas para las Familias**: La app le envía notificaciones con micro-preguntas fáciles al móvil del hijo o nieto para que las responda en 10 segundos ("¿Le gustaban más a Juanito los gatos o los perros? Pulsa una opción"). Esto asegura un **seguimiento continuo e incremental**, mejorando la resiliencia del sistema y manteniendo un perfil rico casi sin esfuerzo por parte de los familiares.
