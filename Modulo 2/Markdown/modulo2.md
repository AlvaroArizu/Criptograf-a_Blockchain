# Modulo 2
1. Fundamentos de la criptografía moderna.
2. Tipos de criptosistemas modernos.
3. Criptografía simétrica.
4. Bits de seguridad.
5. Cifrado por bloque y por flujo.
6. Modos de operación.
7. Padding.
8. Algoritmos de cifrado simétricos.
9. Criptografía asimétrica.
10. Algoritmos de cifrado (RSA, EC). 11. Sesión de claves.
12. Algoritmo RSA.
13. Laboratorio: vulnerar contraseñas.

# Criptografia Asimetrica
riptografía asimétrica utiliza dos claves:, 
- Pública -> DESCIFRADA
- Privada  -> CIFRADA

Se emplea cuando es difícil enviar claves simétricas de manera segura. Aunque más lenta y con claves más grandes que la simétrica, se usa para cifrar, descifrar, generar claves y firmar. Las claves asimétricas tienen estructura, a diferencia de las simétricas que son flujos aleatorios. El mensaje cifrado es más extenso que el texto plano.
## Esquema HPKE
El esquema HPKE (Hybrid Public Key Encryption) utiliza cifrados asimétricos para cifrar claves simétricas, optimizando la velocidad en conexiones remotas. Permite enviar claves asimétricas al receptor y utilizarlas para cifrar la comunicación de manera eficiente.
## Algoritmos RSA
La seguridad de RSA depende de la factorización de números primos. Aunque efectivo, su rendimiento disminuye significativamente con el aumento del tamaño de la clave. Las claves RSA contienen módulo, exponente y, opcionalmente, primos y coeficientes. El cifrado y descifrado son más lentos a medida que la clave crece. El tamaño del bloque cifrado es igual al de la clave, resultando en textos cifrados más extensos. La firma RSA sigue el estándar PKCS#1 y tiene el mismo tamaño que la clave RSA. Es importante considerar que el nivel de seguridad es menor que el tamaño de la clave, según estimaciones del NIST.
### Qué tamaño elegir? NIST recomienda:
- Al menos 2048 bits hasta 2030.
- Al menos 3072 bits después de 2030.

**Cuando lleguen las computadoras cuánticas, el cifrado asimétrico estará completamente roto. Se cree que no sucederá antes del 2030.**
## Curvas elípticas
La criptografía de curva elíptica es esencial en ciberseguridad, siendo un formalismo matemático estudiado por más de 150 años. Proporciona propiedades que permiten la adaptación de algoritmos asimétricos en el campo de la criptografía. Las curvas elípticas se utilizan en algoritmos criptográficos, basándose en el problema de logaritmos discretos. Existen recomendaciones específicas de curvas elípticas con aplicaciones en ciberseguridad, y algunas de ellas presentan propiedades que las hacen más eficientes o resistentes a ciertos tipos de ataques. La elección de curvas elípticas y su implementación adecuada son aspectos clave en el diseño de sistemas seguros en el ámbito de la criptografía y la ciberseguridad.
### Otros algoritmos 
- `RSA:` es el algoritmo más importante. Es el único que permite cifrar datos directamente.
- `DSA` (Digital Signature Algorithm) y `ECDSA` (Elliptic Curve Digital Signature Algorithm): pueden utilizarse para firmas digitales.
- `DH` (Diffie-Hellman) y `ECDH` (Elliptic Curve Diffie-Hellman): pueden ser usados para intercambio de claves en el protocolo TLS (Transport Layer Security).
- `ElGamal:` utiliza un algoritmo DH con claves DSA o un algoritmo ECDH con claves ECDSA para cifrado asimétrico. Involucra una clave efímera (temporal) DSA/ECDSA adicional para el intercambio de la clave secreta compartida (clave de sesión).
## Claves de sesión
En una sesión de red, dos dispositivos se reconocen, abren una conexión virtual y terminan cuando obtienen la información necesaria, enviando mensajes de cerrar_notificar o por inactividad. La clave de sesión simétrica, temporal y de un solo uso, encripta y descifra datos entre partes. En protocolos seguros como TLS, SSH o IPsec, la sesión inicia con handshaking, intercambiando claves. Versiones antiguas usaban cifrado híbrido (HPKE); las actuales, intercambio de claves DH o ECDH, derivando la clave de sesión para cifrar. ElGamal y IES son esquemas similares para cifrado asimétrico. Claves de sesión pueden intercambiarse con Diffie-Hellman o ECDH.
# Algoritmos de cifrado simetricos
## Algoritmos DES y 3DES
- **DES:**
  - Basado en el algoritmo Lucifer de IBM de los años '70.
  - Adoptado como estándar por el gobierno de EE. UU. en 1976.
  - Originalmente diseñado para hardware por la NSA, pero su especificación detallada permitió implementaciones por software.
  - Vulnerabilidades demostradas en 1998 debido a la corta longitud de clave (56 bits).
  - Bloques de 64 bits y clave de 56 bits, considerados inseguros según estándares actuales.

- **3DES (Triple DES):**
  - Consiste en aplicar DES tres veces con 2 o 3 claves diferentes.
  - Longitudes de clave de 80 bits y 112 bits de seguridad respectivamente.
  - Ambos algoritmos se consideran obsoletos.
## Algoritmo AES

- Certificado por NIST en octubre de 2000 como reemplazo de 3DES.
- Rijndael (Vincent Rijmen y Joan Daemen) es el algoritmo adoptado.
- AES es el más popular, rápido y confiable.
- Cifrado por bloques de 128 bits.
- Variantes con claves de 128, 192 y 256 bits (AES-128, AES-192 y AES-256).
- Actualmente, la seguridad se reduce en 2 bits, a 126, 190 y 254 para AES-128, AES-192 y AES-256 respectivamente.
- Soporte común para aceleración por hardware en CPUs actuales.

## Algoritmo ChaCha20
- Moderno cifrado por flujo, seguro y rápido.
- Puede ser usado con claves de 128 bits o de 256 bits.
- No se conocen ataques que reduzcan su nivel de seguridad.
- Modificación con rendimiento mejorado de Salsa20.
- Popularizado a partir de su adopción por Chrome.
- Desventaja menor: usa un contador de bloque de solo 32 bits.
- Debido a la longitud de su contador de bloque, no se considera seguro para textos claros contiguos de más de 256 GiB.
- Si se usa con este fin, se debería fraccionar el texto plano en bloques de menos de 256 GiB y resetear el contador de bloque y el nonce antes de cifrar cada fracción.

## Otros Algoritmos

### RC4
- Antiguo cifrado por flujo con claves de 40 a 2048 bits.
- Muy popular en el pasado por su simplicidad y velocidad.
- Obsoleto.

### CAST5 (CAST-128)
- Usado por el gobierno de Canadá.
- Claves de 128 bits.
- No se conocen ataques, seguridad en 128 bits.

### GOST89 (Magma)
- Antiguo cifrado de la ex URSS, desarrollado en la década del '70.
- Estandarizado en 1989, aún funcional.
- Claves de 256 bits, nivel de seguridad 178 bits.

### GOST2015 (Kuznyechik)
- Sucesor de Magma, usado por Rusia.
- GOST significa GOvernment STandard.

### SEED y ARIA
- Cifrados de Corea del Sur.
- SEED desarrollado en 1998, ARIA en 2003.
- Ambos cifran por bloques de 128 bits.
- ARIA basado en AES, soporta claves de 128, 192 y 256 bits.
- SEED usa claves de 256 bits.
- No se conocen ataques prácticos, seguridad máxima.

### Camellia
- Cifrado por bloques de 128 bits, desarrollado en Japón.
- Similar en diseño a AES con seguridad y rendimiento comparables.
- Patentado pero disponible bajo licencia libre de regalías.

### SM4
- Desarrollado en China, desclasificado en 2006.
- Bloques y claves de 128 bits.
- Seguridad en 128 bits.

### Otros Cifrados RC
- RC2 (1987) y RC5 (1994).
- RC5 notable por su simplicidad de implementación.
- Soportan claves de longitud variable, sin ataques conocidos, pero falta confianza general.

### IDEA (International Data Encryption Algorithm)
- Desarrollado en 1991 como intento de reemplazo de DES.
- Problemas de patentes, llevó al desarrollo de Blowfish.

### Blowfish
- Soporta claves de 32 a 448 bits.
- Sin ataques conocidos, pero riesgo de claves inseguras.
- Bloque pequeño de 64 bits.

### Twofish
- Sucesor de Blowfish.
- Tamaño de bloque de 128 bits.
- Longitudes de clave de 128, 192 o 256 bits.

# Criptografia Moderna
### Fundamentos de la criptografia moderna 
En los criptosistemas clásicos, la seguridad se basa en el secreto del método y en el cifrado de caracteres.` En los criptosistemas modernos, la seguridad se basa en el secreto de la clave y en el cifrado de bits.`

Las bases teóricas de los criptosistemas modernos son:
#### Teoría de la Información de Shannon

- Propuso el cifrado mediante clave secreta utilizando las técnicas de difusión y confusión.
- Difusión: dispersa las propiedades estadísticas del lenguaje en el texto claro, utilizando transposiciones o permutaciones.
- Confusión: genera caos en el resultado cifrado para complicar la dependencia entre texto claro, clave y criptograma, mediante la técnica de sustitución.

#### Teoría de Números

- Estudia propiedades de números enteros (divisibilidad, módulo, máximo común divisor con el algoritmo de Euclides, etc.).

#### Teoría de Complejidad Algorítmica

- Indica la fortaleza de un algoritmo, considerando la cantidad de pasos (tiempo de ejecución) y la memoria utilizada.
- Clasifica problemas algorítmicos en fáciles o difíciles de tratar.
- Problemas difíciles incluyen la factorización de números grandes (PFNG) y el problema del logaritmo discreto (PLD).

## Tipos de Criptosistemas Modernos

### Criptografía Simétrica
- También llamada de clave secreta.
- Utiliza una clave única para cifrar y descifrar.
- Se emplea para cifrar bloques o flujos de datos de cualquier tamaño.

### Algoritmos de Integridad de Datos
- Evitan la alteración de bloques de datos, como mensajes.

### Criptografía Asimétrica
- También llamada de clave pública.
- Usa una clave privada para cifrar y otra pública derivada para descifrar.
- Se utiliza para ocultar pequeños bloques de datos, como claves de cifrado y valores de funciones de hash para firmas digitales.

### Protocolos de Autenticación
- Esquemas basados en algoritmos criptográficos diseñados para autenticar la identidad de las entidades.

### Cifrado Homomórfico

- Permite modificar datos cifrados sin descifrar previamente.

### Criptografía Cuántica

- En fase de desarrollo.
- Utiliza propiedades de la mecánica cuántica (polarización de fotones, entrelazamiento cuántico) para resolver el problema de distribución de claves (QKD, quantum key distribution).

### Criptografía Post Cuántica

- En fase de desarrollo.
- Enfocada en encontrar algoritmos criptográficos de clave pública resistentes a ataques posibles de una computadora cuántica.

# Criptografía simétrica
### 5 Componetes
1. `Un texto claro:` convertido a una cadena de bits
2. `Un algoritmo de cifrado:` Esta cadena de bits se cifra utilizando un algoritmo de cifrado basado en diversas técnicas derivadas en XOR (o exclusiva) y la clave secreta.
3. `Una clave secreta`
4. ` Un texto cifrado`: El texto cifrado o criptograma es enviado al receptor.
5. `Un algoritmo de descifrado`: El receptor descifra
el criptograma aplicando el algoritmo de descifrado, que generalmente es el algoritmo de cifrado aplicado en forma inversa.

## Pasos para Cifrar un Texto Plano

1. **Seleccionar un algoritmo de cifrado.**
2. **Generar una clave de cifrado.**
3. **Generar un vector de inicialización (IV).**
4. **Seleccionar el modo de operación del algoritmo de cifrado.**
5. **Seleccionar el tipo de padding.**
6. **Cifrar el texto plano.**

**Nota:** Dependiendo del algoritmo de cifrado y su modo de operación, algunos de estos pasos pueden no ser necesarios.

**Observación:** Los algoritmos pueden operar sobre bloques de datos o sobre flujos de datos.

## Bits de Seguridad

- La seguridad o fortaleza del cifrado se mide en bits de seguridad.
- La cantidad máxima de bits de seguridad es la longitud de la clave de cifrado.
- La seguridad real es menor debido a posibles ataques.

**Recomendaciones NIST (2021):**
- 112 bits de seguridad deberían ser suficientes hasta 2030.
- 128 bits de seguridad deberían ser suficientes hasta la próxima revolución en tecnología o matemática.

`Una de estas revoluciones esperadas dentro de los años venideros es la computación cuántica.`

## Cifrado por Flujo

- Operan sobre bits o bytes de datos.
- No necesitan padding ni modos de operación.
- Más fáciles de utilizar, implementar y son más rápidos que los cifrados por bloques.
- Menos seguros en general.

## Cifrado por Bloques

- Se subdivide el texto plano en bloques del tamaño requerido por el algoritmo.
- Si el tamaño de los datos es menor al tamaño del bloque o no es múltiplo de este, se debe realizar relleno (padding).
- Encriptar bloque usando clave de cifrado.
- Encriptar bloque usando clave de cifrado.

## Cifrado por Bloque: Modos de Operación

### Electronic Codebook (ECB)
- Cada bloque se cifra independientemente con la misma clave.
- No usa IV ni bloque previo de texto cifrado.
- Utilizado para transmisión de valores simples, bases de datos, ficheros de acceso aleatorio.
- Resiste errores.
- Problema de seguridad: mismo texto plano produce siempre el mismo texto cifrado.

### Cipher Block Chaining (CBC)
- Entrada al algoritmo de cifrado es el XOR del próximo bloque de texto plano y el bloque precedente del texto cifrado.
- Utilizado para transmisiones de propósito general y autenticación.
- Evita la inserción, eliminación o reordenamiento de bloques del mensaje cifrado.
- Usa un IV (number once), almacenado junto al texto cifrado.

### Cipher Feedback (CFB)
- Cada bloque es cifrado y luego combinado mediante XOR con el siguiente bloque del mensaje original.
- Utilizado para transmisiones de propósito general y autenticación.
- Uso de IV para sincronización y longitud variable de bloques del mensaje.

### Counter (CTR)
- Se cifra una secuencia de bloques del contador.
- Cada bloque del contador es un nonce aleatorio concatenado con el entero del contador.
- Utilizado para transmisiones de propósito general y alta velocidad.

### Galois/Counter Mode (GCM)
- Cifrado como en modo CTR, pero autentica el criptograma.
- Utiliza un IV de 96 bits y solo funciona con bloques de 128 bits.
- Vulnerable a reutilización par clave-IV, mitigado con AES-GCM-SIV.

### Otros Modos de Operación
- AES-GCM-SIV: Resiste mal uso de clave y IV, requiere dos pasadas sobre el texto plano.
- Otros modos poco populares: CBC propagado (PCBC), Output feedback (OFB), Counter with CBC-MAC (CCM), Carter-Wegman+CTR(CWC), Sophie Germain Counter (SGCM).


`¿Cuál modo de operación utilizar?`

`- Galois/Counter Mode (GCM): soporta autenticación y cifrado, no requiere padding, permite precalcular el flujo de claves y paralelizar el cifrado/descifrado. Si lo usa, asegúrese de no usar el IV más de una vez.`

`- Cipher Block Chaining (CBC): el estándar de facto anterior. Necesita padding aplicado al texto plano.`

## Padding para Cifrado de Bloques

Existen distintos tipos de padding, siendo el más habitual el PKCS#7 (Public Key Cryptography Standard Number 7), también conocido como PKCS7 o padding estándar de bloques. Consiste en N bytes con el mismo valor N cada uno.

Ejemplo:
- Si el último bloque de texto plano tiene 10 bytes de datos y 6 libres (tamaño de bloque 16 bytes), podría rellenarse con 6 bytes, cada uno con el valor 0x06.

Si la longitud del texto plano es múltiplo del tamaño del bloque, PKCS#7 agrega padding para detectar si el último byte pertenece al texto plano o al padding tras el descifrado del último bloque.

PKCS#7 se denomina a veces PKCS#5 y utiliza el mismo principio de relleno (N bytes de valor N), pero está definido para bloques de más de 64 bits.

### Desventaja

La desventaja de PKCS#7 es que el texto cifrado es susceptible de un ataque de oráculo al padding. Este ataque solo es posible si el atacante puede forzar el cifrado de una gran cantidad de texto plano controlado por él con la misma clave de cifrado.

# Criptoanalisis


El criptoanálisis tiene como objetivo obtener la clave o el mensaje cifrado, y puede abordar diferentes enfoques:

1. **Obtención de la Clave o Mensaje:**
   - Intenta determinar la clave utilizada en el cifrado.
   - Busca obtener directamente el mensaje original.

2. **Explotación de Debilidades en Protocolos Seguros:**
   - Incluye el análisis de fallos en protocolos de comunicación segura, como autenticación, administración de claves, fallas de hardware o software, entre otros.

3. **Romper el Criptosistema:**
   - La práctica del criptoanálisis se conoce coloquialmente como "romper el criptosistema".
   - Busca comprometer la seguridad del sistema cifrado.

4. **Determinación del Lenguaje, Tipo de Cifrado y Claves:**
   - Busca identificar el lenguaje utilizado en el mensaje.
   - Intenta determinar el tipo general de cifrado o código utilizado.
   - Analiza las claves empleadas en el proceso de cifrado.

5. **Reconstrucción del Mensaje:**
   - A través de cantidades variables de texto cifrado y información relacionada, se intenta reconstruir el mensaje original.

Estas determinaciones se basan en diferentes fuentes de información, como el texto cifrado, la identidad del emisor y receptor, análisis estadístico de tráfico y conocimiento específico sobre los contenidos del mensaje.

## Tipos de Ataques en Criptografía

### Ataques Blandos
- Involucran la coerción o ingeniería social, siendo a menudo los más efectivos.

### Ataques por Fuerza Bruta
- Búsqueda exhaustiva de una clave en todo el espacio de claves disponible.
- Pueden ser activos, pasivos, u offline.

### Ataques Man-in-the-Middle (MitM)
- Generalización de la suplantación de IP y uno de los más poderosos.
- Conocido desde antiguo y afecta a todos los cifrados.

### Ataques de Texto Plano
- Utilizan una cantidad conocida de texto claro y su correspondiente texto cifrado para encontrar la clave.
- Común en RSA, emails y e-commerce.

### Ataques de Texto Cifrado Conocido
- Involucran una parte conocida del texto cifrado para obtener la clave y el texto claro.
- Implican un trabajo considerable, por ejemplo, Kasiski.

### Ataques de Retransmisión (Relay Attacks)
- Consisten en reenviar mensajes.
- Pueden ser pasivos o activos y son relevantes en el contexto de NFC.

### Ataques de Texto Claro Elegido
- Implican definir un texto claro particular, cifrarlo, y analizar el texto cifrado resultante.
- Puede ser usado contra sistemas que utilizan las mismas claves para cifrar gran cantidad de información.

### Ataques de Cumpleaños
- Específicos contra firmas digitales y algoritmos de logaritmos discretos.

### Ataques de Texto Cifrado Elegido
- Intentan que la víctima descifre un texto cifrado predeterminado para obtener la clave.

### Ataques de Repetición
- Utilizan partes de un intercambio cifrado previo, requiriendo medidas como el uso de timestamps.

### Ataques contra RSA
- Diversos ataques ilustran problemas de implementación, como el ataque factorial mediante la técnica de Pollard.

### Criptoanálisis Diferencial
- Desarrollado para atacar cifrados basados en redes de Feistel en los '80.

### Ataques con Preprocesamiento
- Aumentan la velocidad de ejecución de los algoritmos, calculando previamente datos para intentar romper códigos más tarde.

### Ataques Cold Boot
- Ataques sobre memoria DRAM volátil al extraer datos de chips de memoria en una computadora apagada recientemente.
- Ejemplo de ataque de canal lateral.

## Ataques de Canal Lateral

Los ataques de canal lateral se basan en información adicional que se puede recopilar debido a la implementación física de un protocolo o algoritmo informático. A diferencia de los fallos en el diseño del protocolo, estos ataques aprovechan efectos físicos causados por el funcionamiento del criptosistema.

### Tipos de Ataques

- Algunos requieren conocimientos técnicos del sistema, mientras que otros, como el análisis de potencia diferencial, son efectivos como ataques de caja negra.
- El auge de las aplicaciones Web 2.0 y el software como servicio ha aumentado la posibilidad de ataques de canal lateral, incluso en transmisiones encriptadas entre un navegador web y un servidor.

### Principio Subyacente

Los efectos físicos del criptosistema pueden proporcionar información útil sobre secretos en el sistema, como la clave criptográfica, información de estado parcial, textos planos completos o parciales, entre otros.

Estos ataques destacan la importancia de asegurar la implementación física de los algoritmos criptográficos, ya que los efectos secundarios pueden revelar información sensible.

## Tipos de Ataques de Canal Lateral

### Ataques de Caché
- Se basan en la capacidad del atacante para monitorear los accesos a la memoria caché realizados por la víctima.
- Pueden ocurrir en sistemas físicos compartidos, entornos virtualizados o servicios en la nube.

### Ataques de Tiempo
- Se basan en medir el tiempo necesario para realizar cálculos, como comparar contraseñas.
- Exploran las variaciones temporales para obtener información sensible.

### Ataques sobre Datos Remanentes
- Buscan acceder a datos supuestamente eliminados, como en ataques cold boot.
- Explotan la persistencia de información en la memoria después de ser eliminada.

### Ataques de Fallas Iniciados por Software
- Una clase rara de ataques, como Row Hammer, que aprovecha efectos secundarios en la memoria DRAM.

### Criptoanálisis Acústico
- Explota sonidos producidos durante cálculos, en particular, sonidos de teclados y componentes internos de computadoras.

### Análisis Diferencial de Fallos (DFA)
- Ataque activo que induce fallas en operaciones criptográficas para revelar estados internos.

### Ataques de Monitoreo de Energía
- Utilizan el consumo variable de energía durante el cálculo para obtener información.

### Ataques Electromagnéticos
- Estudian la radiación electromagnética filtrada para inferir claves criptográficas o obtener información sensible.

### Ataques a Listas de Dispositivos Autorizados
- Se basan en las diferencias de comportamiento entre dispositivos permitidos y no permitidos.
- Pueden rastrear direcciones MAC de Bluetooth y otros dispositivos.

### Ataques Ópticos
- Se basan en la grabación visual de secretos y datos confidenciales utilizando cámaras de alta resolución u otros dispositivos con capacidades similares.

Estos ataques resaltan la diversidad de enfoques que los atacantes pueden utilizar para comprometer la seguridad de los sistemas, subrayando la importancia de una protección integral.
