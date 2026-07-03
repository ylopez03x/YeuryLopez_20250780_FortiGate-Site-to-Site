# FortiGate VPN Site-to-Site
**Autor:** Yeury Lopez | **Matrícula:** 20250780 | **Repositorio:** YeuryLopez_20250780_FortiGate-Site-to-Site

## Video de demostración

[![Ver en YouTube](https://img.shields.io/badge/YouTube-Ver%20Video-red?logo=youtube)](https://youtu.be/0Y3RkZxta1k)

**Enlace directo:** https://youtu.be/0Y3RkZxta1k

---

## 1. Objetivo
Configurar una VPN Site-to-Site entre dos firewalls FortiGate, permitiendo la comunicación cifrada entre dos redes LAN remotas. La configuración se realiza mediante el IPSec Wizard de la GUI web de FortiGate, demostrando las ventajas de una solución UTM comercial.

---

## 2. Topología


> <img width="730" height="730" alt="image" src="https://github.com/user-attachments/assets/f1ff6336-7cc2-4c9d-b3c2-202dab1abefb" />


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

> <img width="1817" height="784" alt="image" src="https://github.com/user-attachments/assets/99418a2d-51c2-4ffc-bcbc-d8cc5733c5ca" />


### 5.2 VPN Wizard — Step 1 VPN Setup

> <img width="1417" height="460" alt="image" src="https://github.com/user-attachments/assets/c4d2acfa-ddd7-4615-9ad9-47933039c02f" />


### 5.3 VPN Wizard — Step 2 Authentication

> <img width="889" height="272" alt="image" src="https://github.com/user-attachments/assets/264814f2-f3de-45e0-8275-b045870ef2fe" />



### 5.4 VPN Wizard — Step 3 Policy & Routing

> <img width="1816" height="408" alt="image" src="https://github.com/user-attachments/assets/a3825fc2-0d75-41e0-b438-9609ba64e6d5" />


---

## 6. Verificación y Funcionamiento


### 6.3 Demostración de conectividad — Ping and traceroute

Ejecutar en Linux1:
```
ping -c 4 192.168.80.2
```
> <img width="888" height="287" alt="image" src="https://github.com/user-attachments/assets/c40d5a29-f335-45d2-b7d3-be76999bd25d" />


