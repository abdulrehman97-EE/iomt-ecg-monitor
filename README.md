# Real-Time IoMT ECG Monitoring System

**Course Project:** Embedded Systems Design (End-of-Semester Project)

## Project Overview
This project implements a **real-time biomedical monitoring system** that captures, transmits, and processes Electrocardiogram (ECG) signals using IoT protocols.

Developed as the final project for the **Embedded Systems Design** course, this system streams raw ECG data from an ESP8266 (NodeMCU) to a Raspberry Pi 4B via **MQTT**. The Raspberry Pi acts as an edge processing unit, applying **Maximal Overlap Discrete Wavelet Transforms (MODWT)** to filter noise and calculate heart rate in real-time.

**Key Capabilities:**
* **Real-Time Visualization:** Live plotting of ECG waveforms using Matplotlib.
* **Signal Processing:** Implementation of `sym4` wavelet decomposition for R-peak detection.
* **IoT Architecture:** Low-latency messaging using the MQTT protocol.

## System Architecture
The system consists of three stages:
1.  **Acquisition:** AD8232 sensor + ESP8266 (at 3.3V) digitize the analog signal.
2.  **Transmission:** Data is published to the `ECG/data` topic over WiFi.
3.  **Processing (Edge):** The Raspberry Pi subscribes to the topic, buffers the data, and applies the R-peak detection algorithm.

![System Block Diagram](images/diagram.png)

## Signal Processing & Math
To ensure accurate heart rate calculation, we implemented a custom filtering pipeline:
* **Wavelet Transform:** We utilized the MODWT with a `sym4` mother wavelet.
* **Feature Extraction:** By reconstructing the signal using only the $2^{nd}$ and $3^{rd}$ wavelet coefficients, we effectively attenuated the P and T waves while enhancing the QRS complex.
* **Peak Detection:** Adaptive thresholding ($5 \times \mu_{amp}$) is used to identify R-peaks dynamically.

<p align="center">
  <img src="images/ecg_sig.png" width="700"/>
  <br/>
  <i>Figure: 10-second segment of the filtered ECG signal showing detected R-peaks (orange markers).</i>
</p>

## Libraries
* **Language:** Python 3.x
* **Protocols:** MQTT (Paho-MQTT), TCP/IP
* **Libraries:**
    * `NumPy` & `SciPy`: Numerical processing and peak finding.
    * `PyWavelets`: Wavelet transform support.
    * `Matplotlib`: Live data visualization.

## Contributors
* **Abdul Rehman** 
* **Zain Amir**
* **Sardar Hassan Arfan Khan**

