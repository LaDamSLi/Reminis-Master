# Plan Módulo 1: Mapa de Vida

Este documento detalla el alcance, las funcionalidades y la interfaz del Módulo 1 (Mapa de Vida), el cual es el núcleo organizativo y biográfico para cada residente.

## 1. Concepto Visual UX/UI
- **Línea de Tiempo Deslizable**:
  - La interfaz principal es un *Timeline* vertical u horizontal continuo.
  - El eje tendrá **Pasado, Presente (punto central remarcado) y Futuro** (próximas actividades, metas o eventos médicos).
  - **Espaciado Inteligente Distorsionado**: El espaciado entre eventos es proporcional al tiempo, pero con límites visuales ajustables. Si hay un salto histórico grande (ej. 30 años sin un hito relevante en la app), el eje se comprime con un diseño de "salto temporal" (como una línea punteada o rasgada) para no requerir scroll infinito, pero marcando visualmente que hubo un período largo de tiempo.
- **Estética Minimalista**:
  - Uso predominante de escala de grises y un color vibrante de acentuación para resaltar el Presente.
  - Las tarjetas de hitos en la línea de tiempo serán muy resumidas (ej. icono + título), tocándolas para ver detalles.

## 2. Herramienta de Ingreso: El "Smart Questionnaire"
El principal reto es la carga de datos. Se soluciona con un formulario interactivo potenciado por Inteligencia Artificial (LLMs desde Firebase Functions).

### Flujo de llenado por Familiares/Cuidadores:
1. **Asistente Conversacional Guiado**:
   - En lugar de un formulario frío de 50 campos en blanco, la app funciona como una entrevista guiada: *"Dime 3 cosas que le apasionaban a María en su juventud"*.
2. **Generación de Preguntas Inteligentes (IA)**:
   - Basándose en el contexto previo de la persona (ej. fecha de nacimiento, profesión anterior ingresada), la IA formula preguntas específicas que al familiar no se le habrían ocurrido:
     - *“Dado que Juan nació en la postguerra y fue carpintero, ¿tiene alguna herramienta específica que guarde con cariño?”*
   - Las preguntas cambian dinámicamente según se va enriqueciendo el perfil.
3. **Transcripción por Voz**:
   - Para máxima comodidad (pensando en familiares mayores o personal sin tiempo), el formulario aceptará respuestas largas por audio.
   - La IA lo transcribirá, extraerá las palabras clave, y lo encajará en la línea de tiempo automáticamente (identificando fechas aproximadas).

## 3. Arquitectura y Componentes Relacionados
- **React Native (Frontend)**:
  - Uso de animaciones de scroll fluido (`react-native-reanimated`) para la línea de tiempo.
  - Componente de formulario dinámico para el cuestionario paso a paso apoyado por notificaciones de Firebase.
- **Supabase**:
  - Tabla `life_events` relacionada con el perfil del residente (ID, título, fecha_estimada, archivo_adjunto_id, importancia).
  - Tabla `questionnaire_context` para guardar en JSON lo que la IA necesita saber para las siguientes preguntas.
- **Firebase Functions (Backend)**:
  - Endpoint `generateQuestions`: Llama a OpenAI / Claude para sugerir la próxima pregunta.
  - Endpoint `parseAudio`: Llama al módulo de Speech-to-Text y extracta entidades temporales para guardarlas en base de datos.
