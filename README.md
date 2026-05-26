# ☀️ Dual-Axis Solar Tracker with Arduino UNO

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Arduino UNO](https://img.shields.io/badge/Arduino-UNO-green.svg)](https://www.arduino.cc/)

---

## 📌 Overview
This project presents the design and implementation of a **dual-axis solar tracker** based on an **Arduino UNO**, **four LDR sensors**, and **two servomotors**. The system automatically orients a photovoltaic panel toward the sun to maximize energy harvesting efficiency.

---

## 🎯 Project Information

| | |
|---|---|
| **Author** | Malak BOULAKSA |
| **Institution** | Badji Mokhtar - Annaba University, Algeria |
| **Faculty** | Technology |
| **Department** | Electronics |
| **Specialty** | Electronics |
| **Supervisor** | Prof. REDJATI Abdelghani |
| **Academic Year** | 2024/2025 |

---

## ⚙️ Working Principle
1. **Four LDRs** are placed at the four corners of the solar panel: top-left, top-right, bottom-left, bottom-right.
2. The Arduino **computes averages** to detect the sun's direction.
3. If a difference is detected, the Arduino moves the corresponding servomotor step-by-step toward the brighter side to maximize solar exposure.

---

## 📜 License
This project is open-source under the **MIT License**.  
Copyright (c) 2026 Malak BOULAKSA
