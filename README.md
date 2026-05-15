# Pulse-Code-Modulation
# Aim
Write a simple Python program for the modulation and demodulation of PCM, and DM.
# Tools required
PYTHON IDE Numpy and Scipy
# Program
#PCM
```
import numpy as np
import matplotlib.pyplot as plt

# Parameters
fs = 5000        # Sampling frequency
fm = 50          # Message frequency
T = 0.1          # Time duration
L = 16           # Quantization levels

# Time axis
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2 * np.pi * fm * t)

# Quantization (PCM)
step = (m.max() - m.min()) / L
q = np.round(m / step) * step

# PCM encoding (digital levels)
pcm = ((q - q.min()) / step).astype(int)

# Plotting
plt.figure(figsize=(10, 9))

plt.suptitle(
    "NAME: M.NAGU SHENTHIL \nREG NO: 212224060164",
    fontsize=12,
    fontweight='bold'
)

# Message Signal
plt.subplot(4, 1, 1)
plt.plot(t, m)
plt.title("Message Signal (Analog)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Quantized Signal
plt.subplot(4, 1, 2)
plt.step(t, q, where='mid')
plt.title("Quantized Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# PCM Encoded Signal
plt.subplot(4, 1, 3)
plt.stem(t[:50], pcm[:50], basefmt=" ")
plt.title("PCM Encoded Signal (Digital Levels)")
plt.xlabel("Time (s)")
plt.ylabel("Level")
plt.grid(True)

# PCM Demodulated Signal
plt.subplot(4, 1, 4)
plt.plot(t, q, 'r--')
plt.title("PCM Demodulated Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Layout adjustment
plt.tight_layout(rect=[0, 0, 1, 0.93])

# Show plot
plt.show()```

Attach the program
```
#DELTA MODULATION
```
# Delta Modulation

import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

# Parameters
fs = 10000      # Sampling frequency
fm = 10         # Message frequency
T = 1           # Time duration
delta = 0.1     # Step size

# Time axis
t = np.arange(0, T, 1/fs)

# Message signal
m = np.sin(2 * np.pi * fm * t)

# Delta Modulation (Encoder)
dm = np.zeros_like(m)
bits = np.zeros_like(m)

for i in range(1, len(m)):
    if m[i] > dm[i - 1]:
        bits[i] = 1
        dm[i] = dm[i - 1] + delta
    else:
        bits[i] = 0
        dm[i] = dm[i - 1] - delta

# Delta Demodulation

rec = np.cumsum((2 * bits - 1) * delta)

# Low-pass filter
b, a = butter(4, 20 / (0.5 * fs), btype='low')
rec_filt = filtfilt(b, a, rec)

# Plotting
plt.figure(figsize=(10, 8))

plt.suptitle(
    "NAME: M.NAGU SHENTHIL \nREG NO: 212224060164",
    fontsize=12,
    fontweight='bold'
)

# Original Signal
plt.subplot(3, 1, 1)
plt.plot(t, m)
plt.title("Original Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Delta Modulated Signal
plt.subplot(3, 1, 2)
plt.step(t, dm, where='mid')
plt.title("Delta Modulated Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Demodulated Signal
plt.subplot(3, 1, 3)
plt.plot(t, rec_filt, 'r--')
plt.title("Demodulated Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Adjust layout
plt.tight_layout(rect=[0, 0, 1, 0.93])

# Show plot
plt.show()
```
# Output Waveform

PCM
<img width="1040" height="876" alt="image" src="https://github.com/user-attachments/assets/93436e59-3008-4b34-aaae-97cf83908ce6" />
DELTA MODULATION
<img width="1046" height="766" alt="image" src="https://github.com/user-attachments/assets/b63c8ba5-93c0-4d65-91d6-043d42a95bf9" />

# Results
The analog signal was successfully encoded and reconstructed using PCM and DM techniques in Python, verifying their working principles.

