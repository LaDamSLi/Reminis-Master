# Plan Módulo 4: Experiencias de Reminiscencia (IA Visual y Guiado)

Este documento detalla el Módulo 4, enfocado en exprimir el contenido subido (Módulo 2) ya sea mejorándolo visualmente mediante IA o utilizándolo como base para crear momentos de reminiscencia y conversación directa presencial.

## 1. El Foco del Módulo: Estimulación Guiada
Más que una experiencia tecnológica pasiva (ej. "ponerle unas gafas de RV al anciano y dejarlo solo"), este módulo es una herramienta de **estimulación activa guiada por el cuidador o la familia**.
- **Propósito**: "Sacar un tema y hablar de él". Cuando la familia va de visita o el cuidador tiene 10 minutos, abre este módulo para encontrar *disparadores* de interés actualizados.
- **Actualización Continua**: Mientras hablan de la foto mejorada, el cuidador/familiar puede actualizar en tiempo real qué siente el residente respecto a ese tema *ahora*, o mencionar nuevas conexiones que el mayor recuerde en ese momento. Esto alimenta de nuevo el "Módulo 1: Mapa de Vida", manteniendo el perfil siempre vivo y dinámico, no estático.

## 2. Herramientas Tecnológicas Principales (IA)

### A. Escáner Inteligente (Restauración)
Las familias a menudo tienen fotos físicas de los años 40/50, rotas o muy descoloridas, pero no tienen escáner.
- **Flujo en App**: El módulo incluye una cámara enfocada en "Escanear Documento Antiguo" (con detección de bordes y corrección de perspectiva mediante librerías React Native).
- **Procesamiento Backend (Firebase)**: La foto se sube y un modelo de IA restaurador (integrado vía API externa) mejora la resolución (upscaling), limpia el ruido, arregla las roturas físicas virtuales e incluso sugiere aplicar un coloreado suave y respetuoso. 
- **Impacto Terapéutico**: Un residente con deterioro cognitivo reconoce mucho más rápido una foto brillante y con color que una pálida y rota, disparando antes el recuerdo emocional.

### B. "Hilos de Conversación" Activos
- Basado en el "Reverso Obligatorio" introducido en el Módulo 2, la IA analiza quién sale en la foto y qué se hacía.
- Gira la foto y la interfaz le da al familiar/cuidador 3 "Hilos de conversación" que puede leerle al mayor:
  - *Opción 1*: "Mírate en estas fiestas de San Juan, ¿recuerdas a qué olía la pólvora?" (Sentidos).
  - *Opción 2*: "¿Te sigues hablando con tu prima Rosa, la que está a tu izquierda?" (Conexiones).
  - *Opción 3*: "¿Qué cambiarías de este día si pudieras volver?" (Reflexión).

## 3. Arquitectura Relacionada
- **React Native**: Módulo de cámara integrado (`expo-camera` o `react-native-vision-camera`) con *bounding boxes* para escanear en tiempo real.
- **Firebase Functions / Integraciones**: Lógica de envío a una API de IA de corrección de imágenes (e.g., Replicate / ESRGAN o similar) y retorno de la imagen procesada a Supabase Storage con un estado de `restored = true`.
