# ProyectSolana - Registro de Sensores DePIN

## Link al código funcionando en Solana Playground

[https://beta.solpg.io/69ee91a974a75cd49b9875e6](https://beta.solpg.io/69ee91a974a75cd49b9875e6)

## ¿Qué hace este proyecto?

Es un registro descentralizado de sensores físicos en la blockchain de Solana. Cualquier persona puede registrar sus propios sensores y actualizar sus lecturas en tiempo real.

Este proyecto pertenece a la categoría "DePIN" (Redes de Infraestructura Física Descentralizada), donde dispositivos del mundo real como sensores de temperatura, humo o movimiento interactúan con la blockchain.

## ¿Cómo funciona el código?

### Estructura del programa

El programa permite **4 operaciones principales**:

1. **Crear un sensor** - Se registra un nuevo sensor con:
   - ID único
   - Ubicación (ej: "Laboratorio Mecatrónica")
   - Tipo de sensor (ej: "Temperatura", "Movimiento", "Humo")

2. **Actualizar lectura** - El dueño del sensor puede registrar una nueva medición

3. **Desactivar sensor** - Marca el sensor como inactivo (no se elimina de la blockchain)

4. **Reactivar sensor** - Vuelve a activar un sensor que estaba desactivado

### Uso de PDAs (Program Derived Addresses)

Cada sensor tiene su propia **cuenta única** generada con una PDA. La dirección se calcula usando:
- La palabra `"sensor"` como semilla
- La dirección pública del dueño
- El ID del sensor

Esto garantiza que cada sensor tenga una dirección predecible y única en la blockchain.

### Datos que guarda cada sensor

```rust
pub struct Sensor {
    pub owner: Pubkey,        // Quién es el dueño
    pub id: u64,              // ID del sensor
    pub ubicacion: String,    // Lugar físico
    pub sensor_type: String,  // Tipo (temperatura, humo, etc.)
    pub ultima_lectura: f64,  // Último valor medido
    pub activo: bool,         // Estado (activo/inactivo)
}
