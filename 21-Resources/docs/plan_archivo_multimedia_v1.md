# Plan Módulo 2: Archivo Multimedia y Conexión Familiar

Este documento desarrolla la visión técnica y visual del Módulo 2, cuyo objetivo principal es crear un ecosistema nostálgico que conecte a las familias con la historia del residente, facilitando al mismo tiempo la labor de conexión emocional del personal cuidador.

## 1. Concepto Visual UX/UI: El "Archivador Analógico"
La estética debe romper con la frialdad de la típica "galería de fotos" o "feed de Instagram". Para apelar a la memoria de toda la vida y al diseño elegante:
- **Metáfora de Cajonera o Archivo Físico**:
  - Las colecciones o meses se representan visualmente como *carpetas de cartón* o apartados de un archivador antiguo (en texturas lisas blanco/gris).
  - Al hacer tap en una "carpeta", las fotos se deslizan hacia arriba o se apilan (stack animations) simulando sacar papeles de un sobre.
- **Fotos Estilo Polaroid / Analógico**:
  - Las imágenes tendrán márgenes gruesos en la parte inferior simulando espacio para escritura o notas al margen.
  - La navegación entre fotos se sentirá como "pasar fotos físicas" sobre la mesa.

## 2. Herramientas Core del Módulo

### A. Historias con Contexto Obligatorio ("El Reverso de la Foto")
No se trata de subir fotos vacías. Cada archivo o imagen que introduzcan los familiares requerirá un pequeño contexto ("Smart Context"):
- **¿Quién aparece?** (Etiquetado simple).
- **¿Dónde es?**
- **¿Por qué se tomó o qué anécdota tiene?**
- *Valor en Residencias*: Si el residente olvida, el cuidador, leyendo el "reverso" de la foto, puede ser el guía activo: _"Mira María, ¡aquí estás en las fiestas del pueblo con tu prima Ángela en los años 60!"_.

### B. Botón "Tirar del Hilo" (Recuerdo Sorpresa)
- Un CTA único, grande y accesible para el cuidador: **"Extraer Foto"**.
- El algoritmo (Firebase Functions) busca una foto aleatoria no vista recientemente y la saca en pantalla completa.
- Actúa como el perfecto rompehielos para cuando un residente está apático, ansioso o el cuidador necesita calmarle con un momento de conexión rápido.

### C. El Buzón Familiar (Mensajería Asíncrona)
- Los cuidadores, al leer la ficha diaria, a veces no tienen de qué hablar con los residentes.
- Funcionalidad de "Buzón de Correspondencia": Las familias pueden escribir mensajes breves o grabar audios (ej. _"¡Buenos días abuelo, hoy el niño empieza el cole!"_).
- El cuidador ve que hay "1 carta en el buzón". Al iniciar el turno, puede leerle o ponerle el audio al anciano, abriendo una ventana instantánea al mundo exterior y generando conversación automática entre el profesional y el residente.

## 3. Arquitectura y Componentes Relacionados
- **React Native / UI**:
  - Uso intensivo de `react-native-reanimated` y `react-native-gesture-handler` para simular las físicas de apilamiento de fotos y el deslizamiento de las carpetas/cajones.
- **Supabase (Backend y Auth)**:
  - Tabla `media_archive` (ID, residente_id, url_storage, fecha, descripcion, caras_etiquetadas).
  - Tabla `family_mailbox` (ID, residente_id, mensaje_texto, mensaje_audio_url, leido_por_cuidador, fecha_creacion).
  - Storage para guardar imágenes optimizadas y clips de audio.
- **Firebase Functions (Innovación IA - Opcional V2)**:
  - **Sugerencias de etiquetas**: Una IA sencilla podría proponer tags al detectar qué hay en la foto.
  - Generación de un "Podcast de Vida": A futuro, la IA de Firebase puede leer la historia de la foto con voz realista si el cuidador no está disponible.
