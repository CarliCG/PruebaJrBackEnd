# Prueba Técnica - Respuestas y Código

## Respuestas a Preguntas de Opción Múltiple

1. **You're building a high-throughput API for a cryptocurrency trading platform. For this platform, time is extremely important because microseconds count when processing high-volume trade orders. For communicating with the API, you want to choose the verb that is fastest for read-only operations.**

What verb should you choose for retrieving trade orders with the API server?
   - **Respuesta:** GET
   - **Explicación:** `GET` verbo para operaciones de solo lectura porque es diseñado para recuperar datos sin modificar el estado del recurso. Este método se usa para leer o recuperar datos del servidor
   - 
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
2. **You work for a Customer Relationship Management (CRM) company. The company's clients gain CRM access through a RESTful API. The CRM allows clients to add contact information for customers, prospects, and related persons (e.g., virtual assistants or marketing directors). You want to choose an appropriate API request path so clients can easily retrieve information for a single contact while also being flexible for future software changes.**

Which of the following API paths should you use?
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
3. **You work for a large social media network, and you've been tasked with error handling for the API. You're trying to decide on an appropriate errorcode for
authentication failures based on non-existent users and incorrect passwords. You want to balance security against brute force attacks with providing descriptive
and true error codes.**

Which HTTP error code(s) should you use to keep the system secure and still report that an error occurred?
- **Respuesta:** 404 if the user doesn't exist, and 403 if the password is wrong.
- **Explicación:** Permite ocultar la existencia de usuarios (utilizando 404) mientras se indica que las credenciales proporcionadas son incorrectas (utilizando 403). Esto ayuda a evitar que atacantes obtengan información sobre usuarios válidos mientras que el sistema aún responde adecuadamente a fallos de autenticación.

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
