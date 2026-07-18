# quiz-cli

Aplicación CLI de quiz interactivo desarrollada en **Node.js** y **JavaScript con ES Modules**, sin dependencias externas. Permite seleccionar una categoría, responder preguntas desde la terminal y obtener un resumen final con puntuación, retroalimentación y repaso de respuestas incorrectas.

## Descripción general

`quiz-cli` es una aplicación de línea de comandos orientada a practicar conceptos de programación mediante cuestionarios interactivos.

A partir del código fuente analizado, la aplicación:

- carga preguntas desde un archivo JSON local;
- permite elegir una categoría;
- permite seleccionar cuántas preguntas responder;
- muestra opciones numeradas en terminal;
- valida la respuesta del usuario;
- informa si cada respuesta fue correcta o incorrecta;
- muestra una explicación cuando está disponible;
- presenta resultados finales con porcentaje y mensaje de desempeño;
- ofrece volver a jugar al finalizar una partida.

## Características

- Interfaz interactiva en terminal.
- Implementación en **JavaScript ES Modules**.
- Uso exclusivo de módulos integrados de Node.js.
- Sin dependencias externas.
- Selección de categoría antes de iniciar el quiz.
- Selección de cantidad de preguntas (`todas`, `3` o `5`, según disponibilidad).
- Barajado de preguntas antes de cada partida.
- Barra de progreso durante el juego.
- Resumen final con puntaje y porcentaje.
- Revisión de respuestas incorrectas.
- Colores y estilos ANSI para mejorar la experiencia en consola.

## Tecnologías utilizadas

### Lenguajes

- JavaScript

### Entorno y herramientas

- Node.js `>=18.0.0`
- npm scripts definidos en `package.json`

### Módulos integrados de Node.js utilizados

- `node:fs/promises`
- `node:path`
- `node:url`
- `node:readline`

### Dependencias externas

- No tiene dependencias externas declaradas.

## Arquitectura

A partir del código fuente, se identifica una arquitectura simple de tipo **CLI monolítica**, organizada por responsabilidades:

- **Punto de entrada**: `index.js`
- **Lógica del juego**: `src/quiz.js`
- **Entrada e interacción por terminal**: `src/input.js`
- **Estilos ANSI y utilidades visuales**: `src/colors.js`
- **Fuente de datos**: `data/questions.json`

### Flujo general

1. La aplicación inicia desde `index.js`.
2. Se carga el archivo `questions.json`.
3. Se muestran las categorías disponibles.
4. El usuario selecciona una categoría.
5. El usuario elige cuántas preguntas responder.
6. Se crea una instancia de `Quiz`.
7. Las preguntas se presentan una a una en la terminal.
8. Cada respuesta se valida y se muestra retroalimentación inmediata.
9. Al finalizar, se muestran resultados y preguntas falladas.
10. El usuario puede decidir si desea jugar nuevamente.

## Requisitos

- **Node.js 18 o superior**
- Terminal compatible con ejecución de comandos Node.js

> Según `package.json`, el proyecto requiere `node >=18.0.0`.

## Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/oddiemva/test-app.git
```

### 2. Entrar al directorio del proyecto

En el repositorio analizado, la aplicación se encuentra dentro de:

```bash
cd test-app/test-app
```

### 3. Verificar la versión de Node.js

```bash
node --version
```

Debe ser `18.0.0` o superior.

> No se identificaron dependencias externas que requieran instalación adicional.

## Uso

### Ejecutar la aplicación

```bash
npm start
```

o directamente con Node.js:

```bash
node index.js
```

### Flujo de uso en terminal

Al ejecutar la aplicación:

1. se muestra un banner de bienvenida;
2. se pide elegir una categoría;
3. se pide elegir cuántas preguntas responder;
4. se inicia el quiz;
5. cada respuesta se selecciona escribiendo el número de la opción;
6. al finalizar, se muestra el resultado total;
7. se pregunta si se desea volver a jugar.

### Ejemplo de ejecución

```bash
npm start
```

Ejemplo de interacción esperada:

```text
Choose a category:

  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming

Your choice (enter number): 2
```

Luego la aplicación solicita la cantidad de preguntas y continúa con el cuestionario.

## Scripts disponibles

Según `package.json`, los scripts disponibles son:

| Script | Comando | Descripción |
|---|---|---|
| `start` | `node index.js` | Inicia la aplicación CLI |
| `test` | `node --test` | Ejecuta pruebas usando el runner nativo de Node.js |

## Estructura del proyecto

La estructura observada en el repositorio es la siguiente:

```text
.
├── README.md
└── test-app/
    └── test-app/
        ├── package.json
        ├── index.js
        ├── data/
        │   └── questions.json
        └── src/
            ├── colors.js
            ├── input.js
            └── quiz.js
```

### Descripción de archivos principales

- `package.json`: metadatos del proyecto, scripts y requisito de versión de Node.js.
- `index.js`: punto de entrada de la aplicación y flujo principal.
- `src/quiz.js`: clase `Quiz`, puntuación, progreso, mezcla de preguntas y resultados.
- `src/input.js`: utilidades para prompts, selección de opciones y confirmaciones.
- `src/colors.js`: funciones para aplicar estilos ANSI a la salida en terminal.
- `data/questions.json`: banco de preguntas agrupado por categorías.

## Cómo funciona

### Carga de preguntas

La aplicación lee `data/questions.json` utilizando `readFile` de `node:fs/promises` y convierte el contenido con `JSON.parse`.

### Selección de categoría

Las categorías se obtienen desde la clave `categories` del JSON y se presentan como una lista numerada.

### Cantidad de preguntas

Para cada categoría, la aplicación permite seleccionar:

- todas las preguntas;
- 3 preguntas, si la categoría tiene al menos 3;
- 5 preguntas, si la categoría tiene al menos 5.

### Orden de las preguntas

Las preguntas se mezclan mediante un algoritmo tipo **Fisher-Yates** implementado en `src/quiz.js`.

### Respuestas

El usuario responde introduciendo el número correspondiente a la opción elegida. Internamente:

- las opciones mostradas al usuario empiezan en `1`;
- la respuesta correcta en el JSON se almacena como índice numérico base `0`.

### Resultados

Al terminar el cuestionario, se muestran:

- categoría jugada;
- puntaje total;
- porcentaje de aciertos;
- mensaje de desempeño;
- lista de preguntas respondidas incorrectamente, con la respuesta elegida y la correcta.

## Preguntas y categorías

Las preguntas se almacenan en `data/questions.json`. 

### Categorías identificadas

A partir del archivo analizado, existen las siguientes categorías:

- **JavaScript Basics**
- **Node.js Fundamentals**
- **General Programming**

### Estructura de cada pregunta

Cada pregunta sigue esta forma:

```json
{
  "question": "Texto de la pregunta",
  "options": ["Opción 1", "Opción 2", "Opción 3", "Opción 4"],
  "answer": 2,
  "explanation": "Explicación de la respuesta correcta"
}
```

### Observaciones sobre los datos

- Las preguntas están agrupadas por categoría.
- Cada categoría contiene un nombre visible y una colección de preguntas.
- La propiedad `answer` representa el índice correcto dentro del arreglo `options`.
- La propiedad `explanation` se muestra después de responder.

## Configuración

No se identificaron variables de entorno, archivos `.env` ni parámetros externos de configuración.

La configuración funcional del contenido del quiz depende principalmente de:

- `data/questions.json`
- `package.json`

## Pruebas

El proyecto define el siguiente comando para pruebas:

```bash
npm test
```

que ejecuta:

```bash
node --test
```

Sin embargo, **no se identificaron archivos de prueba en el repositorio analizado**, por lo que no se pudo determinar a partir del código fuente qué casos de prueba existen actualmente.

## Notas de desarrollo

- El proyecto usa `"type": "module"` en `package.json`, por lo que emplea sintaxis `import/export`.
- El punto de entrada define un *shebang* (`#!/usr/bin/env node`), lo que es consistente con una herramienta CLI.
- La interfaz de entrada se implementa con `readline`.
- Los colores y estilos visuales se implementan manualmente con códigos ANSI en `src/colors.js`.
- El proyecto no usa frameworks ni librerías de terceros.
- La salida de error incluye mensaje y stack trace cuando ocurre una excepción durante la ejecución.
- El contenido del quiz es extensible mediante la edición de `data/questions.json`.

## Contribuciones

Si deseas contribuir, una forma razonable de trabajo sería:

1. hacer un fork del repositorio;
2. crear una rama para tu cambio;
3. implementar la mejora o corrección;
4. probar la aplicación localmente;
5. abrir un Pull Request.

### Recomendaciones al contribuir

- Mantener el estilo modular actual.
- Evitar agregar dependencias externas si no son necesarias.
- Si se agregan nuevas preguntas, respetar la estructura existente en `data/questions.json`.
- Si se modifica la experiencia CLI, mantener la interacción simple y consistente.

## Licencia

Este proyecto está distribuido bajo la licencia **MIT**.
