# Master Plan: Reminiscencia

- **Objetivo Principal**: Desarrollar una aplicación nativa que ayude al personal de residencias a conocer profundamente y preservar la identidad de las personas mayores.
- **Público Objetivo**: Personal gerontológico (cuidadores, médicos, enfermeras) y familiares.
- **Enfoque de Diseño**: Estética minimalista. "Interfaces atractivas que destacan por su sencillez y dinamismo". La información compleja debe comprenderse en muy pocos segundos por la sobrecarga laboral.

---

## 1. Arquitectura del Sistema
El proyecto se divide en 3 áreas ya estructuradas:
- **Frontend (01-app)**: Aplicación Móvil en React Native (Expo) usando NativeWind (TailwindCSS) para conseguir la estética moderna y consistente.
- **Base de Datos (03-database)**: Supabase (PostgreSQL) para gestionar el almacenamiento estructurado de la información médica, el perfil del residente, y las jerarquías de roles (Admin, Cuidador, Familiar).
- **Backend de Procesamiento (02-backend)**: Firebase Cloud Functions (Python o Node.js) para algoritmos pesados, procesamiento de fotos (ej. reducciones, reconocimiento), integración de IA, lógicas de gamificación, y envío de notificaciones.

---

## 2. Definición de Módulos (Refinada)

### Módulo 1: Mapa de Vida y Cuestionario AI
- Fichas visuales o tarjetas rápidas para el cuidador (cero texto denso).
- **Cuestionario Avanzado (AI Asistido)**: Una subsección donde los familiares/residentes pueden rellenar información de forma sencilla. La IA asiste haciendo preguntas o estructurando respuestas incompletas para mantener la información siempre actualizada de manera fácil.

### Módulo 2: Archivo Multimedia y Conexión Familiar
- Un repositorio personal del residente ("Instagram privado").
- **Conectividad Familiar**: Los familiares pueden subir fotos antiguas/nuevas y recibir notificaciones (Push alerts) sobre el día a día del residente y sus actividades.

### Módulo 3: Actividades, Emparejamiento e IA (El Cerebro)
- **Generación de Actividades**: La IA usa el historial/gustos del residente para sugerir dinámicas aplicables al personal o a la familia.
- **Match de Residentes (Socialización)**: Algoritmo en Firebase que cruza los Mapas de Vida de los residentes para encontrar intereses comunes y sugerir conexiones, aliviando la carga al cuidador al promover relaciones entre internos afines.

### Módulo 4: Experiencias de Reminiscencia (IA Visual)
- **Mejora y Restauración**: Módulo de escaneo que recupera fotos dañadas (usando modelos de IA como ESRGAN integrados vía API).
- **Animación y Color**: Capacidad de dar color a fotos en blanco/negro antiguas o animar rostros suavemente para potenciar el recuerdo emocional.

---

## 3. Arquitectura y Stack Tecnológico Detallado

- **Autenticación**: `Supabase Auth`. Control de roles (Personal, Familiares).
- **Base de Datos**: `Supabase PostgreSQL`. Relaciones complejas (Residentes, Familiares, Actividades).
- **Almacenamiento (Storage)**: `Supabase Storage`. Gratuito hasta 1GB, cuenta con una fácil integración con CDN locales y redimensionamiento. Es lo mejor para iniciar sin requerir plataformas externas como Cloudinary (a menos que se excedan los límites, en cuyo caso Firebase Functions actuará de puente a AWS S3 o similar).
- **Backend / Procesamiento**: `Firebase Cloud Functions` (Python). Actuará como integrador. Funciones en Python recibirán la señal de nueva foto en Supabase, llamarán a APIs externas de IA para restaurar imagen/colorear, y devolverán el resultado. También correrá los scripts de *matching* de residentes y generación de lenguaje natural.

---

## 4. UI / Estética Minimalista
- Inspirado directamente en los PDFs académicos: **Gama policromática sobria** centrada en Blancos, Negros y Grises, aportando un tono clínico pero elegante.
- Se incluirá **un único color de acento** (por ejemplo, un azul apagado o tono "terracota" muy sutil, dependiendo del moodboard final) para botones y llamadas a la acción (CTAs).
- Interfaces dominadas por el espacio en blanco (White-space), bordes muy redondeados y uso masivo de iconografía para reducir fatiga visual.
