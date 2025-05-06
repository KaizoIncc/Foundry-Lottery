# 🎲 Foundry Lottery

Este proyecto implementa una **lotería descentralizada** utilizando [Foundry](https://book.getfoundry.sh/), con integración de **Chainlink VRF v2** para aleatoriedad segura y **Chainlink Automation (Keepers)** para ejecutar automáticamente la selección del ganador.

## 📌 Características

- Los usuarios pueden unirse a la lotería pagando una cantidad mínima de ETH.
- Chainlink VRF selecciona un ganador de manera justa y verificable.
- Chainlink Automation verifica regularmente si las condiciones están listas para seleccionar un ganador.
- Solo el contrato gestiona la lógica, completamente descentralizado.

---

## 📁 Estructura del Proyecto

```text
Foundry-Lottery/
│
├── script/              # Scripts de despliegue
├── src/                 # Contratos principales (Lottery.sol)
├── test/                # Pruebas en Solidity
├── lib/                 # Dependencias externas (Chainlink)
├── foundry.toml         # Configuración del proyecto Foundry
└── .env                 # Variables de entorno (clave privada, RPC, etc.)
```

---

## 🔧 Requisitos

- [Foundry](https://book.getfoundry.sh/getting-started/installation)
- [Node.js](https://nodejs.org/) (para herramientas como dotenv si se usa)
- RPC URL (por ejemplo, de Alchemy o Infura)
- Clave privada con fondos en Sepolia u otra testnet

Instala las dependencias de Foundry:

```bash
forge install
```

---

## 🚀 Uso

### 🔨 Compilar

```bash
forge build
```

### ✅ Probar

```bash
forge test -vv
```

### 🧪 Tomar una instantánea de gas

```bash
forge snapshot
```

### 🛠️ Desplegar (en testnet)

```bash
forge script script/DeployLottery.s.sol:DeployLottery --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast --verify
```

> Asegúrate de tener configuradas tus variables de entorno en un archivo `.env` o como variables del sistema:

```env
SEPOLIA_RPC_URL=https://sepolia.infura.io/v3/tu-api-key
PRIVATE_KEY=tu_clave_privada
ETHERSCAN_API_KEY=tu_api_key
```

---

## 🔄 Automatización con Chainlink

Para usar Chainlink Keepers (Automation), registra tu contrato desplegado en [https://automation.chain.link](https://automation.chain.link) usando:

- El `checkUpkeep()` para verificar si se cumplen las condiciones (ej. tiempo transcurrido y participantes).
- El `performUpkeep()` para iniciar la solicitud de aleatoriedad.

## 🎰 Aleatoriedad con Chainlink VRF

Este proyecto utiliza Chainlink VRF v2. Asegúrate de:

- Tener suficiente LINK en tu contrato (usa [faucets de testnet](https://faucets.chain.link/)).
- Configurar correctamente `subscriptionId` y registrar el contrato como consumidor.

---

## 📜 Licencia

Este proyecto está bajo la licencia MIT. Consulta el archivo [`LICENSE`](LICENSE) para más detalles.

---

## 🙏 Agradecimientos

Inspirado en el curso de [Patrick Collins - Solidity, Chainlink & Foundry](https://github.com/Cyfrin/foundry-smartcontract-lottery-f23) y adaptado como proyecto personal de aprendizaje.
