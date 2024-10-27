<a id="readme-top"></a>
# Documentación de QuickStatements (QS) 3.0

<details>
 <summary>Traducciones:</summary>
 <ul>
  <li><a href="translations/qts-index-fr.md">Francés</li>
  <li><a href="translations/qts-index-pt.md">Portugués</li>
  <li><a href="translations/qts-index-es.md">Español</li>
 </ul>
</details>
<a href="#mentor-feedback">Implementaciones Basadas en Retroalimentación de los Mentores</a>

## Índice
<!-- TABLA DE CONTENIDO -->
<details>
  <summary>Índice</summary>
  <ol>
    <li><a href="#overview">Visión General de QuickStatements</a></li>
    <li><a href="#a-brief-on-wikidata">Breve Introducción a Wikidata</a>
      <ul>
        <li><a href="#structure-of-wikidata">Estructura de Wikidata</a></li>
        <li><a href="#lda">Etiquetas, Descripciones y Alias</a></li>
        <li><a href="#wiki-statements">Declaraciones en Wikidata</a></li>
        <li><a href="#syntax-and-command-structure">Sintaxis y Estructura de Comando</a></li>
      </ul>
    </li>
    <li><a href="#qs-v3-docs">Documentación de QuickStatements 3.0</a>
      <ul>
        <li><a href="#prerequisites">Comenzando: Requisitos Previos</a></li>
        <li><a href="#qs-3.0-homepage">Visión General de la Página Principal de QuickStatements 3.0</a></li>
        <li><a href="#what-is-a-batch">Guía: ¿Qué es un Lote?</a>
          <ul>
            <li><a href="#create-new-batch">Crear un Nuevo Lote</a></li>
            <li><a href="#details-of-a-batch">Detalles de un Lote</a></li>
          </ul>
        </li>
        <li><a href="#batch-details">Visualización de Detalles e Historial de Lotes</a></li>
        <li><a href="#batches-per-user">Ver todos los Lotes Creados por un Usuario</a></li>
        <li><a href="#writing-batch-commands">Escribir Comandos de Lote</a>
          <ul>
            <li><a href="#create-new-item">Crear un Nuevo Elemento</a>
            <li><a href="#add-statements">Añadir Declaraciones</a>
            <li><a href="#add-qualifiers">Añadir Calificadores</a> 
            <li><a href="#add-references">Añadir Referencias</a>
            <li><a href="#modify-lda">Modificar Etiquetas, Descripciones y Alias</a>
            <li><a href="#remove-items">Eliminar Declaraciones o Elementos</a>
            <li><a href="#import-data">Importar Datos CSV/TSV</a>                                                                  </ul>
        </li>
        <li><a href="#best-practices">Mejores Prácticas</a></li>
        <li><a href="#error-handling">Manejo de Errores</a></li>
        <li><a href="#recommendations">Recomendaciones</a></li>
        <li><a href="#conclusion">Conclusión</a></li>
      </ul>
    </li> 
  </ol>
</details>

## Visión General

**QuickStatements (QS)** es una herramienta poderosa diseñada por [Magnus Manske](https://en.wikipedia.org/wiki/User:Magnus_Manske) para realizar ediciones masivas en Wikidata. Permite a los usuarios agregar, modificar o eliminar grandes cantidades de datos de manera eficiente, utilizando una sintaxis simple, similar a una línea de comandos. Ya sea que estés agregando nuevos elementos, declaraciones o actualizando propiedades en múltiples entidades, QuickStatements es una herramienta esencial para los editores de Wikidata que necesitan hacer cambios a gran escala de manera rápida y confiable.

Esta documentación proporciona una introducción a las características, uso y mejores prácticas de QuickStatements 3.0. _[Haz clic](#qs-v3-docs)_ para comenzar. Sin embargo, para comprender completamente las funcionalidades de QuickStatements 3.0, es importante entender primero el principal componente de QuickStatements⎯ ```Wikidata.```

#

<a id="a-brief-on-wikidata"></a>
<details>
<summary> Breve Introducción a Wikidata</summary>
Wikidata es una base de datos gratuita, colaborativa, multilingüe y secundaria, gestionada por la Fundación Wikimedia. Sirve como un almacenamiento central de datos estructurados que se utiliza en varios proyectos Wikimedia, como Wikipedia, y también proporciona datos a usuarios y organizaciones externas. El objetivo principal de Wikidata es permitir que humanos y máquinas comprendan y consulten información de manera fácil.

Algunas características clave incluyen:

- **Soporte multilingüe:** Los datos se almacenan de manera que pueden ser accedidos en cualquier idioma.
- **Datos abiertos:** Los datos de Wikidata están disponibles bajo la Licencia de Dominio Público de Creative Commons (CC0).
- **Edición colaborativa:** Cualquiera con una cuenta puede editar Wikidata, haciéndolo un recurso impulsado por la comunidad.
- **Enlace de datos:** Wikidata se integra con otros proyectos Wikimedia, sirviendo como la fuente de datos consistente y actualizada.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

<a id="structure-of-wikidata"></a>
## Estructura de Wikidata
La estructura de Wikidata se basa en un modelo simple pero poderoso de **elementos**, **propiedades** y **valores**. Estos tres componentes forman la columna vertebral de cómo se almacenan, enlazan y recuperan los datos.

- **Elementos (números Q):** Cada elemento es un concepto único representado por un **QID** (por ejemplo, Douglas Adams está representado por Q42). Estos elementos almacenan datos y se vinculan a otros elementos.

- **Propiedades (números P):** Las propiedades describen atributos específicos de un elemento y se identifican mediante **PIDs** (por ejemplo, la fecha de nacimiento se representa por **P569**). Las propiedades pueden describir relaciones entre elementos o entre un elemento y un valor de datos.

- **Valores:** Estos son los puntos de datos reales (por ejemplo, la fecha **1952-03-11** como valor para **P569** en el elemento **Q42** para la fecha de nacimiento de Douglas Adams).

Juntos, los elementos, propiedades y valores crean **declaraciones**, que son los componentes básicos de Wikidata.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

<a id="lda"></a>
## Etiquetas, Descripciones y Alias
Cada elemento en Wikidata puede tener múltiples **etiquetas**, **descripciones** y **alias** en diferentes idiomas:

- **Etiquetas:** Una etiqueta es el nombre principal de un elemento (por ejemplo, “Douglas Adams” para **Q42**). Un elemento puede tener una etiqueta diferente en cada idioma.

- **Descripciones:** Las descripciones proporcionan contexto sobre el elemento para diferenciarlo de elementos similares (por ejemplo, “Autor y guionista británico” para **Q42**).

- **Alias:** Los alias son nombres alternativos para un elemento que se utilizan para fines de búsqueda. Por ejemplo, **Q42** (Douglas Adams) podría tener un alias como "Douglas Noel Adams."

Estos tres componentes ayudan a garantizar que los elementos sean fáciles de encontrar, distinguir y acceder en una variedad de idiomas y contextos.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

<a id="wiki-statements"></a>
## Declaraciones en Wikidata
**Las declaraciones** son las unidades de conocimiento clave en Wikidata, utilizadas para describir elementos a través de una combinación de una propiedad y un valor. Una declaración conecta un elemento con sus datos asociados:

- **Propiedad:** Define qué aspecto del elemento estás describiendo (por ejemplo, fecha de nacimiento, ocupación, nacionalidad).
- **Valor:** Proporciona la información específica (por ejemplo, una fecha, una cadena de texto o una referencia a otro elemento).
Una declaración también puede tener **calificadores** y **referencias** para proporcionar más contexto o citar la fuente de los datos.

Por ejemplo:

- **Elemento:** Douglas Adams (Q42)
- **Propiedad:** Fecha de nacimiento (P569)
- **Valor:** 11 de marzo de 1952
- **Calificador:** Fuente (S854) – Enlace a una página web o base de datos que proporciona prueba de la declaración.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

<a id="syntax-and-command-structure"></a>
## Sintaxis y Estructura de Comando

Cada comando de QuickStatements sigue un formato simplificado con columnas que especifican el **Elemento**, **Propiedad**, **Valor** y opcionales **Calificadores**, **Referencias**, etc.

| Campo        | Descripción                                                                                     |
|--------------|-------------------------------------------------------------------------------------------------|
| `Q####`      | Se refiere a un elemento (por ejemplo, `Q42` para Douglas Adams).                               |
| `P####`      | Se refiere a una propiedad (por ejemplo, `P31` para "instancia de").                            |
| Valor        | El valor asociado a la propiedad. Puede ser una referencia a un elemento (por ejemplo, `Q####`), texto, número, etc. |
| Calificador  | Información adicional añadida a una afirmación para darle más contexto (por ejemplo, tiempo, lugar).|
| Referencias  | Datos para respaldar una afirmación (por ejemplo, una URL, fecha de publicación).               |
| Etiquetas    | Nombres o títulos de los elementos en diferentes idiomas.                                       |
| Descripciones| Breves resúmenes que describen los elementos.                                                   |
| Alias        | Nombres o términos alternativos por los que se conoce un elemento.                              |

</details>

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

#

<a id="qs-v3-docs"></a>
## Documentación de QuickStatements 3.0

Esta documentación proporciona una introducción a las características de QuickStatements 3.0, que es una actualización que mejora la funcionalidad, rendimiento y experiencia del usuario de la plataforma QuickStatements para mejorar la estabilidad del sistema.

#

### Requisitos Previos
Para crear y ejecutar lotes, debes asegurarte de lo siguiente:
- **Cuenta en Wikidata**: Debes estar registrado en Wikidata para usar QuickStatements.
- **Datos Estructurados**: Tus datos deben estar bien estructurados en formato CSV/TSV o similar para ser fácilmente importados y procesados.
- **Usuario autoconfirmado**: Para ser un usuario autoconfirmado, debes tener al menos 4 días en la plataforma y haber realizado 50 ediciones.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

<a id="qs-3.0-homepage"></a>
## Visión General de la Página Principal de QuickStatements 3.0
La página principal de **QuickStatements 3.0** está diseñada para facilitar el acceso a las funciones principales para gestionar y ejecutar ediciones en lotes. A continuación, se muestra un desglose de los elementos visibles:

<p align="center">
  <img src="https://github.com/user-attachments/assets/339297cb-b5e4-46ca-82d1-799ea0b964dd" alt="Página Principal de QuickStatements 3.0" />
  <p align="center">Página Principal de QuickStatements 3.0</p>
</p>

#### Menú de Navegación:
1. **Nuevo lote:** Un enlace que te lleva a un formulario donde puedes crear un nuevo lote de ediciones para ser cargadas en Wikidata.

2. **Últimos lotes:** Este enlace proporciona acceso al historial de lotes enviados recientemente. Los usuarios pueden rastrear el estado y los detalles de sus operaciones de lote pasadas.

3. **Git:** Enlaces al [repositorio de QuickStatements en GitHub](https://github.com/WikiMovimentoBrasil/quickstatements3), donde los usuarios pueden ver el código, reportar problemas o contribuir al desarrollo de la plataforma.
  
4. **Iniciar sesión:** Permite a los usuarios iniciar sesión en sus cuentas de Wikidata. Una vez que inicies sesión, puedes acceder a funciones como enviar y rastrear tus envíos de lotes.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

#### Interfaz Principal:
5. **“Bienvenido a QuickStatements 3.0”:** Un encabezado que da la bienvenida a los usuarios a la interfaz principal.

#### Botones de Acción Principales:

6. **Nuevo lote:** Al hacer clic en este botón, se inicia la creación de un nuevo lote. Los usuarios pueden ingresar datos y comandos para procesar y cargar múltiples ediciones en Wikidata de forma masiva.
  
#### Sección de Búsqueda de Lotes:
7. **ID de Lote:** Los usuarios pueden ingresar un ID de lote específico para recuperar información detallada sobre ese lote en particular. Al hacer clic en el botón ```Ver detalles del lote``` se muestra el estado, progreso y resultados del lote.

8. **Nombre de usuario:** Los usuarios pueden ingresar un nombre de usuario específico de Wikidata para recuperar una lista de todos los lotes asociados con ese usuario. Al hacer clic en ```Ver lotes por usuario``` se mostrarán todos los lotes enviados por ese usuario.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

#
  
<a id="what-is-a-batch"></a>
### ¿Qué es un Lote en QuickStatements?
Un **lote** se refiere a un conjunto de comandos u operaciones que se ejecutan juntos para realizar ediciones masivas. Cada lote puede incluir múltiples declaraciones o afirmaciones que deseas agregar, modificar o eliminar de los elementos en Wikidata.

#

<a id="create-new-batch"></a>
#### A. Creación de un Nuevo Lote en QuickStatements
Para crear un nuevo lote en QuickStatements, sigue estos pasos:
1. Haz clic en el botón ```Nuevo Lote``` ubicado en la página principal

<p align="center">
  <img src="https://github.com/user-attachments/assets/d153bc61-0d95-4d32-b48e-876e1009f908" alt="Página Principal de QuickStatements 3.0" />
  <p align="center">Haz clic en Nuevo Lote</p>
</p>

2. Aparecerá un formulario donde puedes ingresar tus comandos o cargar tu archivo de datos. Los formatos disponibles incluyen tanto el formato V1 de QuickStatements como el formato CSV/TSV.
<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

#

<a id="details-of-a-batch"></a>
#### B. Detalles de un Lote en QuickStatements

<p align="center">
  <img src="https://github.com/user-attachments/assets/e81cd5a6-e029-454c-b4d6-67b7e607b920" alt="Detalles de un Nuevo Lote en QuickStatements 3.0" />
  <p align="center">Detalles de un Nuevo Lote</p>
</p>

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

Un nuevo lote consiste en:
1. **Formato de comando:** Tu formato de comando puede estar en formato V1 o CSV.
     - **Formato V1:** Formato basado en comandos donde cada línea representa un comando separado por tabulaciones.
     - **Formato CSV:** Consiste en una primera línea⎯el encabezado⎯que define el contenido de cada columna. Las líneas posteriores suministran información para ser aplicada a Wikibase de acuerdo con el contenido del encabezado de cada columna.
  
Ejemplo de sintaxis V1:
```
CREATE
LAST Len Doctor Worm
LAST Den 1998 canción interpretada por They Might Be Giants
LAST P2650 Q128309
```

Ejemplo de sintaxis CSV:
```
qid,Len,Den,P31
,Regina Phalange,fictional character,Q95074
```

QuickStatements también se puede ejecutar a través de URL. 
```Ver ejemplo: 
https://quickstatements.toolforge.org/#/v1=Q37887397%7CP214%7C%2296480189%22%7CS143%7CQ565 
Qid: Q37887397 
Propiedad: P214 
Senwiki: S143 
Valor: Q565
```

2. **Nombre personalizado del lote:** Este es un rótulo o identificador que puedes asignar a un lote específico de ediciones para facilitar su gestión y referencia. Por defecto, los lotes reciben nombres genéricos, típicamente solo un ID de lote. Sin embargo, tienes la opción de proporcionar un nombre personalizado al crear o cargar un lote. Este nombre personalizado facilita el reconocimiento o la recordación del propósito de un lote específico, especialmente al trabajar con varios lotes a lo largo del tiempo.

3. **Comandos:** Son las instrucciones que ingresas para realizar operaciones específicas en los elementos de Wikidata. Estos comandos te permiten agregar, modificar o eliminar datos de elementos en Wikidata. Los comandos se escriben en un formato específico, y cada línea generalmente representa una acción a realizar en un elemento de Wikidata.
<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## Visualización de Detalles e Historial de Lotes
Puedes rastrear el progreso y el estado de un lote específico ingresando el **ID de Lote** en el campo correspondiente y haciendo clic en el botón **Ver detalles del lote**. Esto muestra información como el número de ediciones realizadas, el éxito o fracaso de las operaciones y cualquier error que haya ocurrido.

#

<a id="batches-per-user"></a>
#### C. Ver todos los Lotes por Usuario en QuickStatements
Para ver el historial de ediciones en lote de un usuario específico:
1. Ingresa el ```nombre de usuario``` del usuario en el campo de nombre de usuario (el nombre de usuario se encuentra en el login de wiki).
2. Haz clic en ```Ver lotes por usuario``` para listar todos los lotes que el usuario ha enviado. La lista incluirá:
 - **ID de los Lotes**
 - **Descripciones (si agregaste nombres personalizados)**
 - **Estado (por ejemplo, en progreso, completado o fallido)**
 - **Fechas**
 - **Número de ediciones en el lote**

> [!NOTE]
> Cada lote tiene una URL única asociada. Puedes marcar esta URL o compartirla para acceder o monitorear un lote más tarde.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

#

<a id="writing-batch-commands"></a>
#### D. Escribir Comandos de Lote en QuickStatements

<a id="create-new-item"></a>
#### 1. Crear un Nuevo Elemento

Este comando creará un nuevo elemento con una etiqueta y descripción.

```plaintext
CREATE
LAST  Len  "Elemento Ejemplo"
LAST  Den  "Este es un elemento de ejemplo para fines de demostración."
LAST  P31  Q5  # Agrega una afirmación de que el elemento es una instancia de humano
```

<a id="add-statements"></a>
#### 2. Añadir Declaraciones (Afirmaciones)
Agregar declaraciones a un elemento existente (por ejemplo, Douglas Adams - Q42).

```
Q42  P569  1952-03-11  # Agrega la fecha de nacimiento (P569) de Douglas Adams
Q42  P19  Q84          # Agrega el lugar de nacimiento (P19) como Cambridge (Q84)
```

<a id="add-qualifiers"></a>
#### 3. Añadir Calificadores

Puedes añadir calificadores a declaraciones existentes para proporcionar más detalles.
```
Q42  P69  Q3918  P580  1971  P582  1974  # Agrega educación (P69) en St John's College (Q3918) con fechas de inicio (P580) y fin (P582)
```

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

<a id="add-references"></a>
#### 4. Añadir Referencias

Agregar referencias a una declaración existente:
```
Q42  P69  Q3918  S854  "https://example.com/educacion"  # Agrega una URL de referencia para la afirmación de educación
```

<a id="modify-lda"></a>
#### 5. Modificar Etiquetas, Descripciones y Alias
Modificar etiquetas, descripciones y alias en diferentes idiomas:
```
Q42  Len  "Douglas Adams"  # Cambia la etiqueta en inglés a "Douglas Adams"
Q42  Ade  "Douglas Adams"  # Cambia la etiqueta en alemán a "Douglas Adams"
Q42  Aen  "Douglas Noel Adams"  # Agrega un alias en inglés
Q42  Den  "Autor y guionista británico"  # Modifica la descripción en inglés
```

<a id="remove-items"></a>
#### 6. Eliminar Declaraciones o Elementos
Eliminar declaraciones o eliminar elementos por completo:
```
-Q42  P19  # Elimina la declaración de lugar de nacimiento (P19) para Q42
-Q100000  # Elimina el elemento completo Q100000
```

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

<a id="import-data"></a>
#### 7. Importar Datos CSV/TSV
Puedes preparar tus datos en formato CSV o TSV, donde cada línea representa una operación. Un formato de ejemplo:
```
Q42,P69,Q3918,P580,1971,P582,1974
Q42,P19,Q84
Q42,P569,+1856-01-01T00:00:00Z/9
```
Carga el archivo a través de la interfaz web para procesar el lote.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

#

### Mejores Prácticas
- **Prueba con Lotes Pequeños:** Siempre prueba tus comandos con un conjunto pequeño de elementos antes de realizar ediciones a gran escala para evitar cambios no deseados.
- **Usa Referencias:** Asegúrate de que las declaraciones estén correctamente respaldadas con referencias para mejorar la calidad de los datos.
- **Monitorea el Progreso:** Después del envío, sigue el progreso de tu lote y verifica si hay errores.

#

### Manejo de Errores
Cuando ocurre un error durante la ejecución, QuickStatements indicará cuál comando falló. Los problemas comunes incluyen:

- IDs de elementos o propiedades incorrectos.
- Errores de sintaxis en formatos de fecha o campos de datos faltantes.
- Permisos o limitación de velocidad de Wikidata para ediciones a gran escala. En estos casos, revisa los comandos fallidos y corrige los problemas antes de volver a ejecutarlos.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

#

### Conclusión
QuickStatements es una herramienta esencial para la edición masiva en Wikidata, permitiendo a los usuarios gestionar grandes conjuntos de datos de manera eficiente. Siguiendo esta guía, puedes crear, actualizar y gestionar elementos con facilidad, mejorando la calidad y precisión de Wikidata.

Para casos de uso más avanzados, consulta la [documentación de Wikidata](https://www.wikidata.org/wiki/Help:QuickStatements) para obtener más detalles y actualizaciones.

#

### Referencias
Esta documentación se inspiró en muchas fuentes; sin embargo, [Diátaxis](https://diataxis.fr/) fue la guía más significativa para escribir esto, ya que proporciona un enfoque sistemático para comprender las necesidades de los usuarios de la documentación. El [Curso de Escritura Técnica de Google](https://developers.google.com/tech-writing/overview) también fue fundamental.

#

<a id="mentor-feedback"></a>
### Modificaciones e Implementaciones Basadas en la Retroalimentación de los Mentores

| Retroalimentación                                         | Modificaciones                                         | Ubicación                    |
|--------------------------------------------------|-------------------------------------------------------|-----------------------------|
| Tienes más de 200 commits                  | Los commits largos han sido comprimidos para mantener el historial limpio | Historial del repositorio          |
| El comando DELETE no existe en QuickStatements  | El comando ha sido rectificado en todas las traducciones                      | [Eliminar Elementos](#remove-items) |
| Tus imágenes hacen que la documentación sea fácil de entender | Se mejoraron las imágenes para mayor claridad                | Todas las imágenes               |

## ️💚️ GRACIAS MENTORES 💙 
<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- prettier-ignore -->
| [<img src="https://github.com/user-attachments/assets/1deb350c-3202-48b3-bef2-ead6c6f9a06d" width="100px;"/><br /><sub><b>Ederporto, EPorto (WMB)</b></sub>](https://phabricator.wikimedia.org/p/Ederporto/)<br />        | [<img src="https://github.com/user-attachments/assets/4d0112e0-00b8-421d-a043-67282f13d413" width="100px;"/><br /><sub><b>Artur Corrêa Souza</b></sub>](https://phabricator.wikimedia.org/p/ACorrea-WMB/)<br /> | [<img src="https://github.com/user-attachments/assets/b8c0a206-9e85-4b2c-a41d-13986e126565" width="100px;"/><br /><sub><b>MGalves (WMB)</b></sub>](https://phabricator.wikimedia.org/p/MGalves_WMB/)<br />          |
| :---------------------: | :-----------------------: | :--------------------: |
<p align="right">(<a href="#readme-top">volver arriba</a>)</p>
<!-- ALL-CONTRIBUTORS-LIST:END -->
