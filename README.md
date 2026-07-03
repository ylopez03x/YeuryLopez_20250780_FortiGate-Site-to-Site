# FortiGate VPN Site-to-Site
**Autor:** Yeury Lopez | **Matrícula:** 20250780 | **Repositorio:** YeuryLopez_20250780_FortiGate-Site-to-Site

---

## 1. Objetivo
Configurar una VPN Site-to-Site entre dos firewalls FortiGate, permitiendo la comunicación cifrada entre dos redes LAN remotas. La configuración se realiza mediante el IPSec Wizard de la GUI web de FortiGate, demostrando las ventajas de una solución UTM comercial.

---

## 2. Topología

```
[Linux1] --- [FortiGate1] --- [ISP] --- [FortiGate2] --- [Linux2]
```

> 📸 **SCREENSHOT:** Insertar captura de la topología completa en EVE-NG

---

## 3. Direccionamiento IP

| Dispositivo | Interfaz | Dirección IP | Rol |
|---|---|---|---|
| FortiGate1 | port2 | 10.7.80.1/30 | WAN → ISP |
| FortiGate1 | port1 | 192.168.7.1/24 | LAN |
| ISP | Fa0/0 | 10.7.80.2/30 | WAN → FGT1 |
| ISP | Fa1/0 | 10.7.81.1/30 | WAN → FGT2 |
| FortiGate2 | port1 | 10.7.81.2/30 | WAN → ISP |
| FortiGate2 | port2 | 192.168.80.1/24 | LAN |
| Linux1 | ens3 | 192.168.7.2/24 | Host LAN FGT1 |
| Linux2 | ens3 | 192.168.80.2/24 | Host LAN FGT2 |

---

## 4. Parámetros VPN

| Parámetro | Valor |
|---|---|
| Tipo de VPN | IPSec Site-to-Site |
| Dispositivos | FortiGate 7.0.13 (ambos peers) |
| Template Wizard | Site to Site — FortiGate |
| Fase 1 — Cifrado | AES-128 |
| Fase 1 — Hash | SHA-256 |
| Autenticación | Pre-Shared Key |
| Grupo DH | Group 14 (2048-bit) |
| Pre-Shared Key | Yeury0780 |
| Herramienta de config | FortiGate GUI — IPSec Wizard |

---

## 5. Configuración

### 5.1 Interfaces FortiGate1

> 📸 **SCREENSHOT:** Insertar captura de `Network → Interfaces` en FortiGate1 mostrando port1 (LAN 192.168.7.1) y port2 (WAN 10.7.80.1)

### 5.2 VPN Wizard — Step 1 VPN Setup

> 📸 **SCREENSHOT:** Insertar captura del Wizard mostrando Site to Site, No NAT between sites y FortiGate seleccionado

### 5.3 VPN Wizard — Step 2 Authentication

> 📸 **SCREENSHOT:** Insertar captura mostrando Remote IP 10.7.81.2, Outgoing Interface port2 y Pre-shared key Yeury0780

### 5.4 VPN Wizard — Step 3 Policy & Routing

> 📸 **SCREENSHOT:** Insertar captura mostrando Local interface port1, Local subnets 192.168.7.0/24 y Remote Subnets 192.168.80.0/24

### 5.5 VPN Wizard — Review Settings FortiGate1

> 📸 **SCREENSHOT:** Insertar captura mostrando **"The VPN has been set up"** con todos los objetos creados

### 5.6 VPN Wizard — FortiGate2

> 📸 **SCREENSHOT:** Insertar captura del Wizard en FortiGate2 con la configuración espejo apuntando hacia 10.7.80.1

---

## 6. Verificación y Funcionamiento

### 6.1 Estado del Túnel en FortiGate1

Ir a: `VPN → IPSec Tunnels`
> 📸 **SCREENSHOT:** Insertar captura mostrando el túnel **VPN-FGT1-FGT2** activo en verde

### 6.2 Políticas de Firewall

Ir a: `Policy & Objects → Firewall Policy`
> 📸 **SCREENSHOT:** Insertar captura mostrando las políticas `vpn_VPN-FGT1-FGT2_local` y `vpn_VPN-FGT1-FGT2_remote` activas con acción ACCEPT

### 6.3 Demostración de conectividad — Ping

Ejecutar en Linux1:
```
ping -c 4 192.168.80.2
```
> 📸 **SCREENSHOT:** Insertar captura del ping exitoso desde Linux1 hacia Linux2

### 6.4 Demostración de conectividad — Traceroute

Ejecutar en Linux1:
```
traceroute 192.168.80.2
```
> 📸 **SCREENSHOT:** Insertar captura del traceroute mostrando: Linux1 → FortiGate1 → FortiGate2 → Linux2

---

## 7. Archivos del repositorio

| Archivo | Descripción |
|---|---|
| `YeuryLopez_20250780_Script_P10.txt` | Script del video |
| `YeuryLopez_20250780_Informe_P10.pdf` | Documentación técnica en PDF |
| `YeuryLopez_20250780_Links_P10.txt` | Enlace al video |
| `README.md` | Este archivo |
