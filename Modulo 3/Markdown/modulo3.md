# Modulo 3
1. Funciones resumen (hash).
2. Algoritmos de hash.
3. Códigos de autenticación de mensajes (MAC).
4. Funciones derivadoras de clave (KDF).
5. Firmas digitales.
6. Algoritmos de firmas digitales.
7. Esteganografía.
8. Laboratorio: atacar algoritmos cifrados. 9. Laboratorio: descubrir malwares ocultos.

# Funciones de Hash 
Es un algoritmo que convierte un mensaje de cualquier tamaño, en un array de bits de tamaño fijo y pequeño

Un buen hash debe verificar: 
- Ser determinístico (el mismo mensaje produce el mismo hash).
- Ser irreversible (debe ser extremadamente dificultoso o imposible recuperar el mensaje original a partir de su hash).
- Debe ser computacionalmente inviable hallar dos mensajes con el mismo hash (colisión).
- Cualquier cambio en el mensaje, por mínimo que sea, debe resultar en un extenso cambio en el hash para que sea imposible relacionar los mensajes con sus hashes (efecto avalancha).
- Debe ser muy fácil de calcular.

## Aplicaciones de Criptografía

La criptografía desempeña un papel crucial en diversas áreas, brindando seguridad y confiabilidad. Algunas de sus aplicaciones clave incluyen:

- **Verificación de integridad de datos:** Garantiza que la información no ha sido alterada durante la transmisión o almacenamiento.

- **Códigos de autenticación de mensajes (HMAC):** Se basan en funciones hash para proporcionar autenticación segura en la comunicación.

- **Firmas digitales:** Utilizadas para verificar la autenticidad y la integridad de documentos electrónicos.

- **Protocolos de red (TLS, SSH):** Garantizan la seguridad en la transmisión de datos a través de redes.

- **Verificación de contraseñas:** Almacenamiento seguro y verificación de contraseñas mediante técnicas criptográficas.

- **Identificador de contenidos:** Empleado en sistemas de administración de código fuente como GIT y Mercurial para identificar y asegurar versiones de código.

- **Blockchain y criptomonedas:** Uso de hashes criptográficos para encadenar bloques de datos y garantizar la seguridad en transacciones.

- **Pruebas de trabajo:** Aplicadas en el minado de criptomonedas y la prevención de ataques de denegación de servicio y spam.

Estas aplicaciones demuestran la versatilidad y relevancia de la criptografía en la seguridad informática.

## Seguridad de las funciones de hash
La seguridad de una función de hash radica en su resistencia a ataques

Los principales tipos de ataque posibles son:
- Ataques de colisión: 
  - Intenta hallar dos mensajes que produzcan el mismo hash.
  - Un ataque de colisión es mucho más sencillo de implementar que un ataque de preimagen, porque la búsqueda del mensaje no se limita a un solo objetivo.
  - La base de estos ataques es la paradoja del cumpleaños.

- Ataques de preimagen: 
Intenta hallar un mensaje que produzca un hash predefinido.

### Nivel de seguridad
- El nivel de seguridad de una función hash es la complejidad computacional del ataque de colisión. Se mide en bits de seguridad, y depende del tamaño del hash.

`Por ejemplo: para SHA-256, la resistencia contra el ataque de colisión es 128 bits y contra el ataque de preimagen, 256 bits.`

```js
Niveles de seguridad recomendados por NIST: 
● 112 bits de seguridad: deberían ser suficientes
hasta 2030.
● 128 bits de seguridad: deberían ser suficientes hasta la próxima revolución tecnológica o matemática.
```

### Paradoja del Cumpleaños

Sea **P** la probabilidad de que una persona cumpla años el mismo día que yo. ¿Cuántas personas deben estar en una habitación para que P sea igual o mayor al 50%?

La probabilidad se define como:
```markdown
P = 1 – (364/365)^n
```
Donde podemos estimar que para P=0,50, resulta:

```md
n >= 253
```
Esto se relaciona con funciones hash al considerar las personas como mensajes y sus cumpleaños como hashes. La paradoja se reinterpretaría como:
“La cantidad de mensajes que debo intentar criptoanalizar por fuerza bruta para encontrar dos hashes iguales”.

Es el ataque de la preimagen. La cantidad de hashes que debo calcular es aproximadamente el 70% de todas las claves.

### Paradoja del Cumpleaños Modificada
Sea P la probabilidad de que dos personas cumplan años el mismo día

¿Cuántas personas deben estar en una habitación para que P sea igual o mayor al 50%?

La probabilidad para n >= 2 es:

```md
P = 1 – [364x363x...x(365-n+1)]/365^(n-1)
```
Estimamos que, para P=0,50, resulta:
```md
n >= 22
```
Nuevamente, pensando en personas como mensajes y cumpleaños como hashes, reinterpretamos esto como:
“La cantidad de mensajes cuyos hashes debo calcular para encontrar dos hashes iguales que provengan de dos mensajes distintos”.

Es el ataque de colisión. La cantidad de hashes que debo calcular es aproximadamente el 6% de todas las claves disponibles en el espacio de claves del algoritmo.

# Algoritmos de funciones hash
En las próximas slides, veremos en detalle los
siguientes algoritmos: 
- FamiliaSHA-2.
- FamiliaSHA-3.
- Otros algoritmos.

## Familia SHA-2

Desarrollados por la NSA y publicados en 2001 por el NIST, los algoritmos de la familia SHA-2 son seguros y ampliamente utilizados. Incluyen:

- **SHA-256:** Hash de 256 bits con nivel de seguridad de 128 bits.
- **SHA-224:** Modificación de SHA-256 con salida truncada a 224 bits.
- **SHA-512:** Similar a SHA-256 pero para palabras de 64 bits, con salida de 512 bits.
- **SHA-384, SHA-512/256 y SHA-512/224:** Modificaciones de SHA-512 con tamaños de hash y resistencias a la colisión específicos.

## Familia SHA-3

Sucesora de SHA-2, la familia SHA-3 se basa en principios diferentes y fue publicada en 2014. Algunos detalles:

- Algoritmo ganador: Keccak.
- No obsoletos, complementan a SHA-2.
- Funciones notables: SHA3-224, SHA-256, SHA3-384, SHA-512, SHAKE128, SHAKE256.
- SHAKE128 y SHAKE256 son funciones de salida extensible (XOF).

## Otros Algoritmos

### SHA-1 y SHA-0
- SHA-1 desarrollado en 1993, obsoleto en 2017.
- SHA-0 fue la versión anterior de SHA-1.

### Familia MD (Message Digest)
- MD2, MD4, MD5, y MD6.
- MD5 fue popular antes de ser reemplazado por SHA-1.

### Familia BLAKE2
- Incluye BLAKE2s y BLAKE2b.
- Rápidos y con mayor margen de seguridad que SHA-2.
- Sucesor: BLAKE3, lanzado en 2020.

### GOST (GOvernment STandards)
- GOST94 y su sucesor

## ¿Qué algoritmo utilizar?
| Requerimiento                                            | Algoritmo                            |
|----------------------------------------------------------|--------------------------------------|
| Ningún requerimiento especial.                           | SHA3-256                             |
| Necesitas más compatibilidad e interoperabilidad.        | SHA-256 de la familia SHA-2          |
| Debes estar preparado para migrar ante la computación cuántica. | SHA-3                             |
| Necesitas más velocidad, seguridad, sin preocuparte por interoperabilidad. | BLAKE2b con hash de 512 bits  |


# Códigos de autenticación de mensajes (MAC)
## MAC
**Un código de autenticación de mensajes (MAC, Message Authentication Code) es un array corto de bits, usados para autenticar un mensaje.** Se conocen también como etiquetas de autenticación.

## Resumen de Características e Implementación de MAC

- **Generación del MAC:**
  - El emisor necesita un mensaje y una clave secreta.
  - Se utiliza para autenticar el origen del mensaje y garantizar su integridad.

- **Verificación del MAC:**
  - El receptor necesita el mensaje y la misma clave secreta.
  - Permite al receptor confirmar la autenticidad del mensaje y su integridad.

- **Diferencias con la Firma Digital:**
  - A diferencia de la firma digital (que usa criptografía asimétrica), los MAC no requieren claves distintas para emisor y receptor.
  - La firma digital proporciona no repudio además de autenticación.

- **Aplicaciones:**
  - Utilizados en protocolos de red para garantizar integridad y autenticidad de datos transmitidos.
  - Empleados en cifrado general.
  - Base de funciones derivadoras de clave, como PBKDF.

- **Clases de Funciones MAC:**
  - Diversidad de funciones MAC disponibles.
  - Destacan los HMAC (códigos de autenticación basados en hash) en protocolos seguros de red.

Los MAC son esenciales para garantizar la autenticación e integridad de los datos en protocolos de red, así como en aplicaciones de cifrado y funciones derivadoras de clave. La utilización de HMAC es común para lograr estos objetivos.

##  Seguridad en MAC

Un MAC se considera seguro si puede resistir los siguientes ataques:

- **Ataque de Falsificación Universal:**
  - Un atacante crea un MAC válido para cualquier mensaje.

- **Ataque de Falsificación Selectivo:**
  - El atacante produce el MAC correcto para un mensaje particular, elegido previamente al ataque.

- **Ataque de Falsificación Existencial:**
  - El atacante puede relacionar cualquier mensaje con su MAC.

- **Ataque de Falsificación Existencial a un Mensaje Elegido:**
  - El atacante puede enviar mensajes a un oráculo para que este genere un MAC, analizando el comportamiento del oráculo.

El nivel de seguridad del MAC se mide en bits, dependiendo de las funciones criptográficas y de la clave secreta utilizada.

Los códigos de autenticación de mensajes basados en hash (HMAC) utilizan una función hash y una clave secreta. La función no es compleja:

```plaintext
HMAC(K, message) = H(K' XOR opad || H(K' XOR ipad || message))
```
## Detalles de la Función HMAC

| Elemento          | Descripción                                                                                     |
|-------------------|-------------------------------------------------------------------------------------------------|
| H                 | La función hash utilizada, por ejemplo, SHA3-256.                                                |
| K                 | La clave secreta.                                                                               |
| K'                | La clave derivada de K del tamaño de bloque adecuado dependiendo del tamaño B del bloque interno de la función H. |
| ipad              | El padding interno, consiste en el byte 0x36 repetido B veces.                                   |
| opad              | El padding externo, consiste en el byte 0x5C repetido B veces.                                   |
| \|\|              | Representa una concatenación.                                                                   |

La fórmula HMAC se expresa como:

```plaintext
HMAC(K, message) = H(K' XOR opad || H(K' XOR ipad || message))
```

##  Seguridad en HMAC

- **Nomenclatura:**
  - Una HMAC que utiliza SHA-256 se denomina HMAC-SHA-256.

- **Nivel de Seguridad:**
  - El nivel de seguridad es el mínimo entre la longitud de la clave secreta y la del hash, medido en bits.
  - Ejemplo: HMAC-SHA-256 con clave de 256 bits tiene seguridad de 256 bits.

- **Fortaleza de la Clave Secreta:**
  - La seguridad de la clave secreta depende de su entropía.
  - Una clave generada aleatoriamente con un generador criptográficamente seguro tiene seguridad igual a su longitud.

- **Consideraciones sobre la Entropía:**
  - Si el generador aleatorio tiene sospecha de aleatoriedad débil, se debe duplicar el tamaño de la clave.
  - Si la clave se deriva de una fuente de baja entropía (como una contraseña), la seguridad de la HMAC se degrada a la entropía de la contraseña.

## Esquemas de Uso de MAC con Cifrado

Los esquemas más comunes de uso de los MAC con cifrado son:

1. **EtM (Encrypt-then-MAC):**
   - Se cifra el texto claro.
   - Se calcula el MAC sobre el texto cifrado.
   - Se envían juntos el MAC y el criptograma.

2. **E&M (Encrypt-and-MAC):**
   - Se cifra el texto plano.
   - Se calcula el MAC sobre el texto plano.
   - Se envían juntos el MAC y el criptograma.

3. **MtE (MAC-then-Encrypt):**
   - Se calcula el MAC sobre el texto plano.
   - Se concatenan el MAC y el texto plano.
   - Se cifran juntos.

Los investigadores en seguridad recomiendan EtM como el esquema más seguro.

Además, dos esquemas ganando popularidad son:

- **AES-GCM:**
  - Modo de cifrado autenticado que no requiere HMAC.

- **ChaCha20-Poly1305:**
  - Otro modo de cifrado a

# Funciones derivadoras de claves (KDF)
## KDF: Key Derivation Function
Una contraseña o una frase de paso son legibles por humanos y no se pueden usar directamente en un algoritmo de cifrado. `Tenemos que usar una clave derivada de la contraseña/frase de paso.`

## Cuadro de Funciones KDF

| Término                        | Descripción                                     |
|-------------------------------|-------------------------------------------------|
| **1 IKM (Input Key Material)**  | Materias primas de entrada para la KDF.         |
| **2 KDF (Key Derivation Function)** | Función derivadora de clave.                 |
| **3 OKM (Output Key Material)** | Material de clave generado como salida de la KDF.|

## Detalles Adicionales sobre Funciones KDF

- **IKM (Input Key Material):**
  - Puede ser una contraseña, una frase de paso, o una combinación de claves pública y privada.

- **OKM (Output Key Material):**
  - Es la clave secreta producida.
  - IKM y OKM a menudo tienen longitudes diferentes.

- **Tipo de Función KDF:**
  - Una KDF suele ser una función hash u operaciones de cifrado de bloque ocultas.

- **Función Derivadora de Claves Basadas en Contraseñas (PBKDF):**
  - Es un tipo de KDF diseñado para producir claves secretas a partir de IKM de baja entropía como contraseñas.
  - Las claves generadas pueden utilizarse para cifrado simétrico.
  - Otro uso común de PBKDF es el hasheo de contraseñas.

### Composición de una KDF
Una KDF puede contener los parámetros:
- Sal.
- Info.
- PRF.
- Parámetros de resistencia.
- Longitud de OKM.

`Sal`

Alguna cantidad de **datos generados de manera aleatoria para añadir azar al proceso de derivación de claves**.

NIST recomienda al menos 128 bits de longitud.

La generación de la sal no debe depender del IKM, y puede ser pública o secreta.

### Resumen de Información sobre KDF

- **Info:**
  - Información específica de la aplicación, no añade seguridad pero vincula la clave y su uso.
  - Puede incluir versión del protocolo, identificador del algoritmo, etc.
  - Utilizar diferentes valores de 'info' para distintos propósitos se denomina separación de dominio.

- **PRF (Pseudo-Random Function):**
  - Función pseudoaleatoria subyacente como HMAC o una función de cifrado por bloques.

- **Parámetros de Resistencia:**
  - Parámetros para resistir ataques de fuerza bruta específicos de la función.

- **OKM (Output Key Material):**
  - Longitud de OKM deseada.

- **Secreto Obligatorio:**
  - De todos los parámetros mencionados, el único obligatoriamente secreto es IKM.

### Propiedades de una KDF

1. **Determinístico:**
   - Los mismos parámetros de entrada producen siempre el mismo secreto.

2. **Irreversible:**
   - Es computacionalmente intratable obtener el IKM original a partir del OKM producido.

3. **Resistente:**
   - Es resistente a los ataques de fuerza bruta.

4. **Entropía de la Contraseña:**
   - La KDF debe manejar adecuadamente la entropía de la contraseña para garantizar la seguridad.

### Entropía de Contraseña y Algoritmos de KDF

**Entropía de la Contraseña:**
- La entropía se calcula con la fórmula: Entropía = log2(nchar ^ plen).
- Una contraseña de 8 caracteres tiene aproximadamente 51 bits de entropía, y con 12 caracteres crece a alrededor de 76 bits.

**Algoritmos de KDF:**
1. **PBKDF2:**
   - Popular y recomendado por el estándar PKCS#5.
   - Utiliza HMAC, generalmente HMAC-SHA-256, con iteraciones variables.
   - En 2021, la OWASP recomendó 310,000 iteraciones con HMAC-SHA-256.

2. **Scrypt:**
   - Computacionalmente intensivo con intensos requisitos de memoria.
   - Utiliza HMAC-SHA-256 y es personalizable en términos de memoria y paralelismo.
   - Recomendado generalmente por su robustez.

3. **Otros Algoritmos:**
   - KDF y HKDF de paso simple no son tan adecuados como PBKDF.
   - ANSI X9.42, ANSI X9.63 y TLS1 PRF requieren parámetros específicos de TLS.
   - SSH KDF requiere parámetros específicos de SSH.

**Recomendación General:**
- Se recomienda el uso de Scrypt debido a su robustez y capacidad para manejar eficientemente los requisitos de memoria y paralelismo.

# Firmas digitales
- **Firma Digital:**
  - Array de bits obtenido al cifrar el hash del mensaje con una clave privada y descifrar con la clave pública (hash-and-sign).
  - Utilizado para firmar documentos, certificados, transacciones financieras, etc.
  
- **Aplicaciones y Protocolos:**
  - Presentes en TLS, SSH, IPSec, certificados digitales X.509, PGP, S/MIME, entre otros.

- **Relación con Criptografía Asimétrica:**
  - La criptografía asimétrica descansa en la simétrica; claves de sesión simétricas en uso.
  - Firmas digitales se basan en resúmenes de mensajes.

- **Limitaciones del Algoritmo de Firma:**
  - Limitación en la cantidad de datos que se pueden firmar en un bloque.
  - No es recomendable dividir mensajes en varios bloques con varias firmas debido a vulnerabilidades.

- **Enfoque en Resumen del Mensaje:**
  - La mayoría de algoritmos, excepto EdDSA, firman el resumen del mensaje, no el mensaje mismo.
  - Uso de algoritmos de hash rápidos para transformar mensajes largos en resúmenes breves procesables por algoritmos de firma más lentos.

## Comparación entre Firmas Digitales y MAC

| Características          | Firmas Digitales                               | MAC                                          |
|--------------------------|------------------------------------------------|----------------------------------------------|
| **Producción/Verificación** | Utilizan claves privadas para producir y claves públicas para verificar. | Utilizan la misma clave simétrica para producción y verificación.  |
| **Revelación de Clave**    | Posible verificar sin revelar la clave privada. | La clave secreta debe ser compartida entre el firmante y el verificador.   |
| **Verificación por Terceros** | Cualquier entidad con la clave pública puede verificar. | Un tercero no puede verificar el mensaje, se complica con múltiples verificadores. |
| **No Repudio**             | Proveen no repudio.                             | No proveen no repudio.                          |

## Comparación de Algoritmos de Firma Digital

| Características          | RSA                                 | DSA                               | ECDSA                             | EdDSA                             | SM2                                |
|--------------------------|-------------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| **Uso**                  | Cifrar y Firmar                     | Firma Digital                     | Firma Digital con Curvas Elípticas| Firma Digital con Curvas Edwards  | Firma Digital Oficial de China    |
| **Velocidad**            | Lento para Firmar, Rápido para Verificar | Moderado para Firmar y Verificar | Rápido para Verificar, Moderado para Firmar | Rápido para Firmar y Verificar   | Similar a Curvas Brainpool de 256 bits |
| **Seguridad**            | Depende del Tamaño de Clave         | Similar a RSA                     | Seguridad con Claves más Cortas   | Seguridad con Claves más Cortas   | Similar a Curvas Brainpool de 256 bits |
| **Desventajas Principales** | Firmas Largas, Claves Extensas, Antiguo | Firmas más Cortas que RSA       | Claves más Cortas que RSA         | No necesita RNG, Menos Vulnerable a Timing Attacks | Utilizado Oficialmente por China   |
| **RNG Necesario**        | Sí                                  | Sí                                | Sí                                | No (Inmune a Timing Attacks)      | No                                |
| **Curvas Soportadas**    | No Aplicable                        | No Aplicable                     | Varias (Brainpool, EdDSA, NIST)   | Curve25519, Curve448              | SM2 de 256 bits                   |

## ¿Qué algoritmo de firma digital utilizar?

1. **EdDSA con Curve25519:**
   - **Ventajas:** Muy confiable, recomendado para datos que caben en memoria.
   - **Consideraciones:** No bien soportado para certificados TLS.

2. **ECDSA:**
   - **Ventajas:** Popular, adecuado para situaciones que requieren un enfoque más tradicional o soporte para streaming.
   - **Consideraciones:** Menos soporte para software antiguo.

3. **RSA:**
   - **Ventajas:** Popular, buena interoperatividad con software antiguo, verificación de firma rápida.
   - **Consideraciones:** Tamaño de firma más grande, menos eficiente para ciertos casos.

**Nota:** La elección depende de los requisitos específicos de tu aplicación, considerando factores como compatibilidad, velocidad y tamaño de firma.

## Esquema de Firma Digital y Cifrado

### Referencias del Esquema:

1. **A cifra el texto claro con la clave pública de B.**
2. **A calcula el hash del texto claro y lo cifra con la clave privada de A (lo firma).**
3. **A envía el texto cifrado y la firma a B.**
4. **B descifra el texto cifrado con la clave privada de B y calcula el hash del texto claro.**
5. **B descifra la firma con la clave pública de A y obtiene el hash del texto claro.**
6. **B verifica que los hashes calculados en d) y e) sean iguales.**

# Esteganografía
## Generalidades

La esteganografía, derivada de las palabras griegas "steganos" (oculto) y "graphein" (escribir), se define como la escritura oculta. El término proviene del libro "Steganographia" escrito por Johannes Trithemius en 1499.

## Términos y Definiciones en Esteganografía

- **Esteganografía:** Estudia procedimientos para ocultar información, ya sea almacenándola en algún soporte o transmitiéndola por algún canal.

- **Stegoanálisis:** Examina la seguridad de algoritmos esteganográficos, detectando la posible presencia de información oculta o eliminándola.

- **Estegomedio:** Medio o soporte de comunicación utilizado para enmascarar información sin levantar sospecha.

- **Estegoobjeto:** Resultado de ocultar información en un estegomedio.

## El Problema del Prisionero

En el problema del prisionero, dos personas (A y B) deben coordinar un plan de fuga sin comunicación directa, utilizando esteganografía a través de un guardián. El guardián puede tener diferentes comportamientos:

1. **Ataque Pasivo:** El guardián analiza la información intercambiada, permitiendo la comunicación si no detecta nada sospechoso.

2. **Ataque Activo:** El guardián puede modificar la información, ya sea accidentalmente o a propósito, incluso dañándola significativamente.

3. **Ataque Malicioso:** El guardián puede modificar la información oculta con la intención de provocar acciones específicas en las entidades receptoras (altamente improbable).


## Comparación de Tipos de Sistemas Esteganográficos

| Características                    | Estegosistemas de Clave Simétrica | Estegosistemas de Clave Pública | Estegosistemas Cuánticos |
|------------------------------------|------------------------------------|----------------------------------|---------------------------|
| **Claves Necesarias**               | Clave secreta (estegoclave)         | Clave pública y privada         | Principios cuánticos      |
| **Seguridad Dependiente de**        | Estegoclave                         | Ambas claves                     | Principios cuánticos      |
| **Divulgación de Algoritmo**        | Puede ser público                  | Puede ser público               | Puede ser público          |
| **Nivel de Seguridad**              | Depende de la estegoclave           | Depende de la clave privada     | Basado en física cuántica  |
| **Aplicaciones Comunes**            | Mensajes confidenciales            | Firma digital, comunicación segura| Comunicación cuántica     |
| **Revelación de Información**       | Requiere estegoclave               | Requiere clave privada          | Depende de principios cuánticos |


## Algoritmos Esteganográficos: Características Principales

| Características      | Descripción                                                                                     |
|-----------------------|-------------------------------------------------------------------------------------------------|
| **Capacidad**         | Cantidad de información que puede ser ocultada.                                                  |
| **Seguridad / Invisibilidad** | Probabilidad de detección por un estegoanalista.                                            |
| **Robustez**          | Cantidad de alteraciones dañinas que el medio puede soportar antes de perder la información oculta.|

### Tipos de Algoritmos Esteganográficos

#### 1. Alteración de Cubierta Existente
   - Modifica una cubierta existente, generando alteraciones.
   - **Ejemplos:** Least Significant Bit (LSB), Algoritmo de Modificación de Pixel (PVD).

#### 2. Generación Automática de Cubierta
   - Crea automáticamente una cubierta ocultando información en ella.
   - **Ejemplos:** F5, JSteg.

#### 3. Ocultación sin Modificación de Cubierta
   - No altera la cubierta existente durante la ocultación.
   - **Ejemplos:** Algoritmo de Codificación de Longitud Variable (VLC), Algoritmo de Duplicación de Pixel.

## Técnicas esteganográficas
### Ocultación en Imágenes Digitales

Existen diversas técnicas para ocultar información en imágenes digitales de formatos como PNG, GIF, BMP o JPEG. Estas técnicas se emplean principalmente en la ocultación de comunicaciones digitales y en malware moderno para evadir medidas de seguridad perimetral. A continuación, se detallan algunas de estas técnicas:

#### Técnica LSB (Último Bit Significativo)
- Es la técnica más común y de fácil aplicación.
- Permite ocultar grandes cantidades de información con bajo impacto en el estegomedio.
- Resistencia media al estegoanálisis.

#### Utilización de Coeficientes Cuantificados DCT (Transformada Discreta de Coseno)
- Otra técnica habitual.
- A diferencia de LSB, oculta menos información pero tiene alta resistencia al estegoanálisis.

#### Estegomalware
- Permite ocultar datos de configuración del malware y la comunicación C&C (conexión malware-servidor) en imágenes digitales.
- También se puede utilizar como canal encubierto para el robo de información.

#### Polyglot
- Permite que un archivo con un formato específico se comporte como otro.
- Posibilita incrustar el código del exploit del malware mediante LSB para que la imagen sea interpretada como Javascript, HTML, PDF, etc.

### Ocultación en Audio Digital

Las técnicas de ocultación en audio digital destacan en su mayoría en el uso de LSB, ocultación en la fase de una señal (phase coding), en el eco de una señal (echo hiding), y ocultación estadística, aunque no son muy comunes.

### Ocultación en Sistemas de Archivos y Formatos

Las técnicas de ocultación en sistemas de archivos y formatos comprenden:
- Ocultación basada en fragmentación interna de sistemas operativos (slack space).
- Borrado de archivos (unallocated file space).
- Técnicas EoF (End of File).
- Ocultación en flujos de datos alternativos en NTFS (ADS en NTFS).

### Esteganografía en Código HTML/XML

La ocultación en código HTML/XML se basa en:
- Caracteres invisibles.
- Codificación de caracteres.
- El orden de atributos de una etiqueta.

### Canales Encubiertos en Protocolos de Comunicación

Los canales encubiertos en protocolos de comunicación son aquellos que violan políticas de seguridad, utilizados para fuga de información y control remoto. Se realiza estegoanálisis mediante algoritmos de machine learning. Algunos protocolos utilizados incluyen HTTP, TCP, UDP, IPv4, IPv6, ICMP, IPSEC, IGMP, FTP, DNS, 802.2, 802.3, redes inalámbricas, etc. Otras técnicas son la esteganografía multinivel (MLS) e Inter-protocolos (IPS).

## Técnicas de Estegoanálisis

Existen diversas técnicas de estegoanálisis utilizadas para detectar la presencia de información oculta. Algunas de estas técnicas son:

### Detección Estructural de LSB
- Ataques estadísticos por análisis de pares de muestras.
- Ataques RS (Reversible Steganography).
- Ataques triples, entre otros.

### Ataques de Calibración a Esteganografía JPEG
- Se fuerza la recompresión de una imagen JPEG para obtener una nueva imagen con propiedades estadísticas similares a las de la imagen de cobertura.

### Ataques de Fuerza Bruta
- Intentos sistemáticos de probar todas las combinaciones posibles para descubrir la información oculta.

### Estegoanálisis por Machine Learning
- Utilización de algoritmos de machine learning para analizar patrones y detectar posibles ocultamientos de información.

Estas técnicas de estegoanálisis son empleadas con el fin de evaluar la seguridad y la resistencia de los sistemas esteganográficos frente a intentos de detección.
