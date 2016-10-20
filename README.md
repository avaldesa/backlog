# backlog

### 44. Eliminar concepto de Connection Role. [Mac]

Eliminar concepto de *Connection Role* haciendo los cambios pertientes en los modelos que lo referencian, como es el casso de los *FLows*.

Luego de esta tarea se debe actualizar las integraciones en Odoo.

### 43. Definir el Cenit Collection Format como un JSON Schema. [Mac]

En todas las colecciones poner un link que permita visualizar el JSON ‘oficial’ de la colección, que se debe corresponder con el Cenit Collection Format.

### 42. Mejorar la interfaz de los wizards. [Aneli]

Los Wizard debemos usarlo solo donde sea impresindible, ya que se aleja de la forma comun de los EDIT que es la propuesta por RailsAdmin.

Donde se justifique el uso de Wizards podemos mejorar la forma en que lo estamos presentando.

- Es conveniente tener un nombre por cada paso, 
- que pueda mostrar los pasos (arriba o abajo)
- que se muestre cual es el paso activo

En este link se puede ver un ejemplo:

- https://drive.google.com/file/d/0B-ltzH-m3LxTZXpvaFM4N18xZUk/view?usp=sharing

### 41. Adicionar los logs de Activity, basado en el history. [Mac]

RailsAdmin tiene extensión para visualizar el historial de actividades para aquellos modelos que sean decorados, este historial aparece en una vista asociada al modelo y en el dashboard. Esa extensión la estamos usando para gestionar las versiones de cross sharing.

Es importante excluir algunos modelos de esta opción como los logs porque tienen una frecuencia muy alta de ocurrencia con relación a otros modelos, es el caso por ejemplo de las tareas y las notificaciones

### 40. Accion que genere cURL para acciones que existen en el API. [Pacheco]

Similar a algoritmia.com, que tiene varios link para usar la api según el sdk, de momento para nosotros es suficiente con tener cURL, la idea es tener una accion en el admin de cenit (para aquellas accionees que corresponden a metodos que existen en el API), donde al dar click la accion aparezca el codigo cURL y se pueda copiar y pegar en una consola y funcione, para esto el curl incluira las credenciales correspondiente al tenant.

Por ejemplo vean el curl en

- https://algorithmia.com/algorithms/nlp/Summarizer

```shell
curl -X POST -d '<INPUT>' -H 'Content-Type: application/json' -H 'Authorization: Simple YOUR_API_KEY' https://api.algorithmia.com/v1/algo/nlp/Summarizer/0.1.3
```

### 39. Lanzar un flujo al termina la ejecución (de la tarea) de un flujo previo. [Mac]

Permitir que un modo de ejecutar un flujo sea lanzarlo luego de terminada la ejecución de un flujo previo.
Este cambio debe ser suficiente para poder enlazar los flujos y definir ‘dataflows’.

Es importante notar que actualmente los Flow se puede combinar mediante eventos, pero esta alternativa podria ser una manera mas sencilla de relacionar data flows.

De modo que un flujo se podría lanzar de 3 maneras:
Mediante los triggers (data event o schedulers)
De forma manual
Definiendo un flujo previo (el flujo actual se lanzaría al terminar la ejecución del flujo previo)

Estos modos de ejecución no tienen que ser exclusivos

En estos momento hay algo equivalente, mediante la definición de un callback al terminar un flujo, la diferencia básica, es que, en el flujo nuevo es donde se define el flujo previo, esto permite que cuando se termine de ejecutar un flujo ‘B’, se pueda ejecutar múltiples flujos, en caso de abajo ‘B’ y ‘C’.

- A 
  - \--- B
  - \----C
    - \-----D

A- se define como flujo previo en ‘B’ y ‘C’ 

C- se define como flujo previo en ‘D’ 

Es importante notar que ‘B’  podría ser un flujo que lo único que defina sea un traslator de tipo algoritmo, donde la salida del flujo sean datos.

### 38. En el dashboard sustituir el listado de acciones de cada modelo por 3 puntos verticals. [Aneli]

En el dashboard asociado con cada modelo, aparece el listado de acciones, que han ido creciendo con el tiempo. La propuesta es sustituir este listado de acciones por un icon de 3 puntos verticales, que al dar click despliegue un menu con el listado de acciones correspondientes.

### 37.Usar el background color en el logo de los shared collections. [Mary]

Algunos logos usan color blanco y tienen asociado un color de background, al parercer en los shared collections no estamos usando el background por lo que los logos no se ven bien o nada, ejemplo: infermedica, Jirafe Event API, NeoWs, watchful.

### 36. Menu lateral de Objetos. [Pacheco, Aneli]

Propuesta: Cuando se de click a un elemento hoja de este menu lateral actual, debe cambiar a un menu de objectos relacionado con el elemento seleccionado.

Por ejemplo si vamos a API Connectors, y le damos click a un connection en particular el menu contextual de objetos podria lucir como el siguiente jerarquia:

- PetStore (Collection Name)
  - PetStore API - v1 (API Connection Name)
    - /pet/findByTags (Resouce Name)
      - Get FindByID (Webhook Name)
  ...    
- Uber (Collection Name)
  - Uber Rest API - v1 (API Connection Name)
  ...
  
Tendriamos un boton flotante con un over que permita cambiar del menu contextual de objetos al menu standard.  

Revisar la parte final de esta presentacion.

- https://docs.google.com/presentation/d/1U7npFSNCPMDZDrDZyPNuP9blxEZmcxFGkDDvTFm2nqw/edit?usp=sharing

### 34. :bug: Errores en los algoritmos en produccion. [Mac]

1. En las entrada de los algorimo *Array* no aparece como un tipo valido

2. Implementando los algoritmos que aparecen aqui

https://www.sitepoint.com/algorithmic-fun-ruby-hashes/

Version 1:
```ruby
if (n % 3 == 0) && (n % 5 != 0)
  'Fizz'
elsif (n % 3 != 0) && (n % 5 == 0)
  'Buzz'
elsif (n % 3 == 0) && (n % 5 == 0)
  'FizzBuzz'
else n
end
```

Version 2:
```ruby
 h = {
    'Fizz' => (n % 3 == 0) && (n % 5 != 0),
    'Buzz' => (n % 3 != 0) && (n % 5 == 0),
    'FizzBuzz' => (n % 3 == 0) && (n % 5 == 0),
    n => (n % 3 != 0) && (n % 5 != 0)
  }
  h.key(true)
```

Salida esperada en los casos:
```ruby
puts declarative(2) #=> 2
puts declarative(3) #=> Fizz
puts declarative(5) #=> Buzz
puts declarative(7) #=> 7
puts declarative(15)#=> FizzBuzz
```
Las dos versiones dan error

### 33. Añadir el concepto de Resource en la categoria de Connectors. [Mac]

Para poder lograr una mayor correspondencia entre los conceptos de Connectors y una especificacion formal de API (como Sagger) es importante introducir el concepto de Resource

Se debe concluir la implementacion iniciada en la rama

add_new_model_resource

Queda pendiente:

* Los Webhooks no necesitan tener asociado un Data Type, en su lugar los webhooks pertencen a un Resource y el Resource tiene un data type.

* Los Webhooks no necesitan tener asociado un path, en su lugar los webhooks pertencen a un Resource y el Resource tiene un path.

* Crear el Script para la migracion de los datos.

### 30. Crear el Shared Collection de Cenit a partir del spec en el directorio de Guru API. [Mary]

Actualizar el script que lee las especificaciones del directorio de Guru API que ya incluyen el spec de Swagger de Cenit IO y generar el Shared Collection de Cenit, con la misma logica que se genera cualquier otro spec.

### 29. Probar y actualizar las integracion de Cenit con Odoo 9. [Mary]

Instalar Odoo 9 y probar cada una de las integraciones con Odoo 9.

Como parte de la actualizacion revisar la documentacion.

### 28. Crear una integracion de Magento basada en el Swagger. [Mary]

El Swagger de Magento y fue adicionado al directorio de Guru API, de modo que debemos actualizar la sincronizazcion de las shard collections para poder adicionar el shared collection de Magento a Cenit basado en esa spec. 

Hacer un pull request a Guru  API annadiendo a la spec los temas de seguridad con OAuth 1 que soporta Magento.

Posteriormente agregarla a las Integraciones disponibles para Odoo.

### 27. Crear Integracion para Spree Ecommerce. [Mary]

Es importante trabajar en esta integracion con Spree. Es una tegnologia que dominamos y podemos tener potenciales clientes. Hay muchas pruebas que podemos realizar con Spree, similares a las que realizamos para Odoo.

### 26. Permitir importar diferentes tipos de API Spec. [Mac] 

Permitir importar diferentes tipos de especificaciones formales de API:

* Swagger
* RAML
* I/O Docs
* Google Discovery
* WADL, 
* API Blueprint

Esta tarea esta inciada por parte de Mary, pero esta pendiente de revisar a partir de los ultimos cambios que se han realizado en Cenit.

Para la transformacion a Swagger se uso 

- https://github.com/APIs-guru/api-spec-converter

### 25. Usando el API de Cenit generar los modulos de integracion de Odoo. [Pacheco]

Actualmente en Cenit tenemos mas de 2270 integraciones, de estas integraciones unas 10 las hemos adecuado a modulos de integracion Cenit Odoo, lo cual permite a Odoo integrarse con terceros sistemas a traves de Cenit.

La mayoria de los clientes que han llegado a Cenit han sido a partir de conocer estas integraciones en Odoo.

En esta URL se pueden ver los modulos publicados en Odoo Apps

- https://www.odoo.com/apps/modules/browse?search=cenit

Daniel incio un proyecto en Python que de forma programatica permite generar un addons de Odoo correspondiente a un shared collection en Cenit.

- https://github.com/cenit-io/odoo-cenit-collection-bundler

Esta generacion automatica se puede hacer a partir de la informacion que se obtiene de Shared Collection a traves del API. El proyecto no se ha actualizado en mas de un anno, durante ese tiempo se ha modificado el API.

En este repo estan los modulos actuales de las integraciones en Odoo.

- https://github.com/cenit-io/odoo-integrations

Por ejemplo, la integracion particular de Twilio, se puede encontrar en

- https://github.com/cenit-io/odoo-integrations/tree/8.0/cenit_twilio

y es un sub-directorio con la siguiente estructura

- cenit_twilio/
  - models/
    * __init__.py
    * config.py
  - secuirity/
    * ir.model.access.csv
  - static/
    * description/
      - index.html
      - ...
  - view/
    - config.xml
    - wizard.xml
  - __init__.py
  - __openerp__.py
    

### 24. API Connection ⇔  Swagger Spec [Pacheco]


La propuesta es que un Swagger Spec se pueda corresponder con un API Connection y sus conceptos relacionados de Resources y Webhooks

Revisar la siguiente presentacion para tener mas elementos relacionados con esta tarea

https://docs.google.com/presentation/d/1U7npFSNCPMDZDrDZyPNuP9blxEZmcxFGkDDvTFm2nqw/edit?usp=sharing

* Connectors
  * API Connections 
    * Resources
      * Webhooks

Lo que es lo mismo que:
* Webhook *belogs_to* Resource
* Resource *belogs_to* API Connection 

nota: el nombre de webhooks no es el mas apropiado, pero de momento seguiremos usandolo, se puede enteder como Metodo o Operacion e incluye la especificaicon del Metodo HTTP y ademas la posibilidad de especificar parametros.

En lo posible vamos a tratar de tener resultados parciales que podamos ir desplegando.

1. Tener una nueva accion (tag) que sea *Swagger*, que muestre la conversion a swagger del API Connection en modo de solo lectura. 

2. Mas adelante, debemos poder editar el Swagger y su edicion debe modificar la configuracion del API Connection correspondiente, o sea debe haber una sincronizacion entre el modelo API Connection (y sus referencias a Resources y Webhoks)  con el fichero Swagger.

3. Agregar a la vista del Swagger la opcion de visualizar el Swagger similar a Swagger Editor (http://editor.swagger.io/). Una variante es ver si es posible embeber el Swagger Editor en Cenit como alternativa a implementarlo desde cero.

### 23. Adicionar en el menú superior indicador para storages. [Aneli]

Cuando se esta logueado se muestran los monitors en ese grupo esta pendiente por adicionar a los storage.

### 22. Limitar el listado de acciones a 4 y luego un boton que diga more. [Aneli]

Un boton more, inmediatamente a la derecha de las primeras 4 acciones. 
Este boton debe permitir desplegar el resto de las acciones.

(Opcional) al lado del boton se puede mostrar entre parentisis la cantidad de accciones adicionales que hay.

### 21. Activar el modelo de Confirmable. [Mac]

Para poder activar el modulo confirmable es necesario migrar los datos y a todos los usuarios existente asignarle a confirmed_at  Date.today-1 

### 20. Mejorar y expandir el uso de los tags. [Aneli]

Los tags fueron adicionados por Daniel para los Algoritmos. Pero usan la interfaz por default de rails_admin para las relaciones Many to Many con dos text area uno al lado del otro, donde es posible seleccionar los tag y pasarlo a la otra area..

1. Mejorar la interfaz de los tags, para que sea un imput de múltiples tag con autocompletamiento. Revisar las librerias de JQuery existentes.

2. Adicionar los tags a otros modelos como las Collecciones y los Shared Collections, revisar que otros modelos se pueden beneficiar de esto, pero la intencion es que sea un patron que podamos relacionar con todos los modelos que necesitan funcionalidades que faciliten el *discovery*.

### 19. Mejorar el tour. [Aneli]

Del tour se hizo una primera implementacion en el portal anterior de Cenit por parte de Daniel, se puede ver aqui

- https://cenit-portal.herokuapp.com/

Y en repo

- https://github.com/cenit-io/cenit-portal

Luego esa implementacion se paso ha Cenit, se puede ver un link en el menu lateral derecho, pero en estos momento no esta funcional.

La propuesta es ir abriendo los elementos hojas del sidebar lateral de navegación, e ir expandiendo los niveles y colapsando en la medida que el tour avanza.

### 18. Cambiar los has_many en los index mostrando solo los primeros elementos y la cantidad. [Aneli]

Cambiar la vista por default de index de rails_admin, para que las columnas que se corresponden con una relación has_many mostrando los 3 primeros elementos de la lista y luego un número con la cantidad total de elementos

### 17. En el Show de los Shared Collections incluir un link a la lista de todos los Webhooks. [Aneli]

Cuando un Shared Collections que tiene muchos Webhooks, en el Show aparecen listado solo una parte de los Webhooks. Por ejemplo en caso de Gmail, solo se muestran 35 de un total de 56. Sería conveniente tener un link que al darle click redireccione a la pagina donde se listen todos los webhooks que pertenecen al Shared Collection.

### 16. Adicionar estadisticas de los monitors en el dashboard. [Mac]

En el dashboad se muestran 3 rectangulos con los *monitors*:

* running task
* autorizactions
* notifications

Cada uno debe mostrar la cantidad correspondiente. Esto cuando se este logueado y cuando no.

### 15. Push asincronos. [Mac]

Un push a Cenit mediante el API debe ser procesado de forma asíncrona, en el momento del push se debe retornar el *id* de una Tarea, de modo que posteriormente se pueda revisar el estado de la ejecución de la tarea.
Por ejemplo la tarea que se retorna asociada a un push puede estar relacionada con otras tareas.

Una tarea puede generar otras subtareas y se necesita recuperar ese arbol de dependencias para poder saber si todo se termino correctamente

### 14. Permitir múltiples usuarios por cuenta. [Mac]

Ya esta implementado la logica para poder tener multiples tenants por usuario, queda pendiente permitir múltiples usuarios por tenant.

Se debe tener al menos dos roles dentro de account, el role de  owner de la cuenta y  una con otro Rol (que en el futuro limite por ejemplo la vista de factura, o de adicionar usuarios y cambiar los roles dentro del tenant, etc)

El rol Owner tendria acceso en  el dashboard al area de administración

### 13. Revisar solapamientos entre Tenant y Namespace y entre Collection y Namespace. [Mac]

El Namespace como elemento base de los shared cross: 

Con la idea de simplificar toda la gestión de los namespace y su repetición en todos los formularios, podemos revisar la posibilidad de unificar los conceptos actuales de Tenants y Namespace siguiendo un poco el estilo de Github con las Organizaciones.

Cuando uno se crea una cuenta en github, tiene por una especie de ‘organización por default’ asociado al user_name, luego tiene la posibilidad de crear nuevas Organizaciones. Las Organizaciones hacen la funcionalidad de gestión modular, similar a la de un namespace, cada repo queda asociado a una organización (o la que llamamos organización por default del usuario). Esta lógica de Organización en Github permite además gestionar permisos y asociar usuarios, define el acceso por API. Cuando a un repo se le hace un fork, se puede decir que es equivalente a cambio de namespace.

Si unificamos en cenit los conceptos de Tenant y Namespace, podemos quedarnos solo con Tenant, manteniendo la lógica actual de crear un tenant por default asociado a una nueva cuenta, y luego se da la posibilidad de crear nuevos tenant. Si el tenant a la vez lo entendemos como un namespace, no es necesario en cada formulario tener un campo que especifique el namespace. Esto junto con la nuevas opciones de la UI que simplifican la forma en que se cambia de tenant a otro debe hacer que queden mas intuitivas y fácil estos conceptos a los usuarios.  

 Cuando a un Shared Collection se le haga pull, sería una especie de ‘fork’ quedando el collection dentro del namespace especificado por el tenant.

Por último en cuanto agreguemos la posibilidad de subdominio podemos, asociar cada tenant a un subdominio de cenit, con lo que la funcionalidad multi-tenant debe quedar mas explicita. 

El namespace como funcion de modularidad:

Otra pregunta podria ser: "Si ya tenemos el concepto de Collection para que necesitamos los Namespace?"

En cuanto a la logica actual, donde el namespace es lo que permite identificar que los diferentes modelos son relativos a un mismo Collection como Facebook, creo podemos usar el name de collection para sustituir ese uso de los namespace. Cualquier modelo nuevo que se cree podria pertener a un Collection. Cuando tengamos implementado el menu de Objetos, el primer nivel de navegacion podria ser el Collection, revisar la propuesta del menu lateral de objetos en esta presentacion (https://docs.google.com/presentation/d/1U7npFSNCPMDZDrDZyPNuP9blxEZmcxFGkDDvTFm2nqw/edit?usp=sharing) 


### 12. Usar las url con slug como url por default en lugar del ID. [Mac]

Ya en Cenit se soportan las url con slug y ademas de las id, en adicion seria conveniente que las url predeterminadas en la documentacion sean con slug. Esto ademas ayudaria a que sean indexadas por los motores de busqueda.

### 11. Eliminar ‘setup~’ prefijo de las url. [Mac]

Todas las url tienen el prefijo 'setup~' que lo toma rails_admin de la carpeta setup. eliminar este prefijo que no cumple funcion.

### 10. Redireccionar los link de notificaciones a filtros. [Aneli]

En el menu superior aparece un icon de las notificaciones y asociado con el icon diferentes numeros relacionados con el tipo de notificacion, cuando se le da click a uno de los numeros esta redireccionando a las notificaciones, pero no a las notificaciones filtradas por el tipo de notificacion del numero.

### 9. Cambiar el nombre del modelo Account por Tennant. [Mac].

Ahora en Cenit es posible tener asociado a un usario varias "Accounts" con lo cual es mejor renombrar el concepto de "Account" por "Tennant"

### 8. Definir un Segmento en los Datos asociado a un Data Event. [Mac]

Por ejemplo si se define un evento de Placed Order para las ordenes con status Placed
Que automáticamente en la navegacion del menu lateral se cree un subnivel para Placed Orders

Donde podamos inspeccionar este subconjunto de las ordenes, y tenga solamente los flujos asociados con ellas (en caso que existan flujos definidos)

Una misma orden puede estar en varios segmentos.

### 7. Los Récords por default deben ser visibles en la navegación. [Mac]

I)
Aun cuando hay casos como X12 que tienen cientos de de modelos, la mayoría de los shared collections que tenemos tiene pocos modelos.

El sidebar tiene hoy implementado un scroll que hace que no sea tan engorroso la navegación, además tendremos la opción de poderlos eliminar del menú si se desea. Incluso podemos agregar un acción sobre la lista, por ejemplo si se instala X12 se podría tener una opción en el collection (o en otro lugar mas visible) que permita eliminar todos los modelos de la navegación de records,

II)  La otra parte de la propuesta es en lugar de tener Records en la navegación sustituirlo por dos conceptos Objects y Files, correspondiendo a JSON Data Types y File Data Types.

III) Cuando no se este logueado que en el menú lateral aparezca Objects y Files pero que no se puedan expandir.

### 6. Mejorar navegación e interfaz de las Transformaciones. [Aneli, Mac]

Las transformaciones es uno de los conceptos principales que hemos desarrollado y en expresividad es comparable con los algoritmo u otros conceptos que tenemos.
Aun pueden ser usado como una parte impotante en los Flujos, la idea es que tengan valor en si mismo, y puedan ser usando de forma independiente.

I ) Incluir este concepto como un primer nivel en la navegación

* Transformations 
  * Render (type exporter)
    * HTML (html.erb, liquid)
    * JSON (json.rabl)
    * XML (xml.rabl, xslt)
    * JS (js.erb)
    * PDF (pdf.prawn)
    * CSV (csv.erb)
    * Text (txt.erb)
  * Parser (type importer)
  * Convert
  * Updater

 IV) Mejorar la UI a partir del hecho que cada una corresponderá a un tipo particular de transformations  a diferencia de como estábamos trabajando hasta ahora.

 III) Incluir la ventana de test que se implemento al principio
 
 
### 5. El email y el pdf de OSSE no soporta tildes. [Mac]
 
 Al parecer porque es UTF-8, hay que revisar la posibilidad de seleccionar el enconde
 
 
### 4. Generar los SDK para ruby, python, node.js. [Pacheco]
 
 Generar los SDK correspondientes al API de Cenit para los principales leguajes de programacion

### 3. Subdominios para las aplicaciones. [Pacheco]

Para que las aplicaciones tegan mayor valor de uso, es importante que se pueeda asociar un dominio o subdominio propios.

- www.userdomain.com
- www.sub.userdomain.com

Para esto debemos desplegar las aplicaciones en un sudominio de cenit.io, preferentemente generado alearotiamente, de modo que no tengamos colisiones con los subdominios que deben ser reservados a cenit. Ejemplo

- https://polar-wave-7672.cenit.io

Para esto tenemos que asociar un certificado wildcard con el dominio cenit.io

Hay que ver como es posible configurar Nginx para que dinamicamicamente pueda responder a estos dominios o subdominios propios

Por ejemplo para una web como mytriptomoon, podria tener una aplicacion para la autenticacion con varios provedores de identidad usando cenit, que desee que se visualice en:

https://signin.mytriptomoon.com

### 2. Agregar a la navegacion Ecommerce. [Mac]

Las motivaciones de este cambio son para hacer mas evidente las posibilidades que tiene Cenit para el mundo Ecommerce. Cenit es una plataforma genérica de integración, y técnicamente las funcionalidades para el tema ecommerce son similares a otros dominios de aplicación, pero es importante diferenciar ese segmento. Similar a Google Analitic, que permiten monitorear la actividad en el sitio web, definiendo eventos customizados de acciones específicas en la web que se desean monitorear, mas allá de la funcionalidad genérica tiene una seccion especifica para Ecommerce.

Propongo que en el menu de navegacion tengamos explicitamente un item para Ecommerce, y como segundo nivel tendriamos: Customers, Products, Orders, Shipments, Payments. Los modelos de ese namespace estarian pre-instalados en cada nuevo tenant que se lance.

* Ecommerce
  * Customers
  * Products
  * Orders
  * Payments
  * Shipments

Aunque se permitia cargar otros modelos tendriamos una biblioteca "oficial" de Ecommerce, de modo que siempre que los modelos sean algunos de los oficiales se pueda sacar provecho de ello y contar con funcionalidades Out the box para estos modelos.

Es importante notar que MondoDB permite que cuando persista una orden en particular, pueda tener tener campos dinamicos, o sea atributos adicionales a los especificados originalmente en el modelo, lo que brinda flexibilidad a los mapeos, de hecho esos atributos dinamicos pueden ser incluso anidados.

En los SDK que desarrollemos podemos tener facilidades para el push de estos modelos hacia Cenit. O una plataforma ecommerce como Spree o Magento, puede tener una extension para la sincronizacion de estos modelos. Por ejemplo cualquiera de estos Store, con una extencion puede implementar una logica de push automatico que se ejecute automaticamente que se cree una nueva orden, lo cual tiene ventajas a la hora de lanzar eventos sin que se tenga que esperarar por una instancia del scheduler periodico cada 20 minutos.
Veamos algunos ejemplos:

En el caso de Sathechi, las ordenes de cada uno de los marketplace es traducida a los Shipments de Shipstation.
lo ideal es que exista integraciones de:

- Order Fancy <-> Order Ecommerce
- Order OverStock <-> Order Ecommerce
- Order Shipstation <-> Order Ecommerce

La ventaja de este enfoque es que cualquier funcionalidad que se haga a partir de Order Ecomerce queda disponible por transitividad para todos los modelos Order que sean posible transformarce en Order Ecommerce.

Escenario 1:

Si de momento en lugar de enviar a Shipstation, lo que interesa es hacer el envio a Shipwire, el esfuerzo se debe reducir a transformar la Order (o el Shipment de Shipwire) en la Order de ecommerce

Escenario 2:

Si tenemos una funcionalidad que a partir de un Order se genere un Invoice pdf con un template prawn
Aunque del punto de vista de implementacion, no debe cambiar mucho, ya que deben ser modelos que se carguen dinamicamente, el hecho de que tengan una UI propia, permite agregar actions que se puedan visualizar desde el mismo dashboard.

Podriamos tener en el API una descripcion explicita para estos modelos, de modo que la curva de aprendizaje para que alguien logre subir una Orden a Cenit sea menor.


### 1. Algoritmos remotos. [Pacheco]

Cenit Algorithms

En Cenit podemos pensar en dos tipos de algoritmos, local or remote, 

Los algoritmos locales: son los que tenemos actualmente, tiene full acceso a la bd de cenit, de momento solo soportados en ruby, y no permiten referencias a bibliotecas. Deben poderse ejecutar de forma sincrona o asincrona

Algoritmos remotos: la comunicación con cenit sería mediante el api, y debe ser programada, soportados múltiples lenguajes mediante la tecnología del buildpacks,  permiten incluir referencias a bibliotecas. Deben ser siempre ejecutados de forma asíncrona.

Cada ejecución del algoritmo es representada por una tarea asíncrona en Cenit.

De forma opcional el output es definido por un DataType. Cada ejecución del algoritmo puede tener un set de objetos del data type (con cenit, pueden ser exportados como JSON, XML, CSV, etc)


Algoritmos remotos

Un algoritmo por default no tendría nada para la comunicación con los modelos de Cenit. Pero para lograr esto podemos en el template (un gist) agregar una secuencia de pasos comentados, que permitan leer los parametros del algoritmo desde cenit, mediante un push (HTTP Post) retornar el resultado del algoritmo a cenit.

Del mismo modo puede estar comentadas otras operaciones con el API de cenit. En caso que se desee leer objetos del setup(conectores, tareas etc)

Por ejemplo el template para ruby, tendría el Gemfile, Gemfile.lock y un algorithm.rb, un template similar al que crea morph.io, por ejemplo:
https://github.com/sanchojaf/city_test3/blob/master/scraper.rb

Como el algoritmo puede ser público es importante que las credenciales se suban al buildpack como variables de ambiente.


Input

curl GET -H "X-User-Access-Key: N63563526" -H "X-User-Access-Token: TYQTWY454521QQ12" \
https://www.cenit.io/api/v1/algo/#namespace/#algo_name/input

Json 

```Json
-> {
    "input": ["transformer","retransform"],
}
```

Output

```bash
curl -H "Content-Type: application/json"\
     -H "X-User-Access-Key: N446264203"\
     -H "X-User-Access-Token: 5T6YJqGYJgE5cULq6WQ_"\
     -X POST -d '{“output": json_result}'\
     https://www.cenit.io/api/v1/algo/#namespace/#algo_name/output
```

Con ejecución del curl anterior desde el algoritmo, podemos en cenit, garantizar que el algoritmo esté asociado con cada uno de los output. (mostrándolo similar a como lo hace cenit)

Del mismo modo el algoritmo puede realizar un push a cualquier otro modelo de cenit, o invocando otras acciones del API de cenit.


En función del lenguaje que se seleccione para el algoritmo, pondremos una alternativa de curl para el lenguaje específico (Ruby, Python, Node.js), por ejemplo en el caso de Python algo como.


Version de python

```Ruby
import json,httplib
connection = httplib.HTTPSConnection( https://www.cenithub.com/api/v1', 443)
connection.connect()
connection.request('GET', 'algo/#namespace/#algo_name/input', json.dumps({
       "input":  ["transformer","retransform"],
), {
       "X-User-Access-Key": "${APPLICATION_ID}",
       "X-User-Access-Token": "${REST_API_KEY}",
       "Content-Type": "application/json"
     })
result = json.loads(connection.getresponse().read())
print result
```

Modificar los parametros de entrada y la salida de los algoritmos

Por cada parámetro de entrada, debemos:
Eliminar la descripcion del parámetro (el algoritmo tiene una descripcion donde se puede describir los parametros), ademas el nombre debe ser suficiente para que se entienda de qué es el parámetro.
Especificar si el parámetro corresponde a una lista o un solo elemento, por default asumir que es un solo elemento
Poder asociar de forma opcional un Validator. El Validator puede ser un schema o cualquier otro tipo de validador.
Permitir definir un valor por default del parámetro. 
Especificar si el parámetro es obligatorio u opcional (por default obligatorio). 

El algoritmo debe tener un área que sea Sample, donde se pueda asociar un conjunto de valores correspondiente a cada uno de los  parametros de entrada. 

En la pestaña Run en lugar de tener un textarea para el imput, se debe cargar un field imput por cada parámetro de entrada con el label que sea el name del parámetro, debe poder cargar el valor por default en caso que esté’ definido, si el parámetro es una lista, se deben poder entrar los valores de entrada separado por signo de coma.

Si el algoritmo tiene un sample definido, En el Run debe aparecer un checkbox que sea ‘load sample’ por default en false. Si se marca en true todos los parametros de entrada  toman los valores correspondientes definidos en el sample..

Debe existir un tiempo maximo de ejecucion para el algoritmo síncrono, y un tiempo máximo para el asíncrono (en este último se debe permitir un tiempo mayor de ejecución). Esa información de los tiempos máximos debe aparecer como una info en el Run,

(La funcionalidad a continuación podemos dejarla para más adelante)
En relación con la salida de los algoritmos, cuando se seleccione validar la salida, se debe poder seleccionar varios Validators, los validators pueden ser un schema o cualquier otro validator, si está seleccionado un Data Type de salida, y se marca validar se puede cargar ese mismo esquema como un primer validator, pero el usuario puede eliminarlo si lo desea.

Agregar un nuevo action para mostrar el output de la última ejecución visualmente similar a la página a la que se llega cuando se le da click al icon de records de el  output más reciente que se muestra en show. La idea es que la última ejecución este’ más jerarquizada que el resto de las ejecución y que sea sencillo inspeccionarla, exportar los datos, etc


Sobre el el modelo Algorithm Output:
Almacenar el valor de los parametros de entrada.
Hay que buscar la manera de poder salvar el inicio de la ejecución y la duración.

Hay una herramienta q es una variante open source ligera de heroku, se llama dokku. Heroku hizo open source los buldpacks, la mayoria de las plataforma de computo azure, google cloud. Permite desplegar una app a partir del buildpack. En cenit queremos correr buildpaks en diferentes lengiajes. Eso seria prinero para los algoritmos en cenit. Scripts con referencias a bibliotecas, ruby, python, node.js pero tambien para un concepto de aplicaciones q tenemos en cenit, hoy son aplicaciones sinatras pero podrian ser un aplicacion web definida por buildpack

Dokku tiene un deamon. Seria trabar en un api para dokku. Donde se pueda hacer un despliegue de una app programatixamente


# done

### 32. ~~Actualizar la pagina actual de la documentacion del API.~~ [Mary] 

Actualizar la documentacion del API, en correspondencia con el Swagger.

La URL de documentacion del API es:

- http://cenit-io.github.io/docs/api/

La URL del Swagger es:

- https://cenit.io/openapi/v1/swagger.json

Para actualizar la pagina de documentacion se debe modificar dos ficheros JS:

- https://github.com/cenit-io/docs/blob/gh-pages/api/api_project.js
- https://github.com/cenit-io/docs/blob/gh-pages/api/api_data.js

Esta actualizacion debe ser temporal porque debemos lograr que la pagina de documentacion del API se genere automaticamente a partir del fichero Swagger.

### 31. ~~Crear tarea que genere el swagger.json a partir del swagger.yml~~ [Mary]

La generacion del swagger.json debe ser programatica de modo que cada vez que se modifique el swagger.yml sea posible ejecutar un *rake task* como

    rake openapi:ymltojson

Que lea el yaml:

    /public/openapi/v1/swagger.yaml

y sobreescriba el json:

    /public/openapi/v1/swagger.json

### 35. :bug: ~~Cenit local no esta salvando correctamente los objetos.~~ [Mac]

En mi instancia local de Cenit, cuando creo los namespace no aparecen luego en el listado del index

Lo mismo me paso creando un JSON Data Type, cuando doy save aparentemente salva satisfactoriamente, pero luego el listado aparece vacio.

Cree una cuenta nueva y paso lo mismo, previendo que mi cuenta estuviese corrupta.
