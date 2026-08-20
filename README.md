**INTELLIGENT WIRELESS SENSOR DATA COMMUNICATION SYSTEM**

**PROJECT OVERVIEW**
- An experimental activity project that demonstrates sensor-data transmission through a simulated digital communication system using ESP32 and Wokwi.
- The project combines digital modulation, channel estimation, error detection, performance measurement, and lightweight machine learning into a single communication-processing chain.

**COMMUNICATION PROCESSING CHAIN**
*Sensor Data*
    ↓
*Packet Formation*
    ↓
*CRC*
    ↓
*ML-Based Modulation Selection*
    ↓
*BPSK / QPSK*
    ↓
*Pilot Insertion*
    ↓
*Simulated Wireless Channel*
    ↓
*AWGN Noise*
    ↓
*Channel Estimation*
    ↓
*Equalization*
    ↓
*Demodulation*
    ↓
*BER Calculation*
    ↓
*CRC Verification*
    ↓
*Recovered Data*

**MAIN FEATURES**
• ESP32-based simulation
• DS18B20 temperature sensing
• Adjustable simulated channel/SNR using a potentiometer
• BPSK modulation
• QPSK modulation
• KNN-based modulation selection
• Pilot-symbol insertion
• Simulated complex wireless channel
• AWGN noise model
• Pilot-assisted channel estimation
• Channel equalization
• BER calculation
• CRC-based error detection
• Sequence-number tracking
• OLED transmitter and receiver displays
• TX/RX LED indicators
• Performance logging
• Experiment logging

**OPERATING MODES**
*ML AUTO:* The KNN model selects either BPSK or QPSK based on communication-channel features.
*BPSK:* BPSK is selected manually for testing and comparison.
*QPSK:* QPSK is selected manually for testing and comparison.

**HARDWARE USED: SIMULATIONS**
• ESP32
• DS18B20 temperature sensor
• Potentiometer
• 2 × OLED displays
• 2 × Push buttons
• 2 × LEDs
• Resistors
• wires

**SOFTWARE USED**
• Wokwi
• MicroPython
• Python-based communication-processing logic

**PROJECT FILES**
main.py
ml_model.py
security.py
performance.py
experiment.py
diagram.json
README.txt

**COMMUNICATION MODEL**
The simulated wireless channel follows the simplified model:
y = h × x + n
where:
x = transmitted symbol
h = simulated channel coefficient
n = AWGN noise
y = received symbol

**CHANNEL EQUALIZATION**
Channel equalization is performed using:
x̂ = y / ĥ
where:
x̂ = estimated transmitted symbol
y = received symbol
ĥ = estimated channel coefficient
The channel coefficient is estimated using pilot symbols transmitted along with the data.

**BER CALCULATION:**
Bit Error Rate is calculated using:
BER = Number of Bit Errors / Total Number of Transmitted Bits
BER is used to evaluate the quality of the simulated communication link.

**MACHINE LEARNING:**
A lightweight K-Nearest Neighbor (KNN) classifier is implemented without external machine-learning libraries.
The model uses:
• SNR
• Channel amplitude
• Estimated BER
The output classes are:
• BPSK
• QPSK
The current training data is experimental/prototype data intended to demonstrate the adaptive-modulation concept.

**ERROR DETECTION:**
CRC is appended to the transmitted payload before modulation.
At the receiver:
1. Received bits are reconstructed.
2. The CRC is checked.
3. The system reports whether the received frame is valid or invalid.
This provides a basic method of detecting errors introduced during the simulated transmission process.

**USER INTERFACE:**
The transmitter OLED displays information such as:
• Temperature
• SNR
• Selected modulation
• Sequence number
• CRC

**The receiver OLED displays:**
• Received temperature
• Modulation
• BER
• CRC status
• Sequence number

**BUTTON OPERATION**
- The Send button starts one complete transmission.
- The Mode button cycles through:
- ML AUTO → BPSK → QPSK → ML AUTO

**TRANSMISSION PROCESS**

When the Send button is pressed, the system performs the following operations:
1. Reads the temperature sensor.
2. Reads the potentiometer value.
3. Converts the potentiometer value into a simulated SNR condition.
4. Determines the channel amplitude.
5. Provides the channel features to the ML classifier.
6. Selects BPSK or QPSK in ML AUTO mode.
7. Creates the sensor-data payload.
8. Adds CRC information.
9. Converts the frame into bits.
10. Generates pilot symbols.
11. Modulates the data.
12. Passes the symbols through the simulated wireless channel.
13. Adds AWGN noise.
14. Separates the received pilot symbols.
15. Estimates the channel coefficient.
16. Equalizes the received data.
17. Demodulates the received symbols.
18. Calculates BER.
19. Reconstructs the received frame.
20. Performs CRC verification.
21. Displays the receiver results.
22. Records the experiment and performance information.

**SIMULATED WIRELESS CHANNEL**
- The project does not use an actual RF wireless transmission link.
- Instead, the wireless communication path is mathematically simulated inside the ESP32/Wokwi environment.

- The simulated channel includes:
• Channel amplitude variation
• Channel phase variation
• SNR variation
• AWGN noise

**PILOT SYMBOLS**
- Pilot symbols are known symbols transmitted before the data symbols.
- The receiver already knows what the pilot symbols should be.
- By comparing the transmitted pilots with the received pilots, the receiver estimates the channel coefficient.
- This estimated coefficient is then used for equalization.

- *WHY BPSK IS USED:* BPSK is a robust digital modulation technique. It uses one bit per symbol and generally provides better noise tolerance than higher-order modulation under difficult channel conditions. BPSK is also available as a manually selected mode for comparison.

- *WHY QPSK IS USED:* QPSK transmits two bits per symbol and can provide higher spectral efficiency than BPSK. It is included as another modulation option in the adaptive communication system.

**ROLE OF MACHINE LEARNING**
- The ML component provides an experimental adaptive-modulation mechanism.
- Instead of always using one fixed modulation technique, the system examines communication-related features and makes a modulation decision.
- The KNN classifier currently contains experimental training samples representing different communication conditions.

**CURRENT STATUS**
- Functional experimental prototype — under further development.
- The current implementation demonstrates the intended communication-processing chain and provides a foundation for additional experiments and improvements.

**LIMITATIONS**
• The wireless channel is simulated rather than physically transmitted.
• The ML training dataset is limited.
• The ML model is intended for demonstration rather than production deployment.
• The channel model is simplified.
• The system has not been validated against a physical RF communication link.
• Extensive statistical testing has not yet been performed.
• The current implementation is not intended to represent a commercial communication system.

**FUTURE IMPROVEMENTS**
• Larger and more representative ML datasets
• Proper training and testing dataset separation
• BER versus SNR experiments
• More realistic fading-channel models
• Rayleigh and Rician fading simulation
• Additional modulation schemes
• Improved channel estimation
• More advanced equalization techniques
• Statistical performance analysis
• Comparison of multiple ML algorithms
• Real wireless hardware validation
• SDR-based implementation
• Automated performance graphs

*EXPERIMENTAL NATURE: This project is an experimental activity project developed to understand and demonstrate communication-system concepts through simulation.
The current implementation should be considered a prototype rather than a finalized or fully validated communication system.
Further testing, validation, optimization, and research are required before making real-world performance claims.*

Intelligent Wireless Sensor Data Communication System is an experimental ESP32/Wokwi project that demonstrates sensor-data communication using BPSK and QPSK modulation, KNN-based adaptive modulation selection, pilot-assisted channel estimation, simulated wireless-channel effects, AWGN noise, equalization, BER measurement, and CRC-based error detection.
The project is currently a functional experimental prototype and can be further extended through improved datasets, realistic channel models, additional modulation schemes, statistical analysis, and physical wireless validation.
