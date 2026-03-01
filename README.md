# Reminiscencia

**"Del Hogar a la Residencia: Diseño para preservar la identidad"**

Este proyecto es el repositorio central (master) de la infraestructura de la aplicación móvil "Reminiscencia", desarrollada como parte de un Trabajo de Fin de Máster (TFM).

## Descripción del Proyecto

"Reminiscencia" es una aplicación digital diseñada como herramienta de apoyo sociosanitario para el personal de residencias de mayores y centros de día. El objetivo principal de la aplicación es **preservar la identidad** de las personas mayores, combatir la soledad, reducir el impacto de la despersonalización y facilitar su integración en el ecosistema residencial.

Se estructura en los siguientes módulos clave:
1. **Mapa de vida**: Acceso rápido visual a información significativa y rutinas del residente.
2. **Archivo multimedia compartido**: Material biográfico, fotos y audios (vínculo con la familia).
3. **Actividades lúdicas de integración**: Dinámicas basadas en la historia de vida del residente para fomentar la socialización.
4. **Inteligencia Artificial y Realidad Virtual**: Experiencias de estimulación cognitiva y reminiscencia.

## Arquitectura y Repositorios

El proyecto sigue una estructura multi-repositorio dividida por componentes arquitectónicos. Cada carpeta funciona como un repositorio Git independiente.

- **`01-app/`**: Aplicación móvil nativa en Android, desarrollada usando React Native y Expo.
- **`02-backend/`**: Lógica de backend y funciones de servidor alojadas en Firebase (Cloud Functions, Authentication, etc.).
- **`03-database/`**: Configuración y esquemas de la base de datos relacional y gestión de almacenamiento gestionada a través de Supabase (PostgreSQL).
- **`21-Resources/`**: Carpeta de recursos de diseño, PDFs y documentación del proyecto.

## Uso de Expo Go
_Nota de seguridad sobre el entorno de desarrollo_

El desarrollo inicial de la aplicación se probará utilizando **Expo Go**. Utilizar Expo Go localmente es **completamente seguro**. Funciona creando un servidor de desarrollo local en tu ordenador que transmite el código Javascript a través de tu red Wi-Fi (LAN) (o mediante cable USB) directamente a la aplicación Expo Go de tu teléfono móvil.

Tu código fuente **no se sube a internet** ni queda expuesto públicamente durante este proceso de desarrollo local (siempre que utilices una red privada y de confianza). Es un entorno pensado precisamente para asegurar iteraciones rápidas de manera privada.

## Convención de Trabajo en Git

Para garantizar la estabilidad del proyecto y el correcto funcionamiento de los submódulos, el equipo (y este repositorio Master) se rige bajo el siguiente flujo de trabajo:

1. **La rama `master` siempre debe ser desplegable** y contener código estable.
2. Todo nuevo desarrollo debe hacerse en una rama separada creada a partir de `master` y siguiendo esta nomenclatura:
   - `feat/nombre-de-la-tarea` (Para características nuevas, ej: `feat/login-screen`).
   - `fix/nombre-del-error` (Para corregir fallos, ej: `fix/crash-on-map`).
   - `chore/nombre-de-la-tarea` (Para actualizaciones de dependencias, configuración, etc.).
   - `docs/nombre-del-documento` (Para cambios en README o documentación).
3. Una vez finalizado el desarrollo en la rama, se hará `git push` y se abrirá un **Pull Request (PR)** hacia `master`.
4. El código sólo se fusionará tras ser revisado mediante **Merge Pull Request**.

> **Nota sobre submódulos**: Al actualizar el repositorio Master de un PR, recuerda también actualizar los submódulos ejecutando `git submodule update --remote` si fuese necesario sincronizar los últimos cambios de las carpetas de App/DB/Backend.
