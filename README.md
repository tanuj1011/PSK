# PSK
# Aim
Write a simple Python program for the modulation and demodulation of PSK and QPSK.
# Tools required
COLAB
# Program
```
1.PSK
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter
fs, fc, br, T = 1000, 50, 10, 1
t = np.linspace(0, T, fs*T, endpoint=False)
bits = np.random.randint(0,2,br)
spb = fs//br
msg = np.repeat(bits, spb)
carrier = np.sin(2*np.pi*fc*t)
psk = np.sin(2*np.pi*fc*t + np.pi*msg)
b,a = butter(5, fc/(0.5*fs), 'low')
demod = lfilter(b,a,psk*carrier)
dec = (demod[::spb] < 0).astype(int)
plt.figure(figsize=(9,7))
plt.subplot(411); plt.plot(t,msg); plt.title("Message"); plt.grid()
plt.subplot(412); plt.plot(t,carrier); plt.title("Carrier"); plt.grid()
plt.subplot(413); plt.plot(t,psk); plt.title("PSK"); plt.grid()
plt.subplot(414); plt.step(range(len(dec)),dec); plt.title("Decoded"); plt.grid()
plt.tight_layout(); plt.show()

2.QPSK

import numpy as np
import matplotlib.pyplot as plt
x = ['10','11','11','10']
t = np.arange(-np.pi, np.pi, 0.1)
phase = {'00':np.pi/4,'01':3*np.pi/4,
         '10':5*np.pi/4,'11':7*np.pi/4}
mod = np.concatenate([np.sin(t+phase[b]) for b in x])
inp = np.array([int(i) for b in x for i in b])
demod = inp.copy()   # since no noise
plt.figure(figsize=(8,6))
plt.subplot(311); plt.step(range(len(inp)),inp); plt.title("Input"); plt.grid()
plt.subplot(312); plt.plot(mod); plt.title("QPSK"); plt.grid()
plt.subplot(313); plt.step(range(len(demod)),demod); plt.title("Demod"); plt.grid()
plt.tight_layout(); plt.show()

```
# Output Waveform

1.PSK

<img width="842" height="659" alt="image" src="https://github.com/user-attachments/assets/75b52a23-e921-419b-a31e-8379798743e7" />

2.QPSK

<img width="767" height="555" alt="image" src="https://github.com/user-attachments/assets/08a676c3-3132-4040-988e-3d9c178ce4a8" />

# Results

Thus the simple Python program for the modulation and demodulation of PSK and QPSK is done and verified.

