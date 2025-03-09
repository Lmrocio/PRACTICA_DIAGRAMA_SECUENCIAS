# Diagrama de secuencias

La actividad consiste en:

- Obtener las clases estereotipadas (Interfaces, Control y Entidad) correspondientes a los casos de uso: CU: Sacar dinero y CU: Validación usuario.
- A partir de las clases estereotipadas, obtener las clases de diseño y con ellas diseñar el diagrama de secuencias para los casos de uso anteriores. 

<hr>

## a) Crea de secuencias

1) Obtener las clases estereotipadas a partir de los casos de uso. (Interfaces, Control y Entidad)

- Caso de uso: sacar dinero.
  - ``Interface``: Usuario, es decir, el actor que inicia la acción de sacar dinero como interacción externa.
  - ``Control``: Sistema bancario como el controlador del flujo e interraciones entre los objetos.
  - ``Entidad``: Cuenta bancario como los objetos o datos que son manipulados durante la interacción.
    
- Caso de uso: validación usuario.
  - ``Interface``: Usuario, es decir, el actor que ingresa sus datos como interacción externa.
  - ``Control``: Validador de usuarios como el controlador del flujo e interraciones entre los objetos.
  - ``Entidad``: Base de datos de los usuarios.
    
2) Diseñar el diagrama de secuencias básico en base a las clases estereotipadas.
- Caso de uso: sacar dinero
  ![CU: SACAR DINERO]()
  
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
 ![CU: VALIDACIÓN USUARIO]()
  
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
  
3) Obtener las clases de diseño a partir de las clases de análisis estereotipadas.

4) Diseñar el diagrama de secuencia final.
