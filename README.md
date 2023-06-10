# Practica-1
Implementación de un algoritmo merge concurrente:

- Tenemos NPROD procesos que producen números no negativos de forma creciente. 
  Cuando un proceso acaba de producir, produce un -1. 
  Cada proceso almacena el valor almacenado en una variable compartida con el consumidor, un -2 indica que el almacén está vacío.

- Hay un proceso merge que toma los números producidos y los almacena de forma creciente en una única lista (o array). 
  El proceso debe esperar a que los productores tengan listo un elemento e introducir el menor de ellos.

- Hay 3 listas de semáforos tal que cada productor solo maneja sus semáforos para sus datos y el proceso merge maneja todos los semáforos.
  1. emptylst: Esta lista almacena los semáforos de tipo Semaphore que representan la disponibilidad de espacios vacíos en los 
    almacenes. Cada productor tiene su propio semáforo en esta lista. El número de semáforos en emptylst es igual al 
    número de productores (NPROD). Cada semáforo se inicializa con un valor N, igual al número total de números que ese productor
    va a producir, lo que indica que inicialmente hay espacios disponibles para que los productores almacenen números.
    
  2. non_emptylst: Esta lista almacena los semáforos de tipo Semaphore que representan la disponibilidad de elementos 
    en los almacenes. Cada productor tiene su propio semáforo en esta lista. El número de semáforos en non_emptylst 
    es igual al número de productores (NPROD). Cada semáforo se inicializa con un valor de 0, lo que indica que inicialmente no hay 
    elementos disponibles para sacar en cada almacén.
    
  3. mutexlst: Esta lista almacena los mutexes de tipo Lock que se utilizan para lograr exclusión mutua al acceder a los almacenes. 
    Cada productor tiene su propio mutex en esta lista. El número de mutexes en mutexlst es igual al número de 
    productores (NPROD). Cada mutex se utiliza para asegurar que solo un productor acceda a un almacén a la vez, 
    garantizando la consistencia de los datos compartidos y la exclusión mutua.

- OPCIONAL: implmentación añadiendo un búffer de tamaño fijo de forma que los productores ponen valores en el búffer.
  Las principales diferencias con la anterior implementación son:
  
  1. emptylst: Esta lista almacena los semáforos de tipo BoundedSemaphore que representan la disponibilidad de espacios vacíos 
    en los buffers de almacenamiento. Cada productor tiene su propio semáforo en esta lista. El número de semáforos en emptylst 
    es igual al número de productores (NPROD). Cada semáforo se inicializa con un valor igual a la capacidad de los buffers (K), 
    lo que indica que inicialmente hay espacios disponibles para que los productores almacenen números.
    
  2. En la función add_data hay que esperar a que el valor del índice del respectivo proceso sea menor que K, porque sino accederá
    a una posición del almacén que no existe.
    
