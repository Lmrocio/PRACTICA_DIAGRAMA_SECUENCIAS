# Diagrama de secuencias

La actividad consiste en:

- Obtener las clases estereotipadas (Interfaces, Control y Entidad) correspondientes a los casos de uso: CU: Sacar dinero y CU: Validación usuario.
- A partir de las clases estereotipadas, obtener las clases de diseño y con ellas diseñar el diagrama de secuencias para los casos de uso anteriores. 

<hr>

## a) Creación de secuencias

### 1) Obtener las clases estereotipadas a partir de los casos de uso. (Interfaces, Control y Entidad)

- Caso de uso: sacar dinero.
  - ``Interface``: Usuario, es decir, el actor que inicia la acción de sacar dinero como interacción externa.
  - ``Control``: Sistema bancario como el controlador del flujo e interraciones entre los objetos.
  - ``Entidad``: Cuenta bancario como los objetos o datos que son manipulados durante la interacción.
    
- Caso de uso: validación usuario.
  - ``Interface``: Usuario, es decir, el actor que ingresa sus datos como interacción externa.
  - ``Control``: Validador de usuarios como el controlador del flujo e interraciones entre los objetos.
  - ``Entidad``: Base de datos de los usuarios.


### 2) Diseñar el diagrama de secuencias básico en base a las clases estereotipadas.
- Caso de uso: sacar dinero
  ![CU: SACAR DINERO](https://github.com/Lmrocio/PRACTICA_DIAGRAMA_SECUENCIAS/blob/main/CU_sacar_dinero.png)
  
  <details><summary>Código empleado</summary>
    @startuml
    
    actor Usuario
    
    participant "Controlador Transacción" as Control
    
    participant "Cuenta Bancaria" as Cuenta
    
    Usuario -> Control: Solicitar sacar dinero
    
    Control -> Cuenta: Verificar saldo
    
    Cuenta --> Control: Responder con saldo
    
    Control -> Cuenta: Descontar dinero
    
    Cuenta --> Control: Confirmar descuento
    
    Control -> Usuario: Entregar dinero

    @enduml
  </details>
  
- Caso de uso: validación usuario.
 ![CU: VALIDACIÓN USUARIO](https://github.com/Lmrocio/PRACTICA_DIAGRAMA_SECUENCIAS/blob/main/CU_validacion_usuario.png)
  
  <details> <summary>Código empleado</summary>
    @startuml
      
    actor Usuario
    
    participant "Controlador Autenticación" as Control
    
    participant "Base de Datos Usuario" as BaseDatos
  
    Usuario -> Control: Ingresar usuario y contraseña
    
    Control -> BaseDatos: Verificar credenciales
    
    BaseDatos --> Control: Responder con validación
    
    Control -> Usuario: Notificar resultado
  
    @enduml
  </details>



### 3) Obtener las clases de diseño a partir de las clases de análisis estereotipadas.
- Caso de uso: sacar dinero.
  - ``Controlador de transacción``: se trataría de una Clase que contiene métodos como verificarSaldo(), ingresarCantidad(), consultarSaldo(), etc.
  - ``Cuenta bancaria``: se trataría de una Clase con atributos como 'saldo', el cuál representa a la cantidad de dinero registrada en una cuenta de banco determinada, y métodos como aumentarSaldo().
    
- Caso de uso: validación de usuario.
  - ``Controlador de validación``: se trataría de una Clase con métodos como validarCredenciales().
  - ``Base de datos``: se trataría de una Clase con métodos como buscarUsuario().


### 4) Diseñar el diagrama de secuencia final.
- Caso de uso: sacar dinero.
  ![CU SACAR DINERO FINAL](https://github.com/Lmrocio/PRACTICA_DIAGRAMA_SECUENCIAS/blob/main/CU_sacar_dinero_final.png)
  
  <details><summay>Código empleado</summay>
    @startuml
    
    actor Usuario
  
    participant "ControladorTransaccion" as Control
  
    participant "CuentaBancaria" as Cuenta
    
    Usuario -> Control: solicitarSacarDinero()
  
    Control -> Cuenta: verificarSaldo()
  
    Cuenta --> Control: saldoDisponible()
  
    Control -> Cuenta: descontarDinero()
  
    Cuenta --> Control: confirmacionDescuento()
  
    Control -> Usuario: entregarDinero()
    
    @enduml
  </details>
  
- Caso de uso: validación usuario.
  ![CU VALIDACION USUARIO FINAL](https://github.com/Lmrocio/PRACTICA_DIAGRAMA_SECUENCIAS/blob/main/CU_validacion_usuario_final.png)

  <details><summary>Código empleado</summary>
    @startuml
    
    actor Usuario
  
    participant "ControladorAutenticacion" as Control
  
    participant "BaseDeDatos" as BaseDatos
    
    Usuario -> Control: ingresarCredenciales()
  
    Control -> BaseDatos: consultarUsuario()
  
    BaseDatos --> Control: respuestaValidacion()
  
    Control -> Usuario: resultadoAutenticacion()
    
    @enduml
  </details>

<hr>

## b) Interpretación del diagrama de CU: Validación usuario.
### Elementos del diagrama:
-  Actor: Usuario, es el actor que ejecuta le interacción principal y externa con el sistema. En este caso, se trata de la persona que quiere acceder a un sistema proporcionando sus datos. Se ubica en el extrema izquierdo del diagrama, y su interacción comienza al dar sus datos.

- Controlador de Autenticación: es el objeto que gestiona el flujo de la autenticación en el sistema, es decir, recibe los datos del usuario y los procesa a través de la base de daatos. Se trata, pues, del intermediario entre el Usuario y la Base de datos.

- Base de Datos: es la entidad que almacena los datos de los diferentes usuarios ingresados en el sistema. El controlador de autenticación consulta la Base de datos para comprobar si los datos ingresados por el usuario coinciden con los almacenados.

### Flujo de interacción:
- El Usuario ingresa sus credenciales: esta acción da comienzo al flujo del sistema, siendo el primer mensaje en el diagrama.
  
- El controlador de autenticación valida las credenciales: verifica la información obtenida a través de una consulta realizada en la Base de datos del sistema.
  
- La base de datos responde a la comprobación de los datos: en este punto, se busca al usuario dentro de los datos almacenados, devolviendo una respuesta al ControladorAuteticacion sobre si las credenciales introducidas son válidas o no.

- Respuesta mostrada al Usuario: una vez comprobados los datos, el Controlador de Autenticación devuelve el mensaje de la Base de datos.

<hr>

## c) Responde a la pregunta: ¿De que manera te ayuda un diagrama de secuencias durante el proceso de desarrollo del software?

Los diagramas de secuencias nos ayudan a visualizar el flujo de las interacciones que los objetos tendrán dentro de un mismo sistemas que estemos desarrollando. Por tanto, son útiles para comprender el funcionamiento de un sistema y el tránsito de la información que se emplea o utiliza para realizar las distintas funciones de dicho sistema. Debido a esto último, podemos añadir que, este tipo de diagramas, nos proporciona una visión clara de las dependencias entre los distintos objetos, lo que nos permite identificar con mayor precisión dónde se ubican los posibles errores o problemas en el funcionamiento o lógica del diseño.
