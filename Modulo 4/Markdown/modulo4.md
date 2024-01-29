# Modulo 4 
1. Conceptos previos.
2. Dilema de los Generales bizantinos.
3. Teorema CAP.
4. Estructura de una blockchain.
5. Estructura de un bloque.
6. Elementos de una blockchain.
7. Beneficios y limitaciones.
8. Cuándo usar una blockchain.
9. Estructura de una dirección. 10. Mecanismos de consenso. 11. Criptomonedas.
12. Red extendida.
13. Wallets & exchanges.
14. Política monetaria de Bitcoin.
15. Nociones de computación cuántica.
16. Criptografía cuántica.
17. Criptografía post-cuántica.
18. Laboratorio: simulación del uso de una blockchain.
19. Laboratorio: ejecutar algoritmos cuánticos.

# Blockchain
## Fundamentos de Sistemas Distribuidos y Blockchain

Un sistema de cadena de bloques (Blockchain) se caracteriza por ser un sistema distribuido. En este contexto:

- **Sistema Distribuido:** Paradigma de computación donde dos o más nodos trabajan coordinadamente para lograr una meta común mediante el intercambio de mensajes.

- **Nodo:** Entidad individual (persona, computadora) en el sistema distribuido. Todos los nodos pueden enviar y recibir mensajes entre sí.

- **Tipos de Nodos:**
  - *Honestos:* Siguen el protocolo correctamente.
  - *Defectuosos:* Pueden tener fallas no maliciosas.
  - *Maliciosos:* Pueden tener comportamientos arbitrarios, conocidos como nodos bizantinos.

- **Desafíos Clave del Diseño:**
  - Coordinación entre nodos.
  - Tolerancia a fallos: El sistema debe continuar funcionando incluso si hay nodos defectuosos o interrupciones en la comunicación de red.

Estos fundamentos son esenciales para comprender cómo los sistemas distribuidos, como la cadena de bloques, operan y enfrentan desafíos en su diseño.

## Problema de los Generales Bizantinos

El Problema de los Generales Bizantinos es un experimento mental propuesto por Lamport en 1982, que presenta un escenario de guerra con generales bizantinos asediando una ciudad desde distintos lugares. Deben ponerse de acuerdo para atacar o retirarse de manera coordinada, con la única forma de comunicación siendo mediante mensajeros.

### Descripción del Problema
- **Generales:**
  - Leales: Nodos honestos.
  - Traidores: Nodos bizantinos con comportamiento arbitrario o malicioso.
- **Comunicación:**
  - Únicamente a través de mensajeros, que pueden ser capturados por la ciudad.
- **Objetivo:**
  - Los traidores buscan evitar que los generales leales se pongan de acuerdo, ofreciendo información errónea.

### Analogía con Sistemas Distribuidos
- Leales: Nodos honestos en sistemas distribuidos.
- Traidores: Nodos bizantinos con comportamiento arbitrario o malicioso.
- Mensajeros capturados: Mensajes demorados o perdidos en sistemas distribuidos.

### Desafío
Hallar un mecanismo de consenso que permita llegar a un acuerdo entre todos los generales leales a pesar de la presencia de nodos traidores y posibles mensajes capturados.

Diversas soluciones se han propuesto para abordar este desafío en sistemas distribuidos.

## Teorema CAP (Consistency, Availability, Partition Tolerance)

Se ha demostrado que un sistema distribuido no puede cumplir al mismo tiempo las propiedades deseadas de consistencia (Consistency), disponibilidad (Availability) y tolerancia a la partición (Partition Tolerance) simultáneamente. Este principio es conocido como el Teorema CAP o Teorema de Brewer.

### Propiedades:
- **Consistencia:**
  - Asegura que todos los nodos tienen una copia idéntica y actualizada de los datos.

- **Disponibilidad:**
  - Implica que los nodos están activos, accesibles y aceptando peticiones, respondiendo con datos sin fallas cuando son requeridos.

- **Tolerancia a la Partición:**
  - Significa que si un grupo de nodos es incapaz de comunicarse con otros debido a fallas en la red y/o dichos nodos, el sistema distribuido puede continuar operando correctamente.

El Teorema CAP establece que en un sistema distribuido, al enfrentarse a una partición de red (división en grupos incomunicados), es necesario sacrificar alguna de las propiedades (Consistencia o Disponibilidad) para garantizar la Tolerancia a la Partición.

## Blockchain y Bitcoin

En una blockchain, se sacrifica la consistencia en favor de la disponibilidad y la tolerancia a la partición (AP). La consistencia se logra a través de la validación de múltiples nodos en el tiempo, conocido como consistencia eventual.

En Bitcoin, la consistencia eventual se logra mediante múltiples confirmaciones de transacciones, para lo cual se introduce el proceso de minado. El minado, que utiliza el algoritmo PoW (Proof of Work), añade bloques a la blockchain.

El problema del doble gasto (usar dos veces el mismo dinero) en un entorno de completa desconfianza fue resuelto por Satoshi Nakamoto en 2008 con la introducción de la criptomoneda Bitcoin.

```md
Definición técnica de Blockchain

Es un libro de contabilidad distribuido en una red entre pares que está criptográficamente seguro, al que solo se le pueden añadir datos, inmutable (extremadamente difícil de cambiar) y actualizable solamente vía consenso entre pares.
```

## Blockchain por Capas

| Capas          | Componentes                                       |
| -------------- | ------------------------------------------------- |
| **Aplicaciones** | - Smart contracts.                                |
|                 | - Aplicaciones descentralizadas.                  |
|                 | - Organizaciones autónomas descentralizadas.     |
|                 | - Agentes autónomos.                             |
| **Ejecución**    | - Máquinas virtuales.                            |
|                 | - Bloques.                                        |
|                 | - Transacciones.                                  |
| **Consenso**     | - Replicación de la máquina de estados.           |
|                 | - Consenso basado en pruebas.                     |
|                 | - Protocolos tradicionales bizantinos tolerantes a fallas.|
| **Criptografía** | - Criptografía de clave pública.                  |
|                 | - Firmas digitales.                               |
|                 | - Funciones de hash.                              |
| **P2P**          | - Protocolos de chismes / protocolos epidémicos. |
|                 | - Protocolos de enrutamiento.                     |
|                 | - Protocolos de inundaciones.                     |
| **Network**      | - Internet.                                      |
|                 | - TCP/IP.                                         |

## Estructura Genérica de Blockchain

1. **Genesis Block:**
   - Bloque inicial de la cadena.
   - Marca el inicio de la blockchain.
   - No tiene un bloque anterior.

2. **Bloque 1:**
   - Transacciones y encabezado del bloque.
   - Hash del encabezado del bloque anterior.

3. **Bloque 2:**
   - Transacciones y encabezado del bloque.
   - Hash del encabezado del Bloque 1.

4. **y así sucesivamente...**
   - Cada nuevo bloque contiene transacciones y su encabezado.
   - Referencia al hash del encabezado del bloque anterior.

La estructura sigue este patrón a medida que se agregan nuevos bloques a la cadena.

## Estructura de un Bloque en Blockchain

- **Dirección:**
  - Identificador único en una transacción de blockchain.
  - Utilizado para identificar emisores y receptores.
  - Generalmente son claves públicas o se derivan de ellas.

- **Transacción:**
  - Representa una transferencia de valor de una dirección a otra.

- **Bloque:**
  - Múltiples transacciones.
  - Puntero al hash del bloque previo.
  - Timestamp (tiempo de creación del bloque).
  - Nonce.

- **Bloque Génesis:**
  - Primer bloque en la cadena.

- **Timestamp:**
  - Tiempo de creación del bloque.

- **Raíz de Merkle:**
  - Hash de todos los nodos en un árbol de Merkle.
  - En un bloque, es el hash combinado de todas las transacciones.
  - Se utiliza para verificar transacciones.

## Tipos de Blockchain

### Públicas
- Abiertas a cualquier persona.
- Cualquiera puede participar como nodo.
- Ejemplos: Bitcoin, Ethereum.

### Privadas
- Abiertas para un consorcio o grupo de individuos/organizaciones.
- Conocidas como blockchain de consorcios.
- Ejemplos: Hyperledger Fabric, Quorum.

### Semi Privadas
- Parte privada y parte pública.
- Conceptuales.
- Controladas por un grupo y abiertas para todos.

### Libros Contables Autorizados
- Participantes conocidos y de confianza.
- Verificación centralizada sin consenso distribuido.
- Ejemplos: Departamentos de gobierno.

### Totalmente Privadas y Propietarias
- Desviación del concepto de descentralización.
- Compartir datos con seguridad.
- Ejemplos: Departamentos de gobierno.

### Tokenizadas
- Generan criptomonedas.
- Proceso de consenso como minado o distribución inicial.

### Sin Tokens
- Solo comparten datos entre partes confiables sin transferir valores.

### Blockchain de Capa 1
- Todas las operaciones en el mismo nivel.
- Monolíticas (ej. Bitcoin, Ethereum) o no monolíticas (ej. Polkadot, Avalanche).

### Blockchain de Capa 2
- Solución a problemas de escalabilidad y privacidad.
- Consenso en la capa 1, transacciones en la capa 2.
- Ejemplos: Sidechains, zero-knowledge rollups, Lightning Networks.


## Ventajas y limitaciones de Blockchain

| Ventajas                              | Limitaciones                                   |
|---------------------------------------|-----------------------------------------------|
| - Ahorros en los costos.              | - Regulaciones.                               |
| - Simplificación en los negocios.     | - Privacidad.                                  |
| - Propiedad digital.                  | - Tecnología relativamente inmadura.         |
| - Descentralización.                  | - Interoperabilidad con otros sistemas.      |
| - Transparencia y confianza.          | - Adopción.                                   |
| - Inmutabilidad.                      |                                               |
| - Alta disponibilidad.                |                                               |
| - Alta seguridad.                     |                                               |
| - Plataforma para smart contracts.    |                                               |
| - Escalabilidad (a otras redes).      |                                               |

## ¿Cuándo usar una Blockchain?
| Pregunta                                      | Si / No | Solución recomendada                           |
|-----------------------------------------------|---------|-----------------------------------------------|
| ¿Necesita alto rendimiento de datos?            | Si      | Usar una base de datos tradicional.            |
|                                               | No      | Una base de datos centralizada puede ser útil, excepto que no pueda establecer confianza. |
| ¿Deben controlarse centralmente las actualizaciones? | Si      | Usar una base de datos tradicional.            |
|                                               | No      | Podría usar una blockchain pública o privada.  |
| ¿Confían los usuarios unos en otros?           | Si      | Usar una base de datos tradicional.            |
|                                               | No      | Usar una blockchain pública.                   |
| ¿Los usuarios son anónimos?                   | Si      | Usar una blockchain pública.                   |
|                                               | No      | Usar una blockchain privada.                   |
| ¿Se requiere que el consenso sea mantenido dentro de un grupo? | Si      | Usar una blockchain privada.                   |
|                                               | No      | Usar una blockchain pública.                   |
| ¿Se requiere estricta inmutabilidad de datos?  | Si      | Usar una blockchain.                           |
|                                               | No      | Usar una base de datos tradicional/centralizada. |

## Sistemas
| Tipo de Sistema     | Características                                                                                               |
|---------------------|---------------------------------------------------------------------------------------------------------------|
| Centralizado        | - Una autoridad única controla y gestiona todas las operaciones.                                              |
|                     | - Todos los usuarios dependen de esta única fuente de servicios.                                              |
| Distribuido         | - Replicación de datos y computación a través de múltiples nodos.                                             |
|                     | - Los usuarios ven un sistema único y coherente.                                                              |
| Descentralizado     | - Control distribuido entre varios nodos.                                                                    |
|                     | - Introducción del consenso descentralizado.                                                                 |
| Blockchain          | - Libro de contabilidad distribuido.                                                                         |
|                     | - Ejecutado sobre sistemas convencionales que incluyen almacenamiento, comunicación y computación.         |


## **Descentralización**

**Organización Descentralizada (DO)**
- Programa de software ejecutado en blockchain.
- Basada en modelo de organización real.
- Descentralizada e interactúa con otras DOs.

**Organización Autónoma Descentralizada (DAO)**
- Totalmente autónoma sin intervención humana.
- Sin fines de lucro.

**Corporación Autónoma Descentralizada (DAC)**
- Similar a DAO, pero con fines de lucro.

**Sociedad Autónoma Descentralizada (DAS)**
- Funciona en blockchain.
- Utiliza smart contracts, DAOs, DApps.

**Decentralized Applications (DApps)**
- Aplicaciones descentralizadas en blockchain.
- Pueden ser DAOs, DACs o DOs.
- Alcanzan consenso con PoW, PoS.
- Distribuyen tokens por minado, recaudación de fondos o desarrollo.

- **Clasificación:**
  - Tipo 1: Ejecutan en su propia blockchain (ejemplo: Ethereum).
  - Tipo 2: Usan blockchain existente (ejemplo: DAI en Ethereum).
  - Tipo 3: Usan protocolos de DApps Tipo 2 (ejemplo: red SAFE usando protocolos de OMNI).




## Principios fundamentales para una dApp
- Estar totalmente descentralizada.
- Ser open source / free software.
- Ser criptográficamente segura.
- Debe incentivar su disponibilidad.
- Debe dar prueba de valor mediante generación de tokens.

## **Sistemas de Almacenamiento**

La blockchain no es adecuada para grandes cantidades de datos. Se usan tablas de hash distribuidas (DTH).

**Sistemas Comunes:**
1. IPFS
2. Ethereum Swarp
3. Storj
4. MadSafe
5. BigChainDB

**Smart Contracts**
- Programa de software en blockchain.
- Ejecución segura y transparente.
- Contiene lógica de negocio y datos limitados.
- Se activa con condiciones predefinidas.

**Agentes Autónomos (AAs)**
- Entidad de software en representación de su dueño.
- Meta lograda con intervención mínima o nula del dueño.


# Bitcoin
**Introducción y Historia**

- Publicación artículo Bitcoin: 31/10/2008.
- Primera versión software: Enero de 2009 (Génesis).
- Bitcoin Pizza day: 22/05/2010 (primer uso como pago).

**Bitcoin Definición**

- Libro de contabilidad público y distribuido.
- Almacena transacciones de forma ordenada e inmutable.

**Minado en Bitcoin**

- Agrega nuevos bloques a la blockchain.
- Mineros realizan diversas tareas.
- Proceso de PoW para agregar bloques.

**Bitcoin como Solución**

- Resuelve problemas históricos: Generales bizantinos, ataques Sybil, doble gasto.

**Direcciones en Bitcoin**

- Codificadas en códigos QR.
- Wallets almacenan clave privada.

**Algoritmo de Consenso en Bitcoin**

- Todos los nodos poseen la blockchain.
- Nuevas transacciones agregadas en bloques.
- Compiten por resolver y agregar bloques (minado).

**Política Monetaria en Bitcoin**

- Emisión finita (21 millones de BTC).
- Recompensas reducidas cada cuatro años.

**Árbol de Merkle**

- Resumen de datos de bloques.
- Mantiene integridad y permite verificación eficiente.

**Tipos de Nodos en Bitcoin**

1. WM Reference Client (Bitcoin Core).
2. Solo Miner.
3. Pool Protocol Servers.
4. Full Blockchain Node.
5. Lightweight (SPV) Stratum Wallet.
6. Lightweight (SPV) Wallet.
7. Mining Nodes.

# Computación cuántica
**Introducción a la Computación Cuántica**

- Tecnología emergente que utiliza leyes de la mecánica cuántica.
- Empresas como IBM ofrecen hardware cuántico real.

**Computación Clásica vs. Cuántica**

- Problemas complejos son difíciles para supercomputadoras clásicas.
- Algoritmos cuánticos resuelven problemas complejos de manera eficiente.

**Fundamentos de la Computación Cuántica**

- Qubits: Equivalentes cuánticos de bits clásicos.
- Qubits en estado de superposición.
- Problemas de decoherencia, escalabilidad y corrección de errores.

**Máquina de Turing Cuántica**

- Modelo abstracto para computadoras cuánticas universales.
- Supremacía cuántica: Resolución de problemas específicos.
- Era actual NISQ (Noisy Intermediate Scale Quantum).

**Criterios de DiVincenzo**

- Lista de criterios para computadoras cuánticas.
- Incluye escalabilidad, decoherencia prolongada y compuertas cuánticas universales.

**Computadoras Cuánticas Comerciales**

- Rigetti, Google, IBM y Microsoft tienen ofertas comerciales.
- Características y herramientas de computadoras cuánticas comerciales.

**IBM Quantum System One**

- Primera computadora cuántica comercial para negocios e investigación.
- Presentada en enero de 2019 por IBM.

**Cálculo en Computadoras Cuánticas**

- Superposición de todos los estados posibles.
- Circuito cuántico: Interferencia selectiva para soluciones.
- IBM Qiskit: Kit de desarrollo para cálculos cuánticos.

**Circuito Cuántico**

- Rutina computacional con operaciones cuánticas y cómputo clásico.
- Representación de un circuito cuántico y ejemplo de teletransportación cuántica.

## **Qiskit Runtime**


Qiskit Runtime es un servicio de computación cuántica basado en la nube desarrollado por IBM. Ofrece primitivas computacionales para realizar tareas fundamentales de computación cuántica que utilizan técnicas integradas de supresión y mitigación de errores. Las primitivas se pueden ejecutar dentro de las sesiones, de modo que las colecciones de circuitos pueden ejecutarse conjuntamente en una computadora cuántica sin ser interrumpidas por los trabajos de otros usuarios.

### Flujo de Trabajo

1. **Construir:** Diseñar un circuito cuántico que represente el problema que está considerando.
2. **Compilar:** Compilar circuitos para un servicio cuántico específico, por ejemplo, un sistema cuántico o un simulador clásico.
3. **Ejecutar:** Ejecutar los circuitos compilados en los servicios cuánticos especificados. Estos servicios pueden estar basados en la nube o ser locales.
4. **Analizar:** Calcular estadísticas de resumen y visualizar los resultados de los experimentos.

# Criptografía cuántica

## **Criptografía Cuántica: Fundamentos**

La criptografía cuántica es la ciencia que aprovecha las propiedades de la mecánica cuántica para realizar tareas criptográficas. Incluye diversas áreas:

1. **Distribución de claves cuánticas (QKD) y cifrado cuántico:**
   - Utiliza propiedades cuánticas para asegurar la distribución segura de claves.
   - Implementa cifrado cuántico en canales de comunicación, ya sea en fibras ópticas o en espacios abiertos.

2. **Hash cuántico y firma digital cuántica:**
   - Aplica principios cuánticos en la generación de funciones hash y firmas digitales.

3. **Codificación en sistemas de transmisión de información cuántica:**
   - Emplea técnicas cuánticas para codificar y transmitir información de manera segura.

4. **Codificación súper densa cuántica de información:**
   - Utiliza partículas entrelazadas e hiperentrelazadas.
   - Permite que un qubit transporte dos bits ordinarios, incrementando el ancho de banda del canal de comunicación cuántico.
  

### Para la computación cuántica, la criptografía se divide en:

|                       | Computación Cuántica | Seguridad Criptográfica |
|-----------------------|----------------------|--------------------------|
| Cuánticamente Segura   | Algoritmos simétricos | Se duplica la longitud de las claves para mantener la seguridad cuántica. |
| Cuánticamente Insegura | Criptografía asimétrica| Considerada insegura en entornos cuánticos.                       |

## Criptoanálisis en Computación Cuántica

En el criptoanálisis cuántico, se logra una aceleración significativa en la resolución de problemas, con ejemplos notables:

- **Aceleración Exponencial:** El algoritmo de Shor es un ejemplo de esta aceleración.
- **Aceleración Cuadrática:** El algoritmo de Grover es un ejemplo de esta aceleración.

Según el NIST, varios algoritmos criptográficos tradicionales están bajo amenaza cuántica:

- AES, SHA-2, SHA-3, RSA, ECDSA, ECDH y DSA.

Se estima que hay un riesgo considerable para los algoritmos de clave pública:

- 15% de probabilidad de ser vulnerados en 2025.
- 50% de probabilidad de ser vulnerados en 2030.

#### Ejemplos de Implementación:

- En 2001, IBM implementó el algoritmo de Shor y factorizó 15 como 3 × 5 usando una computadora cuántica con 7 qubits.
- En 2012 se logró factorizar 21.
- En 2019, un intento para factorizar 35 en una IBM Q System One falló debido a la acumulación de errores.

Es importante señalar que muchos informes de factorizaciones de números más grandes involucran computación híbrida (clásica y cuántica).

### Distribución de Claves Cuánticas (QKD)

La computación cuántica representa una amenaza para el cifrado tradicional basado en las matemáticas. La QKD utiliza fotones, partículas de luz, para transferir datos y establecer una clave secreta entre dos usuarios distantes.

### Sistema QKD

El proceso implica la creación de una cadena común y aleatoria de bits secretos llamada "clave secreta". Esta se produce a través de un canal cuántico, y la validez se acuerda utilizando un canal clásico. El cifrado es "irrompible" debido a la naturaleza del transporte de datos a través de fotones, los cuales no pueden ser copiados sin dejar rastro.

### Protocolo BB84: Ejemplo

1. Alice envía fotones a Bob mediante un canal cuántico inseguro, utilizando cuatro polarizaciones.
2. Alice crea un bit aleatorio y selecciona una base aleatoria para transmitirlo.
3. Alice transmite fotones, registrando estado, base y tiempo de cada uno.
4. Bob selecciona una base aleatoria para medir los fotones recibidos.
5. Al finalizar la transmisión, Bob comunica a Alice la base seleccionada.
6. Alice comunica a Bob los fotones con resultados correctos sin revelar la polarización.
7. Alice y Bob mantienen las polarizaciones correctas, generando un "one-time pad" de Vernam.
8. Eve, intentando espiar, enfrenta la incertidumbre de la polarización sin perturbarla.
9. Alice y Bob verifican el nivel de error de la clave final para validarla, descartando datos si hay sospechas de espionaje.

### Teletransporte Cuántico (AB Par de Bell)

- Data qubit (D): Información cuántica transmitida.
- Qubit teletransportado: Qubit transferido sin transporte físico de partículas.
- Qubits entrelazados: Pares de qubits cuyos estados están vinculados de forma no local.


##  Otros Protocolos de QKD y Ataques

### Protocolos de QKD:

#### 1. E91 (Ekert 1991):
- Utiliza el entrelazamiento de pares de fotones.
- Dos qubits entrelazados comparten información de forma no local.
- Se basa en pares de Bell.

#### 2. B92 (Modificación de BB84):
- Variante del protocolo BB84.

#### 3. MDIQKD (Mayers y Yao 1998):
- Distribución de clave cuántica independiente del dispositivo de medición.

#### 4. TFQKD (Campos Gemelos 2018):
- Distribución de claves cuánticas por campos gemelos.

### Ataques sobre QKD:

#### 1. Ataques Man in the Middle (MITM):
- Vulnerabilidad cuando no se utiliza autenticación.
- La mecánica cuántica no resuelve el problema de la autenticación.

#### 2. Ataque de División del Número de Fotones:
- Utiliza pulsos láser atenuados.
- Eve puede separar fotones adicionales, comprometiendo la seguridad.

#### 3. Denegación de Servicios (DoS):
- Canales cuánticos punto a punto aumentan riesgos de DoS.

#### 4. Ataques de Troyanos:
- Eve envía luz brillante al canal cuántico y analiza los reflejos.
- Posibilidad de discernir la elección de la base secreta de Bob.

#### 5. Otros Ataques Conocidos:
- Ataques de estado falso, reasignación de fase y desplazamiento temporal.

# Criptografía Post Cuántica (PQC)

La criptografía post cuántica (PQC) se centra en desarrollar algoritmos que sean resistentes al criptoanálisis cuántico. En 2016, el NIST inició una competición para actualizar estándares e incorporar algoritmos criptográficos post cuánticos.

## Nuevos Estándares de Criptografía de Clave Pública

- NIST anunció la competición para incluir algoritmos adicionales de firma digital, cifrado de clave pública y establecimiento de claves resistentes a la computación cuántica.
- En julio de 2022, el NIST seleccionó 4 algoritmos para estandarización y 4 candidatos para mecanismos de encapsulamiento de claves (KEM) / cifrado de clave pública.

## Competición y Evaluación

- China también tiene su propio concurso a través de la Chinese Association for Cryptographic Research (CACR) con 38 candidatos.
- El NIST recibió 69 algoritmos candidatos, sometiéndolos a evaluación abierta y transparente con participación de destacados criptógrafos mundiales.
- Este proceso redujo el número de candidatos, destacando la importancia de la colaboración internacional en la búsqueda de soluciones criptográficas post cuánticas.


## Algoritmos Post Cuánticos Estandarizados

| Algoritmo              | Tipo                               | Estatus en FIPS                   |
|------------------------|------------------------------------|-----------------------------------|
| **CRYSTALS-Kyber**     | Cifrado de Clave Pública / KEM     | Cubierto en FIPS 203              |
| **CRYSTALS-Dilithium** | Firma Digital                      | Cubierto en FIPS 204              |
| **SPHINCS+**           | Firma Digital                      | Cubierto en FIPS 205              |
| **FALCON**             | Firma Digital                      | Borrador FIPS programado para 2024|
| **BIKE**               | Cifrado de Clave Pública / KEM     | En proceso de estandarización    |
| **Classic McEliece**   | Cifrado de Clave Pública / KEM     | En proceso de estandarización    |
| **HQC**                | Cifrado de Clave Pública / KEM     | En proceso de estandarización    |

Este cuadro presenta una lista de algoritmos post cuánticos estandarizados y algunos en proceso de estandarización, junto con su tipo y estado en los estándares FIPS.

### Publicaciones FIPS
Las publicaciones FIPS ofrecen detalles exhaustivos para facilitar la implementación de algoritmos en sistemas propios. En septiembre de 2022, el NIST extendió su convocatoria para algoritmos de firma digital, ya que la mayoría se basa en retículos estructurados, careciendo de suficiente variedad contra posibles ataques. En julio de 2023, anunciaron la recepción de 40 candidatos.

## Bases de los algoritmos post cuánticos

Se han propuesto varias técnicas matemáticas para construir criptosistemas cuánticos seguros, que incluyen funciones hash y pruebas simétricas de conocimiento cero, códigos de corrección de errores, retículos, ecuaciones multivariantes e isogénicas de curva elíptica supersingular.

- **SPHINCS+:** Utiliza funciones hash.
- **CRYSTALS-Kyber, CRYSTALS-Dilithium y FALCON:** Utilizan retículos.

### Open Quantum Safe (OQS)

El proyecto Open Quantum Safe (OQS) es un proyecto de código abierto que tiene como objetivo apoyar el desarrollo y la creación de prototipos de criptografía post cuántica. OQS consta de dos líneas principales de trabajo:

- **liboqs:** Una biblioteca en lenguaje C de código abierto.
- Integraciones de prototipos en protocolos y aplicaciones, incluida la biblioteca OpenSSL.
- Soporte para wrappers en C++, Go, Java, .Net, Python y Rust.

### Crystals

La Suite criptográfica para retículos algebraicos (Cryptographic Suite for Algebraic Lattices: CRYSTALS) abarca dos primitivas criptográficas:

- **Kyber:** Un mecanismo de encapsulación de claves (KEM).
- **Dilithium:** Un algoritmo de firma digital.

Ambos algoritmos se basan en problemas difíciles sobre retículos modulares y están diseñados para resistir ataques de computadoras cuánticas.

### Kyber

Se basa en la dificultad de resolver el problema de aprendizaje con errores (LWE) sobre retículos modulares. Kyber-512 apunta a una seguridad aproximadamente equivalente a AES-128, Kyber-768 a AES-192 y Kyber-1024 a AES-256. Se recomienda utilizarlo en modo híbrido en combinación con ECDH.

#### Aplicaciones
- Google (Agosto 2023) está utilizando el algoritmo Kyber-768 para proteger el tráfico en el navegador Chrome a partir de Chrome 116.
- La App Signal (Septiembre 2023) ha pasado de X3DH a PQXDH, que combina el protocolo de acuerdo de clave de curva elíptica X25519 con el mecanismo de encapsulación de clave post-cuántica (KEM) CRYSTALS-Kyber.

### Dilithium

Dilithium es un esquema de firma digital seguro bajo ataques de mensajes elegidos basados en la dificultad de los problemas de retículos modulares. La seguridad reside en que un adversario que tiene acceso a un oráculo de firma no puede producir una firma de un mensaje cuya firma aún no ha visto, ni producir una firma diferente de un mensaje que ya vio firmado. Se recomienda utilizarlo en modo híbrido en combinación con un esquema de firma "precuántico" establecido. Alcanza más de 128 bits de seguridad contra todos los ataques clásicos y cuánticos conocidos.

#### Aplicaciones
- Xiphera diseña e implementa seguridad criptográfica probada para sistemas integrados, utilizando mecanismos basados en Crystals Kyber y Crystals Dilithium.
- Castle Shield Holdings, LLC utiliza Crystals Kyber y Crystals Dilithium para su producto Aeolus VPN.

## QKD, QC y PQC

Algunas organizaciones han recomendado el uso de criptografía post cuántica (PQC) como alternativa a la distribución de claves cuánticas (QKD) debido a los problemas que plantea en el uso práctico. Las teorías publicadas sugieren que la física permite que QKD o QC detecten la presencia de un espía, una característica no proporcionada en la criptografía estándar. Sin embargo, hay desafíos y problemas asociados con QKD:


### Desafíos de QKD en Comparación con PQC

Al considerar la distribución de claves cuánticas (QKD) en relación con la criptografía post cuántica (PQC), se observan varios desafíos asociados con QKD:

a. **QKD es solo una solución parcial:**
   No proporciona un medio para autenticar la fuente de transmisión, requiriendo el uso de criptografía asimétrica o claves previas.

b. **Aumenta los costos de infraestructura y los riesgos de amenazas internas:**
   Las redes QKD con frecuencia requieren el uso de relés confiables, lo que implica un costo adicional y un riesgo de seguridad adicional.

c. **Requiere equipos de propósito especial:**
   QKD se basa en propiedades físicas, limitando su implementación y flexibilidad.

d. **Aumenta el riesgo de denegación de servicio:**
   La sensibilidad a un espía muestra que la denegación de servicio es un riesgo significativo.

e. **Asegurar y validar la QKD es un desafío importante:**
   La seguridad real proporcionada por un sistema QKD es difícil de validar y puede introducir vulnerabilidades en el hardware específico utilizado.
