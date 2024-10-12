# Contenido

Este repositorio contiene dos carpetas: **Funcional** y **NoFuncional**.

## Funcional

En la carpeta **Funcional**, encontrarás la colección de Postman `technicalTest.postman_collection.json`, que incluye todas las validaciones realizadas a los endpoints requeridos para la prueba técnica funcional. Cada carpeta dentro de esta sección cuenta con documentación específica para cada caso de prueba, la cual también se añadirá a este documento.

## NoFuncional

En la carpeta **NoFuncional**, encontrarás:
- El archivo de plan de pruebas de JMeter: `PruebaTecnica.jmx`, donde se encuentran las configuraciones realizadas para ejecutar las pruebas de carga y estrés de acuerdo a los requisitos especificados.
- El documento `Informe de Pruebas de Carga y Estrés de API.docx`, que es un resumen ejecutivo de los resultados de las pruebas de rendimiento.
- Las carpetas `01-150 Users` y `02-100 to 1000 Users`, que contienen los datos de las pruebas y el respectivo reporte en HTML.


### Casos de Prueba de la Prueba Funcional

1. **getProductByCategory**
   - **Título del Caso de Prueba**: Verificar la respuesta de la API para la categoría de productos electrónicos
   - **Descripción**: Este caso de prueba valida que el endpoint responda correctamente al realizar una solicitud GET a la categoría de productos electrónicos, asegurando que se reciba un código de estado 200 y que todos los productos pertenezcan a la categoría correcta.
   - **Endpoint**: `https://fakestoreapi.com/products/category/electronics`
   - **Método HTTP**: GET
   - **Resultados Esperados**:
     - **Código de estado**: 200
     - **Respuesta esperada**: Un array de objetos que representan productos, donde cada objeto debe tener un campo `category` con el valor 'electronics'.

2. **getProductDetails**
   - **Título del Caso de Prueba**: Verificar la respuesta de la API al consultar un producto específico
   - **Descripción**: Este caso de prueba valida que el endpoint responda correctamente al realizar una solicitud GET para consultar el producto con ID 2, asegurando que se reciba un código de estado 200 y que la respuesta cumpla con el esquema JSON definido.
   - **Endpoint**: `https://fakestoreapi.com/products/2`
   - **Método HTTP**: GET
   - **Parámetros de entrada**:
     - **Path Params**:
       - **ID**: 2 (ID del producto a consultar)
   - **Resultados Esperados**:
     - **Código de estado**: 200
     - **Respuesta esperada**:
       ```json
       {
         "id": 2,
         "title": "Mens Casual Premium Slim Fit T-Shirts",
         "price": 22.3,
         "description": "Slim-fitting style, contrast raglan long sleeve, three-button henley placket, light weight & soft fabric for breathable and comfortable wearing.",
         "category": "men's clothing",
         "image": "https://fakestoreapi.com/img/71-3HjGNDUL._AC_SY879._SX._UX._SY._UY_.jpg",
         "rating": {
           "rate": 4.1,
           "count": 259
         }
       }
       ```

3. **addNewProduct**
   - **Título del Caso de Prueba**: Verificar respuesta exitosa al crear un nuevo producto
   - **Descripción**: Este caso de prueba valida que el endpoint responda correctamente al enviar una solicitud POST para crear un nuevo producto, asegurando que se reciba un código de estado 200 y que la respuesta contenga los datos del producto creado con las propiedades correctas.
   - **Endpoint**: `https://fakestoreapi.com/products`
   - **Método HTTP**: POST
   - **Body**:
     ```json
     {
       "title": "name",
       "price": "price",
       "description": "description",
       "image": "image",
       "category": "category"
     }
     ```
   - **Resultados Esperados**:
     - **Código de estado**: 200
     - **Respuesta esperada**:
       ```json
       {
         "id": "nuevo_id",
         "title": "name",
         "price": "price",
         "description": "description",
         "image": "image",
         "category": "category"
       }
       ```

4. **updateProduct**
   - **Título del Caso de Prueba**: Verificar respuesta exitosa al actualizar un producto
   - **Descripción**: Este caso de prueba valida que el endpoint responda correctamente al enviar una solicitud PUT para actualizar un producto existente, asegurando que se reciban los datos actualizados y se verifique el tipo de datos correcto.
   - **Endpoint**: `https://fakestoreapi.com/products/{{id}}`
   - **Método HTTP**: PUT
   - **Parámetros de entrada**:
     - **Body**:
       ```json
       {
         "title": "name",
         "price": "price",
         "description": "description",
         "image": "image",
         "category": "category"
       }
       ```
   - **Resultados Esperados**:
     - **Código de estado**: 200
     - **Respuesta esperada**:
       ```json
       {
         "id": "{{id}}",
         "title": "name",
         "price": "price",
         "description": "description",
         "image": "image",
         "category": "category"
       }
       ```

   - **Pasos**:
     1. Ejecutar la solicitud `addNewProduct` para crear un nuevo producto y obtener su ID.
     2. Ejecutar el endpoint de actualización `updateProduct`.

5. **DeleteProducts**
   - **Título del Caso de Prueba**: Verificar eliminación de productos
   - **Descripción**: Este caso de prueba valida que se eliminen correctamente los productos de la categoría "electronics" con un precio inferior a 100, asegurando que la respuesta de eliminación contenga el producto correcto.
   - **Explicación del Uso de `pm.sendRequest`**:
     En la obtención de productos, se utiliza el endpoint `GET https://fakestoreapi.com/products` para recuperar todos los productos de la API. Este primer paso es crucial porque permite obtener los productos que cumplen con ciertos criterios, en este caso, aquellos que tienen un precio inferior o igual a 100 y pertenecen a la categoría "electronics". Después de obtener la lista de productos, se realiza un análisis para filtrar aquellos que cumplen con las condiciones especificadas. La función `pm.sendRequest` se emplea para iterar sobre cada uno de los identificadores de productos (`productId`) que se han recopilado y, en base a estos, se envía una solicitud DELETE a la API para eliminar cada producto.
   - **Endpoint**: `https://fakestoreapi.com/products/${productId}`
   - **Método HTTP**: DELETE
   - **Headers**: No se requieren headers específicos para esta solicitud.
   - **Parámetros de entrada**:
     - **Path Parameter**:
       - `productId`: ID del producto a eliminar, que se obtiene de la lista de productos de la prueba anterior.
   - **Resultados Esperados**:
     - **Código de estado**: 200 (o el que la API defina para la eliminación exitosa)
     - **Respuesta esperada**: Un objeto que contiene al menos el campo `id` del producto eliminado.


