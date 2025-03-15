# Explicación dos Scripts e Compoñentes de Netcode en Unity

## 1. Explicación dos Scripts

### HelloWorldManager.cs
Este script xestiona a conexión de rede e mostra unha interface gráfica para iniciar o servidor, cliente ou host.

#### **Variables:**
- `m_NetworkManager`: Referencia ao `NetworkManager`, que manexa as conexións de rede.

#### **Métodos:**
- `Awake()`: Obtén a referencia ao `NetworkManager`.
- `OnGUI()`: Mostra botóns de interface gráfica. Se o xogador non está conectado, amosa botóns para iniciar a conexión.
- `StartButtons()`: Botóns para iniciar Host, Cliente ou Servidor.
- `StatusLabels()`: Mostra o modo de rede no que está o xogo (`Host`, `Server`, `Client`).
- `SubmitNewPosition()`: Se o servidor está activo, move todos os xogadores conectados. Se é cliente, solicita o cambio de posición.

---

### HelloWorldPlayer.cs
Este script xestiona o movemento dos xogadores en rede.

#### **Variables:**
- `NetworkVariable<Vector3> Position`: Variable de rede que almacena a posición do xogador.

#### **Métodos:**
- `Move()`: Método que cambia a posición do xogador de maneira aleatoria.
- `MoveServerRpc()`: Método RPC que se executa no servidor para actualizar a posición.
- `OnNetworkSpawn()`: Chámase cando o obxecto se activa na rede e sincroniza a súa posición.
- `Update()`: Se o obxecto pertence ao servidor, actualiza a posición na variable de rede.

---

### NetworkTransformTest.cs
Este script proba o sistema de sincronización de movemento en rede usando `NetworkTransform`.

#### **Variables:**
- `NetworkTransform networkTransform`: Referencia ao compoñente `NetworkTransform`.

#### **Métodos:**
- `Start()`: Obtén a referencia ao `NetworkTransform`.
- `Update()`: Se o obxecto pertence ao xogador local, actualiza a súa posición.

---

### RPCTest.cs
Este script demostra o uso de chamadas RPC para a comunicación entre cliente e servidor.

#### **Métodos:**
- `TestClientRpc()`: Método RPC que se executa en todos os clientes cando é chamado polo servidor.
- `TestServerRpc()`: Método RPC que se executa no servidor cando é chamado por un cliente.

---

## 2. Explicación dos Compoñentes do `NetworkManager`
O `NetworkManager` é o compoñente central de Netcode e xestiona toda a lóxica de rede.

### **Network Manager**
- Controla as conexións entre cliente e servidor.
- Xestiona a creación e destrución de xogadores na rede.
- Permite configurar o modo de rede (`Host`, `Server`, `Client`).

### **Unity Transport**
- É o sistema de transporte de rede que usa Netcode.
- Encárgase de enviar e recibir datos entre os dispositivos conectados.

### **Hello World Manager**
- É o script `HelloWorldManager.cs`, que xestiona a interface gráfica e as conexións.

---

## 3. Explicación dos Compoñentes do Prefab `Player`

### **Network Object**
- Permite que o obxecto sexa sincronizado na rede.
- Fai que o obxecto teña unha ID única para ser identificado nos clientes e no servidor.

### **Hello World Player**
- É o script `HelloWorldPlayer.cs`, que xestiona o movemento do xogador na rede.

### **Rpc Test**
- É o script `RPCTest.cs`, que permite executar funcións remotas con RPCs.

### **Network Transform**
- Sincroniza a posición, rotación e escala do obxecto na rede.

---

