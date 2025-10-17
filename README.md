# Performance-Analysis-of-Mach-Zehnder-Modulator-for-High-Speed-Optical-Communication-Systems
Designed and simulated a Mach–Zehnder Modulator (MZM) in MATLAB/Simulink for optical communication, analyzing modulation techniques to enhance signal integrity, bandwidth, and noise tolerance, while exploring applications in fiber-optics and gaining expertise in system-level simulation.

## 🎯 Strategy  
1. **Modeling**: Develop a Mach–Zehnder Modulator (MZM) in **MATLAB/Simulink**.  
2. **Simulation**: Apply different **modulation techniques** (OOK, DPSK, QPSK, etc.).  
3. **Performance Evaluation**: Analyze  
   - Signal Integrity  
   - Bandwidth Utilization  
   - Noise Tolerance  
   - Bit Error Rate (BER)  
4. **Optimization**: Compare and choose modulation schemes suited for **high-speed fiber-optic communication**.  

---

## ✅ Solution  
- Designed and simulated a **Mach–Zehnder Modulator (MZM)** in MATLAB/Simulink.  
- Demonstrated that **external modulation using MZM** improves:  
  - ✔️ **Signal quality** over long distances  
  - ✔️ **High bandwidth efficiency**  
  - ✔️ **Noise immunity** compared to direct modulation  
- Generated **BER vs SNR plots**, **Eye Diagrams**, and **spectrum analysis** to validate results.  

---

## 🌍 Real-World Applications  
- Long-haul and metro **fiber-optic communication** systems  
- **High-speed data center** interconnections  
- **5G/6G optical backhaul** networks  
- **Military and aerospace** secure communication  

---

## 📊 Key Learning Outcomes  
- Hands-on **system-level simulation** in MATLAB/Simulink  
- Comparative study of **different optical modulation formats**  
- Practical insights into **design challenges of photonic communication systems**  
- Understanding of **trade-offs between BER, bandwidth, and SNR**

- Matlab with Simulink code:-
- % Clear workspace and command window
clear all;

% Define sampling time (ts)
ts = 1/20e4;     % Sampling period = 1 / (sampling frequency)
                 % Change ts for faster or slower operation

% Open the Simulink model
open_system('MZM_FM_ROF_1');

% Run the Simulink simulation
sim MZM_FM_ROF_1;

% Extract time and output data from simulation
x = [time];      % Time vector
y = [out];       % Output signal from Simulink

% Get the length of the output signal
L = length(y);

% Define the sampling rate
Fs = 1 / ts;     % Sampling frequency

% Perform FFT (Fast Fourier Transform)
Y = fft(y, L);                 % Compute FFT of signal
Ymag = abs(Y(1:L/2));          % Magnitude of first half
Xf = Fs * (0:(L/2)-1) / L;     % Frequency vector

% Convert magnitude to dB scale
YdB = 20 * log10(Ymag / max(Ymag));

% Plot frequency spectrum
plot(Xf, YdB, 'LineWidth', 1.4);
grid on;

% Add title and labels
title('MZM Output Spectrum');
xlabel('Frequency (Hz)');
ylabel('Amplitude (dB)');

% Set axis range
axis([0 8e9 -150 0]);   % Frequency range up to 8 GHz, amplitude -150 to 0 dB

