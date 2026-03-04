# Plan Módulo 3: Actividades, Emparejamiento e IA (El Cerebro)

Este documento define la arquitectura lógica y visual del Módulo 3, centrado en aliviar la carga social del cuidador automatizando la búsqueda de afinidades entre residentes y sugiriendo actividades lúdicas personalizadas.

## 1. El Algoritmo de Emparejamiento (Transversal, no solo Tags)
Para que el matching sea resiliente y verdaderamente útil, no podemos limitarnos a un simple filtro de "A ambos les gusta el fútbol". El algoritmo (ejecutado en Firebase Functions) comparará **Categorías de Vida** ponderadas.

### A. Categorización del Mapa de Vida
La información introducida en el Módulo 1 se estructurará internamente en 4 macro-categorías para el algoritmo:
1. **Entorno de Origen / Vivencias**: Dónde nació, dónde vivió la mayor parte de su vida, si migró, si vivió en entorno rural o urbano.
2. **Vida Laboral / Vocación**: Profesión principal, oficios secundarios, si fue amo/a de casa, responsabilidades clave.
3. **Pasiones y Hobbies (Etapa Activa)**: Deportes, manualidades, música, lectura, costura, baile (lo que requiere una acción física/mental activa).
4. **Rasgos de Personalidad / Preferencias Actuales**: Introvertido/extrovertido, prefiere mañanas o tardes, prefiere grupos pequeños o grandes, tolerancia al ruido.

### B. Lógica del Match Transversal
El algoritmo buscará conexiones cruzadas (transversales) entre estas categorías. Ejemplos de match avanzado:
- **Match Directo**: Ambos originarios de pueblos cercanos de Asturias (Categoría 1).
- **Match Transversal (Vocación + Hobby)**: Un residente era profesor de historia (Cat 2) y otra residente es una apasionada de la lectura de novelas históricas (Cat 3).
- **Match de Complementariedad**: Una persona muy extrovertida a la que le gustaba cantar (Cat 4 + Cat 3) emparejada con alguien introvertido que solía tocar un instrumento o disfrutaba del teatro.

## 2. Cartas de Presentación (Para el Cuidador)
Una vez que el sistema detecta una afinidad alta (> 75%), no junta a los residentes automáticamente. Le da la herramienta al cuidador a través de **"Cartas de Presentación"**.

### Cómo funciona en la App:
- El cuidador abre la sección "Conexiones Sugeridas".
- Ve una tarjeta con las fotos de Antonio y Carmen.
- **La Carta de Presentación (Generada por IA)** le da un *script* exacto y un contexto de por qué el sistema los unió.
  - *Ejemplo de la tarjeta*: "💡 **Sugerencia de conexión**: Antonio y Carmen. Ambos vivieron la posguerra en Madrid y comparten el amor por la zarzuela. **Qué decirle a Antonio**: _'Antonio, quiero presentarte a Carmen, me ha contado que ella también solía ir a La Latina a escuchar zarzuelas cuando era joven'_. **Qué decirle a Carmen**: _'Carmen, Antonio es de tu misma época en Madrid, seguro que conocéis los mismos sitios'._"
- **Reducción de dificultad**: Esto abstrae toda la complejidad del algoritmo. El cuidador solo lee una frase amigable de 3 líneas y la ejecuta, facilitando enormemente su labor integradora.

## 3. Generación de Actividades Lúdicas
Basado en las mismas categorías, la IA sugerirá actividades que el equipo de la residencia o la familia pueden llevar a cabo.
- **Actividades Individuales**: Si el residente fue sastre, la app sugiere al familiar: *"Llévale retales de tela con diferentes texturas la próxima vez que vengas, le ayudará a estimular el tacto y la memoria vocacional"*.
- **Actividades Grupales**: Si el sistema detecta que 4 personas tienen afinidad por la botánica o la vida en el campo (Match Transversal), sugiere a la terapeuta ocupacional organizar un taller de jardinería o cuidado de plantas de interior para ese micro-grupo.

## 4. Requisitos Técnicos e Integración
- **Supabase**: Las respuestas del "Smart Questionnaire" del Módulo 1 deben mapearse a campos JSON estructurados según las 4 macro-categorías (ej. `vida_laboral_tags`, `entorno_tags`).
- **Firebase Functions (Python)**:
  - Script programado diario/semanal: Descarga los JSON de nuevos residentes, ejecuta el algoritmo de cálculo de similitud (ej. similitud del coseno sobre embeddings generados por los textos biográficos, o un sistema de pesos por reglas).
  - Llama a un LLM (ej. GPT-4o-mini o Claude Haiku) pasándole el perfil cruzado de los 2 residentes para generar el texto humano de la "Carta de Presentación".
  - Guarda las conexiones generadas en Supabase en una tabla `suggested_connections` para que la app las muestre al cuidador.
