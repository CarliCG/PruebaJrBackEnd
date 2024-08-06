# Prueba Técnica - Respuestas y Código

## Respuestas a Preguntas de Opción Múltiple

1. **You're building a high-throughput API for a cryptocurrency trading platform. For this platform, time is extremely important because microseconds count when processing high-volume trade orders. For
communicating with the API, you want to choose the verb that is fastest for read-only operations.**
What verb should you choose for retrieving trade orders with the API
server?
   - **Respuesta:** GET
   - **Explicación:** `GET` verbo para operaciones de solo lectura porque es diseñado para recuperar datos sin modificar el estado del recurso. Este método se usa para leer o recuperar datos del servidor
- **Ejemplo:**
  
```javascript
// Usamos el módulo Express para crear nuestra API
const express = require('express');
const app = express();

// Definimos una ruta para obtener órdenes de comercio
app.get('/api/trade-orders', (req, res) => {
    // Aquí iría la lógica para obtener las órdenes; por ahora, devolveremos un array vacío.
    const orders = [];  // Esto debería ser el resultado de una base de datos.
    res.json(orders);   // Respondemos al cliente con la lista de órdenes.
});
