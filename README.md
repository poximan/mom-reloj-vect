# Reloj Vectorial
Servicio de reloj vectorial de tamaño n para una arquitectura mom (message-oriented middleware).
De utilidad en sincronizacion de procesos distribuidos, para obtener el orden de cualquier par arbitrario de sucesos.

##
## Configuracion inicial
En propiedades.json debe especificarse cuantos procesos del sistema necesitaran una instancia de reloj.

##
## Parametros
param 1 = indice del que es responsable el reloj vectorial.

##
## Modo de uso

### Alta reloj
var reloj_vectorial = require("mom-reloj-vect")(param 1);

Se requiere el servicio de reloj vectorial.
El proceso consumidor pide por parametros que se reserve una posicion del arreglo vector. El modulo de reloj vectorial reservara esa posicion para el que la solicite.
En caso de conflicto de posiciones, el Reloj notificara con "Reloj vectorial: otro proceso modifico mi reloj".

### Incrementar reloj
reloj_vectorial.incrementar();

Ante un evento que requiera el incremento del valor del reloj, se usara esta funcion. El indice a incrementar es conocido de antemano (durante require).

### Pedir el Reloj
reloj_vectorial.vector();

Devuelve el reloj vectorial completo para operaciones de visualizacion a terceros.

### Pedir indice
reloj_vectorial.indice();

Devuelve el indice reservado para el proceso solicitante.

### Actualizar estado
reloj_vectorial.actualizarVector(nuevo_vector);

..* Sobreescribe con nuevo_vector si posicion != posicion reservada a proceso solicitante.
..* No sobreescribe el vector si posicion == posicion reservada a proceso solicitante.
Para este ultimo caso, si nuevo_vector tiene un valor mayor devuelve falla, pero no interrumpe el proceso.
