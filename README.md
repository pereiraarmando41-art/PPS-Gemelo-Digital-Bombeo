# Gemelo Digital para Gestión Eficiente de Bombeo de Agua

**Práctica Profesional Supervisada (PPS) — Ingeniería en Computación (UNLP)**  
* **Alumno:** Armando Antonio Pereira (Legajo 02530/8)  
* **Lugar de Desarrollo:** Laboratorio LINTI, Facultad de Informática (UNLP)  
* **Tutor de Entidad:** Ing. Agustín Candia  
* **Profesora Coordinadora:** Lic. Laura Fava / Prof. Pablo Thomas  

---

## 📋 Descripción del Proyecto
Prototipo de **Gemelo Digital** dinámico implementado en Python para asistir al operador en la toma de decisiones del sistema de bombeo de agua en San Clemente del Tuyú. 

El simulador evalúa la disponibilidad de generación fotovoltaica en tiempo real y diferido (sistema FV de **55.35 kWp**, 90 módulos Trina 620 Wp), acoplado a la telemetría de 5 cisternas instrumentadas y al caudalímetro general de salida. Mediante el **Método de Euler**, proyecta el balance volumétrico para recomendar la cantidad óptima de bombas a encender sin riesgo de desborde ni faltante en la red.

---

## 🏗️ Arquitectura del Sistema
El modelo se divide en tres capas fundamentales:
1. **Entradas (Inputs):** Serie fotovoltaica horaria $P_{\text{solar}}(t)$ (vía `pvlib`/PVGIS), caudalímetro de salida $Q_{\text{salida}}(t)$ y volumen inicial $V_{\text{actual}}$.
2. **Procesamiento (Motor Python):** Asignación de bombeo solar directo ($N_{\text{bombas}} = \lfloor P_{\text{solar}} / 2.98\text{ kW} \rfloor$), caudal de ingreso y resolución del balance hídrico mediante Euler:
   $$V_{\text{cisterna}}(t+1) = V_{\text{cisterna}}(t) + [Q_{\text{ingreso}}(t) - Q_{\text{salida}}(t)] \cdot \Delta t$$
3. **Salidas (Outputs / Decision Support):** Recomendación directa de bombas a encender para el operador y proyección de tanques completos llenados al final del día.

---

## 🚀 Instalación y Uso

1. Clonar el repositorio:
   ```bash
   git clone [https://github.com/pereiraarmando41-art/PPS-Gemelo-Digital-Bombeo.git](https://github.com/pereiraarmando41-art/PPS-Gemelo-Digital-Bombeo.git)
   cd PPS-Gemelo-Digital-Bombeo
   ```

2. Crear entorno virtual e instalar dependencias:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # En Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Ejecutar la simulación básica:
   ```bash
   python src/main.py
   ```