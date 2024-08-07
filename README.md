# Prueba Técnica - Respuestas y Código

## Respuestas a Preguntas de Opción Múltiple

1. **Estás construyendo una API de alto rendimiento para una plataforma de comercio de criptomonedas. En esta plataforma, el tiempo es extremadamente importante porque los microsegundos cuentan al procesar órdenes de comercio de alto volumen. Para comunicarte con la API, quieres elegir el verbo que sea el más rápido para operaciones de solo lectura.**

¿Qué verbo deberías elegir para recuperar órdenes de comercio con la API?
   - **Respuesta:** GET
   - **Explicación:** `GET` verbo para operaciones de solo lectura porque es diseñado para recuperar datos sin modificar el estado del recurso. Este método se usa para leer o recuperar datos del servidor
     
- **Ejemplo:**
  
```javascript
// Uso módulo Express para crear una API
const express = require('express');
const app = express();

// Definimos una ruta para obtener órdenes de comercio con GET
app.get('/api/trade-orders', (req, res) => {
    // lógica para obtener las órdenes con GET;
    res.json(orders);   // Respondemos al cliente con la lista de órdenes de json.
});
```
2. **Trabajas para una empresa de Gestión de Relaciones con Clientes (CRM). Los clientes de la empresa acceden al CRM a través de una API RESTful. El CRM permite a los clientes agregar información de contacto para clientes, prospectos y personas relacionadas (por ejemplo, asistentes virtuales o directores de marketing). Quieres elegir una ruta de solicitud de API adecuada para que los clientes puedan recuperar fácilmente la información de un solo contacto, al mismo tiempo que sea flexible para futuros cambios en el software.**

¿Cuál de las siguientes rutas de API deberías usar?
   - **Respuesta:** /contacts/{contact_id}
   - **Explicación:** permite acceder a cualquier contacto específico usando su identificador único (contact_id), sin importar si el contacto es un cliente o cualquier otro tipo de contacto, se puede buscar directamente con esta ruta.

En comparación con las otras opciones:
/customers/{customer_id} se limita solo a customers, no a otros tipos de contactos.
/contacts/{contact_type}/all recupera todos los contactos de un tipo específico, no uno solo.
/customers/all solo devuelve todos los clientes, no permite buscar un contacto específico.

- **Ejemplo:**
```
// Ruta para obtener un solo contacto usando su ID
app.get('/api/contacts/:contact_id', (req, res) => {
    const contactId = req.params.contact_id; // Obtenemos el ID del contacto de la URL
    // lógica para buscar el contacto.
    const contact = { id: contactId, name: "Juan" }; //objeto se generara a partir de una base de datos 
    res.json(contact); // Respondemos al cliente con la información del contacto en fomato JSON.
});
```
3. **Trabajas para una gran red social y se te ha asignado la tarea de manejar errores para la API. Estás tratando de decidir un código de error apropiado para fallos de autenticación basados en usuarios inexistentes y contraseñas incorrectas. Quieres equilibrar la seguridad contra ataques de fuerza bruta con proporcionar códigos de error descriptivos y precisos.**
¿Qué código(s) de error HTTP deberías usar para mantener el sistema seguro y al mismo tiempo informar que ocurrió un error?

- **Respuesta:** 404 si el usuario no existe, y 403 si la contraseña es incorrecta.
- **Explicación:**  404 indica que el recurso solicitado no se encuentra en el servidor es decir oculta la existencia de usuarios (utilizando 404) mientras se indica indica que el servidor entiende la solicitud, pero se niega a autorizarla, que las credenciales proporcionadas son incorrectas (utilizando 403). 

- **Ejemplo:**
```
// Ruta para autenticar a un usuario
app.post('/api/authenticate', (req, res) => {
    const username = req.body.username; // Obtener nombre del ususario
    const user = {}; // Buscar el usuario en la base de datos

    if (!user) {
        return res.status(404).json({ error: 'User not found' }); // Si no encontramos el usuario mostramos error 404}

    const passwordValid = false; // Verificar la contraseña que este correcta sino:
    if (!passwordValid) {
        return res.status(403).json({ error: 'Invalid password' }); // Si incorrecta se muestra error 403
    }
    res.status(200).json({ message: 'Authenticated successfully' }); // Si todo es correcto se muestra 200
});
```
4. **Estás escribiendo la documentación para solicitar información sobre un usuario específico en tu sistema. Tu sistema utiliza UUIDs (identificadores únicos universales) como identificadores de usuario. En tu documentación, quieres mostrar un ejemplo.**
Verdadero o falso: Deberías poner un UUID falso en el código de ejemplo (en lugar de solo el texto "UUID") como marcador de posición.

- **Respuesta:** True
- **Explicación:** Poner un UUID falso en el código de ejemplo es una buena práctica porque proporciona una representación realista de cómo se vería un UUID. Esto ayuda a los usuarios a entender mejor cómo deben formatear y usar los UUIDs en sus solicitudes
- **Ejemplo**

```
  // Ejemplo de un UUID que se podría usar en la documentación:
GET /api/users/123e4567-e89b-12d3-a456-426614174000

//Utiliza un UUID de formato estándar (8-4-4-4-12 caracteres hexadecimales con guiones), lo que ayuda a los usuarios a ver exactamente cómo debería verse un UUID válido en una solicitud real.
```
5.**Estás construyendo código para manejar errores emitidos por un servidor API remoto. La respuesta puede o no contener un error.**
¿Cuánto trabajo debería manejar tu método handleErrors(response)?

- **Respuesta:** Verificar la presencia de un error. Si existe, asignar el error a una propiedad de la clase, luego lanzar una excepción.
- **Explicación:** 
- **Ejemplo**
```
function handleErrors(response) {
    // Comprobar si el objeto tiene un error
if (response.error) {
    throw new Error("API Error: " + response.error); // Se muestra error en caso de existir
}

```

6.**Tienes dos clases: un controlador de base de datos y un controlador de correos electrónicos. Ambas clases necesitan manejar errores para que tu interfaz de usuario muestre cualquier error que ocurra en tu plataforma.**
¿Cómo deberías implementar este manejo de errores?
- **Respuesta:** Crear un proveedor de errores basado en los controladores para manejar errores en todas las clases que puedan emitir errores.
- **Explicación:** Esta opción brinda una solución centrada para el manejo de errores que pueda ser utilizada por cualquier clase que genere errores. Esto asegura una implementación uniforme y coherente del manejo de errores en toda la plataforma, facilitando la gestión y visualización de errores en la interfaz de usuario.
- **Ejemplo**

```
class ErrorProvider {
    // Clase para manejar los errores en todo el sistema
    static handleError(error) {
        }
}

class DatabaseDriver {
    connect() {
        try {
            // Conexion a la base de datos
            throw new Error("Connection failed!"); // en caso que falle
        } catch (error) {
            ErrorProvider.handleError(error); // entonces aplicamos el proveedor de errores
        }
    }
}

```

7.**Necesitas nombrar el método privado en tu clase que maneja el recorrido de productos de comercio electrónico para recopilar y analizar datos. Estos datos se almacenan en un arreglo y se configuran como una propiedad de la clase.**
¿Cuál de las siguientes opciones deberías usar para nombrar tu método?
- **Respuesta:** _collectAndParseProducts.
- **Explicación:** Indica que el método se encarga tanto de la recopilación como del análisis de los productos

8.**Hay múltiples lugares en tu base de código que necesitan acceder a la base de datos. Para acceder a la base de datos, necesitas proporcionar credenciales. Quieres equilibrar la seguridad con la facilidad de uso.**
¿Qué estrategia deberías usar para almacenar y acceder a estas credenciales?
- **Respuesta:** Poner las credenciales en un archivo .env, cargar los datos desde él en un sistema de configuración, y luego solicitar las credenciales a un proveedor de servicios de base de datos es la más adecuada
- **Explicación:** el uso de archivos .env para almacenar información sensible, y gestionar las credenciales de manera centralizada reduce el riesgo de exposición accidental de las credenciales y simplifica su administración.
  
**Ejemplo**
```
- // Obtenemos las credenciales desde el archivo .env
const DB_USER = process.env.DB_USER;
const DB_PASSWORD = process.env.DB_PASSWORD;

function connectToDatabase() {
    // usa las credenciales obtenidas para realizar una conexión a la base de datos
    console.log(`Conectando a la base de datos con el usuario: ${DB_USER}`);
}
```
