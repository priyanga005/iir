import numpy as np
import scipy.signal as signal
import matplotlib.pyplot as plt

# Filter specifications
f_c = 1000  # Cutoff frequency in Hz
f_s = 5000  # Sampling frequency in Hz
n = 4       # Filter order

# Normalize the cutoff frequency by the Nyquist frequency
nyquist = 0.5 * f_s
normalized_cutoff = f_c / nyquist

# Design the Butterworth low pass filter
b, a = signal.butter(n, normalized_cutoff, btype='low')

# Create a sample signal (e.g., a noisy sinusoidal signal)
t = np.linspace(0, 1.0, f_s)  # 1 second of data at f_s sampling rate
signal_input = np.sin(2 * np.pi * 500 * t) + 0.5 * np.random.randn(len(t))  # 500 Hz sine wave with noise

# Apply the filter to the signal
signal_output = signal.lfilter(b, a, signal_input)

# Plot the input and output signals
plt.figure(figsize=(10, 6))

plt.subplot(2, 1, 1)
plt.plot(t, signal_input)
plt.title('Input Signal (Noisy)')
plt.xlabel('Time [s]')
plt.ylabel('Amplitude')

plt.subplot(2, 1, 2)
plt.plot(t, signal_output)
plt.title('Filtered Signal (Butterworth LPF
