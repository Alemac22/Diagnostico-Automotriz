# sistema-experto-python
Sistema experto en Python

## Instalación

Utilizar [`pipenv`](https://pipenv.pypa.io)

```bash
pipenv install
```

## Ejecutar

```bash
pipenv run main.py
```


---------------------------------------------------------------------------
![Politecnico](https://github.com/Alemac22/INDICE-DE-ENTORNO-DE-CALIDAD-DE-VIDA/blob/main/reports/figures/Politecnico.jpg)

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


***SISTEMA EXPERTO DE DIAGNOSTICO AUTOMOTRIZ***


A continuación, describo la metodología y los elementos clave que se 
emplearán para la toma de decisiones, basados en las reglas y métodos de 
inferencia.

**Estructura y Organización del Conocimiento**

**1. Representación del Conocimiento:**

   ❖ La base de conocimiento se organiza en un archivo JSON, 
estructurado en forma de entradas de diagnóstico. Cada entrada 
incluye:

      ➢ name: Nombre del diagnóstico o acción a ejecutar.
      ➢ description: Descripción detallada de los síntomas o 
razones que llevan a ese diagnóstico.
      ➢ props: Lista de síntomas o propiedades relevantes que 
      definen las condiciones para llegar al diagnóstico.
   ❖ Este formato JSON facilita la organización jerárquica y la 
      reutilización de conocimiento, permitiendo que cada entrada sea 
      una combinación de síntomas únicos.

**2. Reglas de Decisión:**

   ❖ Cada entrada actúa como una regla if-then. La lógica se aplica de 
      la siguiente forma:
      ➢ Condición (if): Se satisface cuando todos los síntomas 
      listados en props coinciden con los síntomas positivos 
      reportados por el usuario.
     ➢ Acción (then): Si todas las condiciones en props son 
      afirmativas, el sistema infiere el diagnóstico especificado 
      en name.
   ❖ Ejemplo de Aplicación de Reglas:
      ➢ Regla 1: Si el auto no arranca, el motor gira, los cables de 
      bujía tienen chispa, y el vehículo tiene combustible, el 
      sistema recomendará "Reemplazar la bomba de nafta".
      ➢ Regla 2: Si el auto no arranca, el motor gira, los cables de 
      bujía tienen chispa, pero no tiene combustible, el sistema 
      recomendará "Cargar nafta".

**Métodos de Inferencia**

**1. Motor de Inferencia Basado en Reglas:**

   ❖ El motor evalúa de manera iterativa cada entrada de la base de 
      conocimiento:
      ➢ Si una entrada es satisfactoria (es decir, si todos los 
      síntomas de props afirmativos), el sistema concluye con el 
      diagnóstico.
      ➢ Si la entrada no cumple, el sistema pasa a la siguiente, lo 
      que permite continuar la evaluación sin interrupciones 
      hasta encontrar una coincidencia o llegar al final de la base 
      de conocimiento.

**2. Encadenamiento Progresivo:**
   ❖ La estructura de preguntas sigue un encadenamiento progresivo. 
      A medida que el usuario responde, el sistema almacena las 
      respuestas positivas, acumulando síntomas confirmados que se 
      utilizan para la toma de decisiones en tiempo real.

**Organización Jerárquica y Lógica de Conocimiento**

**1. Agrupación de Conceptos:**

   ❖ Los síntomas en props representan un conjunto de condiciones 
     necesarias y suficientes para cada diagnóstico, permitiendo así 
     organizar el conocimiento en categorías de síntomas 
     interdependientes.
   ❖ Las condiciones se estructuran de modo que los diagnósticos 
      más específicos y complejos aparezcan después de evaluar 
      opciones más simples (ej., verificar carga de la batería antes de 
      sugerir cambios en el motor de arranque).

**2. Jerarquización de Reglas:**

   ❖ La jerarquía dentro de la base de conocimiento se organiza con 
diagnósticos de baja complejidad (cargar batería) primero y 
diagnósticos de alta complejidad (reparar el distribuidor) después.
   ❖ Esto permite una búsqueda progresiva y mejora la eficiencia del 
sistema al resolver primero posibles causas simples antes de 
proceder a diagnósticos complejos.

**3. Interrelación de Reglas y Síntomas:**

   ❖ Los síntomas se agrupan en conjuntos de condiciones 
      mutuamente excluyentes, como síntomas relacionados con la 
      carga de la batería y los fusibles, que definen caminos únicos de 
      diagnóstico.
   ❖ La estructura modular permite que el sistema experto agregue 
      nuevos diagnósticos en el futuro sin modificar la lógica del motor 
      de inferencia, solo ajustando o añadiendo nuevas entradas JSON.

**Inferencia de Diagnóstico**

El motor de inferencia compara la lista acumulada de positive_symptoms con 
props de cada entrada. Si encuentra una coincidencia completa, da el 
diagnóstico correspondiente. Si no hay coincidencia, se devuelve una 
respuesta indicando que no hay un diagnóstico posible en la base de 
conocimiento actual.
Esta organización y lógica garantizan que el sistema responda eficazmente, 
adaptándose a nuevos síntomas o diagnósticos y permitiendo una evolución 
constante de la base de conocimiento