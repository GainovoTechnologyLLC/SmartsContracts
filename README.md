🚀 Contratos Inteligentes Gainovo


📋 Contratos Implementados


1.	🪙 ARG (Activo Renta Gainovo)

Token principal del ecosistema Gainovo que representa derechos sobre una estrategia de Renta Dolarizada compuesta por renta variable cripto, Ganadería y bienes raíces.

Características de Seguridad:

✅ Sistema Multi-Firma: Mínimo 3 propietarios, aprobación por consenso (2/3)

✅ Lista Blanca/Negra: Control de direcciones autorizadas/bloqueadas

✅ Mecanismo de Pausa: Congelación inmediata de transferencias por situacion critica de seguridad

✅ Rol de Emergencia: Respuesta rápida a situaciones críticas

✅ EIP-2612 Permit: Transacciones sin gas para mejor UX

Funciones Principales:

// Gestión multi-firma function proponerMintear(address destino, uint256 cantidad) function proponerQuemar(address destino, uint256 cantidad) function confirmarPropuesta(uint256 idPropuesta) function ejecutarPropuesta(uint256 idPropuesta)

// Control de acceso function agregarAListaBlanca(address cuenta)

// Solo gestores function agregarAListaNegra(address cuenta)

// Solo gestores function pause()

// Solo emergencia function unpause()

// Solo emergencia


2.	⚡ GNT (Gainovo Trading)

Token especializado para trading y arbitraje en exchanges descentralizados.

Características Únicas:

✅ Supply Fijo: 5,000,000 tokens máximo

✅ Re-minting Controlado: Solo posible si se han quemado tokens previamente

✅ Optimizado para DEXs: Compatibilidad con Uniswap, Sushiswap, etc.

✅ Mismas Garantías de Seguridad: Multi-firma, listas, pausa de emergencia

Diferencias con ARG:

Propósito:Trading vs Renta

Supply: Fijo (5M) vs Incremental

Enfoque: Alta liquidez vs Largo plazo


3.	📤 MultiSender Gainovo

Sistema de distribución masiva para entregas simultáneas de tokens comprados y bonos multinivel.
Funcionalidades:

✅ Distribución Simultánea: Múltiples tokens en una transacción

✅ Gestión de Tres Assets: Token primario, token secundario y ETH

✅ Sistema Multi-Firma: Mismas garantías de seguridad

✅ Protección contra Reentrancy

Funciones de Distribución:

// Distribución combinada function enviarPrimarioyETH( address[] destinatariosPrimario, uint256[] montosPrimario, address[] destinatariosETH, uint256[] montosETH )

// Distribución simple de bonos function enviarSecundarioa1(address destinatario, uint256 monto)

🛡️ Sistema de Seguridad Integrado

🔐 Multi-Firma

Mínimo 3 propietarios requeridos Aprobación por consenso (2/3 de los propietarios) 24 horas de expiración para propuestas Transparencia completa mediante eventos

📋 Listas de Control

Lista Blanca: Restringe operaciones a direcciones autorizadas

Lista Negra: Bloquea direcciones maliciosas 

⏸️ Mecanismo de Pausa

Congelación inmediata de todas las transferencias Activación por rol de emergencia (sin multi-firma requerida) Reanudación mediante multi-firma 🚨 Rol de Emergencia

Respuesta inmediata a situaciones críticas Capacidad de pausa sin requerir aprobación múltiple Acceso limitado y altamente auditado

🔄 Integración con Gainovo Keysafe

Protección de Fondos para Usuarios:

✅ Recuperación de cuentas comprometidas

✅ Restauración de acceso por pérdida de claves

✅ Protección contra hackeos y phishin

✅ Proceso verificado con múltiples factores de autenticación

Cómo Funciona:

1-Verificacion de Pregunta de Seguridad

2-Usuario bloquea billetera con boton de emergencia irreversible

3-Se crea nueva billetera Gainovo

4-Reporta incidente

5-Transferencia segura de fondos a nueva dirección dentro de las proximas 72hs

////////////////////////////////////////////////////////////////////////////////

💼 Casos de Uso Principales

Para ARG:
Inversión en estrategia Renta Polarizada Recepción de rentas generadas Holding a largo plazo

Para GNT:
Trading en exchanges descentralizados Arbitraje entre diferentes plataformas Operaciones de alta frecuencia Para MultiSender:
Entrega de tokens comprados + bonos multinivel Distribuciones masivas (airdrops, recompensas) Pagos simultáneos a múltiples destinatarios ⚠️ Características de Seguridad Comunes

Todos los contratos incluyen:

✅ Modifiers de acceso: soloPropietario, soloGestor, soloEmergencia

✅ Validación de entradas: Verificación de direcciones y montos

✅ Eventos de auditoría: Tracking completo de todas las operaciones

✅ Protección contra reentrancy: Imposibilidad de ataques recursivos

✅ Manejo seguro de errores: Revertimientos claros y específicos

🎯 Beneficios para Usuarios

Seguridad Garantizada: Multi-firma y mecanismos de emergencia

Recuperación de Fondos: Respaldado por Gainovo Keysafe

Transparencia Total: Todas las operaciones auditables on-chain

Flexibilidad: Diferentes tokens para diferentes propósitos Protección

Proactiva: Listas blanca/negra y capacidad de pausa

ANEXO TÉCNICO - StakingDinamicoGainovo
🔍 Descripción General
Contrato de staking dinámico con gestión multifirma que permite a los usuarios depositar tokens para obtener recompensas, con tasas variables según el balance disponible y múltiples mecanismos de seguridad.

🏗️ Arquitectura del Contrato

📊 Estructuras de Datos Clave

Stake

solidity

struct Stake {

	uint256 inicio;        // Timestamp del inicio del stake
    uint256 cantidad;      // Cantidad de tokens staked
    uint256 intereses;     // Intereses acumulados (calculados al finalizar)
    bool finalizado;       // Estado del stake
}

Propuesta (Multifirma)

solidity

struct Propuesta {

	address creador;       // Propietario que creó la propuesta
    uint8 tipo;            // Tipo de propuesta (8 tipos disponibles)
    address direccionAfectada; // Dirección involucrada
    uint256 valorNumerico; // Valor numérico (montos, índices, plazos)
    uint8 confirmaciones;  // Número de confirmaciones recibidas
    uint40 timestamp;      // Momento de creación
    bool ejecutada;        // Estado de ejecución
    address destino;       // Destino de fondos (para ciertas propuestas)
}

Tasa Histórica

solidity

struct TasaHistorica {

	uint256 timestamp;     // Momento del cambio de tasa
    uint256 tasa;          // Valor de la tasa en ese momento
}

⚙️ Tipos de Propuestas Disponibles

Código	Tipo	Descripción

1	AGREGAR_PROPIETARIO	Agregar nuevo propietario al sistema multifirma

2	ELIMINAR_PROPIETARIO	Eliminar propietario existente

3	FINALIZAR_STAKE	Finalizar stake de usuario por seguridad

4	RETIRAR_RECOMPENSAS	Retirar tokens de recompensa del contrato

5	CAMBIAR_TOKEN_STAKE	Cambiar el token usado para staking

6	CAMBIAR_TOKEN_RECOMPENSA	Cambiar el token de recompensa

7	CAMBIAR_PLAZO_MINIMO	Modificar el tiempo mínimo de staking

8	RETIRAR_STAKE_TOKENS	Retirar tokens de stake del contrato

🔄 Flujos Principales

1. Stake por Usuario Directo

text

Usuario → iniciarStake(cantidad)

    ├── Valida cantidad mínima
    ├── Transfiere tokens al contrato
    ├── Crea registro de stake
    ├── Actualiza tasa dinámica
    └── Emite evento StakeIniciado
	
2. Stake por Relayer (Gasless)
text

Relayer → iniciarStakePorRelayer(...)

    ├── Verifica nonce único
    ├── Valida firma EIP-2612 (Permit)
    ├── Verifica firma personal del usuario
    ├── Ejecuta transferencia aprobada
    └── Crea stake para el usuario
	
3. Finalización de Stake
text

Usuario → finalizarMiStake(indice)

    ├── Calcula tiempo transcurrido
    ├── Determina intereses (si aplica)
    ├── Si tiempo ≥ mínimo: calcula intereses
    │   ├── Obtiene decimales de ambos tokens
    │   ├── Calcula con alta precisión (1e18)
    │   └── Ajusta por diferencia de decimales
    ├── Transfiere stake original de vuelta
    ├── Transfiere intereses (si hay balance)
    └── Actualiza tasa dinámica
	
🧮 Cálculo de Tasas Dinámicas

Fórmula de Cálculo
solidity
tasa = (balanceRecompensas * 100 * 1e18 * 10^decimalsStake) 
       / (totalStaked * 10^decimalsReward)
Características del Sistema
Tasa Variable: Se actualiza automáticamente con cada depósito/retiro

Histórico: Registra todos los cambios de tasa con timestamp

Precisión: Usa factor de 1e18 para cálculos internos

Límite: Máximo 100% (100 * 1e18)

Actualización de Tasa
Se ejecuta automáticamente cuando:

Usuario inicia un nuevo stake

Usuario finaliza un stake

Se depositan recompensas

Se retiran recompensas

🛡️ Mecanismos de Seguridad
1. Sistema Multifirma
Mínimo: 3 propietarios iniciales

Confirmaciones: Mayoría simple (n/2 + 1)

Ventana: Propuestas válidas por 24 horas

Transparencia: Todos los votos registrados on-chain

2. Prevención de Reentrancia
Modificador noReentrante en funciones críticas

Estados: _NO_ENTRADA (1) y _ENTRADA (2)

Protección contra llamadas recursivas

3. Validaciones
Nonces: Previene replay attacks en firmas

Firmas: Verificación ECDSA para operaciones gasless

Decimales: Manejo preciso de diferentes tokens ERC20

Límites: Cantidad mínima, tiempo mínimo

4. Control de Acceso
soloPropietario: Solo propietarios multifirma

Funciones separadas para usuarios vs administradores

📝 Funciones Especiales
Operaciones Gasless
Permit EIP-2612: Aprobación mediante firma

Firma Personal: Verificación ECDSA para acciones

Relayers: Terceros pueden pagar gas por usuarios

Gestión de Propietarios
Adición: Requiere propuesta y votación

Eliminación: No puede quedar menos de 3 propietarios

Lista Dinámica: Array actualizable de propietarios

Recuperación de Fondos
Propietarios: Pueden retirar tokens en emergencia (vía propuesta)

Stakes Bloqueados: Pueden ser finalizados por propietarios

Múltiples Destinos: Flexibilidad en envío de fondos

📊 Estadísticas y Consultas
Funciones de Visualización
solidity
// Para usuarios
obtenerStake(address, indice) → Devuelve detalles del stake
cantidadStakes(address) → Número de stakes activos
calcularIntereses(address, indice) → Intereses acumulados

// Para administración
propuestas(id) → Estado de propuestas
propietarios() → Lista de propietarios
historicoTasas() → Evolución de tasas
tasaActual() → Tasa actual del sistema
⚠️ Consideraciones Técnicas
1. Manejo de Decimales
Detecta automáticamente decimales de cada token

Ajusta cálculos para tokens con diferentes precisiones

Usa IERC20Metadata para compatibilidad

2. Límites de Tiempo
Stake mínimo: Configurable en constructor

Propuestas: 24 horas para votación/ejecución

Registro histórico: Timestamp en cada cambio

3. Gestión de Errores
Revertimientos claros: Mensajes específicos por fallo

Validaciones exhaustivas: Previene estados inválidos

SafeERC20: Manejo seguro de transferencias

4. Optimizaciones de Gas
Estructuras compactas: Uso de uint40 para timestamps

Mappings eficientes: Acceso O(1) a stakes

Eventos selectivos: Solo información relevante

🔗 Integración con Ecosistema Gainovo
Compatibilidad con Otros Contratos
Tokens ARG/GNT: Pueden usarse como token de stake/recompensa

Multifirma Consistente: Mismo sistema que otros contratos Gainovo

Keysafe: Compatible con recuperación de cuentas

Roles en el Ecosistema
Usuarios: Staking para obtener recompensas

Propietarios: Gestión y seguridad del contrato

Relayers: Facilitadores de operaciones gasless

✅ ERC-20: Compatibilidad total

✅ EIP-2612: Soporte para transacciones sin gas

✅ SafeERC20: Manejo seguro de tokens

✅ Checks-Effects-Interactions: Patrón seguido


Nota: Este contrato representa un sistema de staking avanzado con múltiples capas de seguridad y flexibilidad, diseñado específicamente para el ecosistema Gainovo con capacidad de evolución futura.

Nota: Todos los contratos están diseñados con el máximo estándar de seguridad y protección para los usuarios, respaldados por el sistema Gainovo Keysafe que garantiza la recuperación de fondos en caso de incidentes.
