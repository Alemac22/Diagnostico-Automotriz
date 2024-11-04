
![Politecnico](https://github.com/Alemac22/Diagnostico-Automotriz/blob/main/Imagenes/Politecnico.jpg)

 **Carrera:** Tecnicatura Superior en Ciencia de Datos e Inteligencia Artificial.

 **Institucion:** Politécnico Malvinas Argentinas

 **Materia:** Desarrollo de Sistemas de I.A.

 **Proyecto Desarrollo de Sistemas de I.A.:** Sistema Experto de Diagnostico Automotriz

 **Alumno:** Alejandro Maclean

 **Profesor de la Catedra:** Martin Mirabete

 <p align="center">
  <img src="https://komarev.com/ghpvc/?username=Alemac22" alt="Vistas de perfil" />
  <a href="https://opensource.org/licenses/MIT">
    <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT" />
  </a>
</p>


# **SISTEMA EXPERTO DE DIAGNÓSTICO AUTOMOTRIZ**

A continuación, describo la metodología y los elementos clave que se emplearán para la toma de decisiones, basados en las reglas y métodos de inferencia.

___

### <u>Estructura y Organización del Conocimiento</u>

**1. Representación del Conocimiento:**

   ❖ La base de conocimiento se organiza en un archivo JSON, estructurado en forma de entradas de diagnóstico. Cada entrada incluye:

   - **name**: Nombre del diagnóstico o acción a ejecutar.
   - **description**: Descripción detallada de los síntomas o razones que llevan a ese diagnóstico.
   - **props**: Lista de síntomas o propiedades relevantes que definen las condiciones para llegar al diagnóstico.

   ❖ Este formato JSON facilita la organización jerárquica y la reutilización de conocimiento, permitiendo que cada entrada sea una combinación de síntomas únicos.

**2. Reglas de Decisión:**

   ❖ Cada entrada actúa como una regla **if-then**. La lógica se aplica de la siguiente forma:
   - **Condición (if)**: Se satisface cuando todos los síntomas listados en **props** coinciden con los síntomas positivos reportados por el usuario.
   - **Acción (then)**: Si todas las condiciones en **props** son afirmativas, el sistema infiere el diagnóstico especificado en **name**.
   
   ❖ **Ejemplo de Aplicación de Reglas:**
   - **Regla 1**: Si el auto no arranca, el motor gira, los cables de bujía tienen chispa, y el vehículo tiene combustible, el sistema recomendará "Reemplazar la bomba de nafta".
   - **Regla 2**: Si el auto no arranca, el motor gira, los cables de bujía tienen chispa, pero no tiene combustible, el sistema recomendará "Cargar nafta".

___

### **Métodos de Inferencia**

**1. Motor de Inferencia Basado en Reglas:**

   ❖ El motor evalúa de manera iterativa cada entrada de la base de conocimiento:
   - Si una entrada es satisfactoria (es decir, si todos los síntomas de **props** son afirmativos), el sistema concluye con el diagnóstico.
   - Si la entrada no cumple, el sistema pasa a la siguiente, lo que permite continuar la evaluación sin interrupciones hasta encontrar una coincidencia o llegar al final de la base de conocimiento.

**2. Encadenamiento Progresivo:**

   ❖ La estructura de preguntas sigue un encadenamiento progresivo. A medida que el usuario responde, el sistema almacena las respuestas positivas, acumulando síntomas confirmados que se utilizan para la toma de decisiones en tiempo real.

___

### **Organización Jerárquica y Lógica de Conocimiento**

**1. Agrupación de Conceptos:**

   ❖ Los síntomas en **props** representan un conjunto de condiciones necesarias y suficientes para cada diagnóstico, permitiendo así organizar el conocimiento en categorías de síntomas interdependientes.

   ❖ Las condiciones se estructuran de modo que los diagnósticos más específicos y complejos aparezcan después de evaluar opciones más simples (ej., verificar carga de la batería antes de sugerir cambios en el motor de arranque).

**2. Jerarquización de Reglas:**

   ❖ La jerarquía dentro de la base de conocimiento se organiza con diagnósticos de baja complejidad (cargar batería) primero y diagnósticos de alta complejidad (reparar el distribuidor) después.

   ❖ Esto permite una búsqueda progresiva y mejora la eficiencia del sistema al resolver primero posibles causas simples antes de proceder a diagnósticos complejos.

**3. Interrelación de Reglas y Síntomas:**

   ❖ Los síntomas se agrupan en conjuntos de condiciones mutuamente excluyentes, como síntomas relacionados con la carga de la batería y los fusibles, que definen caminos únicos de diagnóstico.
   
   ❖ La estructura modular permite que el sistema experto agregue nuevos diagnósticos en el futuro sin modificar la lógica del motor de inferencia, solo ajustando o añadiendo nuevas entradas JSON.

___

### **Inferencia de Diagnóstico**

El motor de inferencia compara la lista acumulada de **positive_symptoms** con **props** de cada entrada. Si encuentra una coincidencia completa, da el diagnóstico correspondiente. Si no hay coincidencia, se devuelve una respuesta indicando que no hay un diagnóstico posible en la base de conocimiento actual.

Esta organización y lógica garantizan que el sistema responda eficazmente, adaptándose a nuevos síntomas o diagnósticos y permitiendo una evolución constante de la base de conocimiento.


Este sistema experto, desarrollado en **Python**, permite el diagnóstico remoto de problemas en el sistema de arranque de vehículos, utilizando **FastAPI** para el backend y **React** para el frontend.

## Instrucciones de Instalación y Puesta en Marcha

Sigue los pasos a continuación para configurar y ejecutar el sistema experto de diagnóstico automotriz. 

### Requisitos Previos

- **Python** y **pip** instalados en tu computadora.
- **Node.js** y **npm** instalados para manejar el frontend.
- Editor de código como **Visual Studio Code** (VSC) para facilitar la edición.

### Pasos para la Instalación

#### 1. Clona el Repositorio

Copia el repositorio del sistema experto a tu máquina local. Esto creará una carpeta con todos los archivos del proyecto.

```bash
git clone <URL del repositorio>
cd DIAGNOSTICO AUTOMOTRIZ
```

#### 2. Configuración del Servidor Backend (FastAPI)

1. Accede al directorio principal del proyecto en Visual Studio Code (donde está el archivo `main.py`).
2. Abre una terminal en Visual Studio Code (Terminal > Nueva Terminal).
3. Ejecuta el siguiente comando para iniciar el backend con FastAPI:

   ```bash
   uvicorn main:app --reload
   ```

   Esto iniciará el servidor en `http://127.0.0.1:8000`. La opción `--reload` permite que el servidor se reinicie automáticamente cada vez que se detectan cambios en el código.

4. Abre `http://127.0.0.1:8000/docs` en tu navegador para verificar que el backend esté funcionando y para explorar la documentación interactiva de la API.

#### 3. Configuración de la Interfaz de Usuario (Frontend con React)

1. Navega al directorio del frontend ubicado en `frontend/frontend`.
2. Abre una nueva terminal en Visual Studio Code y ve al directorio correspondiente.

   ```bash
   cd frontend/frontend
   ```

3. Instala las dependencias necesarias ejecutando el comando:

   ```bash
   npm install
   ```

   Si encuentras errores al ejecutar este comando, asegúrate de que Node.js y npm están correctamente instalados. Puedes verificar las versiones instaladas con:

   ```bash
   node -v
   npm -v
   ```

4. Inicia el servidor de desarrollo de React en el puerto 3000 usando:

   ```bash
   npm start
   ```

   Esto debería lanzar el frontend en `http://localhost:3000`. Asegúrate de que el puerto 3000 esté libre para evitar conflictos.

#### 4. Comprobación de Conexión entre Backend y Frontend

1. Verifica que ambos servidores (el backend en el puerto 8000 y el frontend en el puerto 3000) estén funcionando sin errores.
2. Accede a `http://localhost:3000` en tu navegador para interactuar con el sistema y realizar pruebas de diagnóstico automotriz desde la interfaz.

### Comandos Clave

- Iniciar el backend con FastAPI:

  ```bash
  uvicorn main:app --reload
  ```

- Instalar dependencias en el directorio del frontend:

  ```bash
  npm install
  ```

- Ejecutar el servidor de React:

  ```bash
  npm start
  ```

### Archivos Esenciales

- **main.py**: Contiene el backend desarrollado con FastAPI, proporcionando rutas para cargar la base de conocimientos (`/base/cargar`), iniciar consultas de diagnóstico (`/consultar/iniciar`), y procesar respuestas del usuario (`/consultar/responder`). La lógica de inferencia se encuentra en la clase `Engine` en el archivo `engine.py`.

- **Base de Conocimiento Diagnostico Automotriz.json**: Archivo JSON que almacena el conocimiento utilizado por el sistema para realizar diagnósticos y deducir posibles problemas en el sistema de arranque de los vehículos.

---

Siguiendo estos pasos, deberías lograr configurar y ejecutar el sistema experto de diagnóstico automotriz correctamente. Revisa cada paso y asegúrate de que los entornos de backend y frontend estén configurados adecuadamente para evitar problemas durante la instalación.
```

Copia y pega este contenido en el archivo `README.md` y tendrá el formato correcto para GitHub u otros visores de Markdown.