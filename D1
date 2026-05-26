import numpy as np
import matplotlib.pyplot as plt
from scipy.interpolate import CubicSpline
from scipy.optimize import brentq

f = np.array([
    100, 120, 145, 170, 200,
    235, 270, 310, 355, 405,
    460, 520, 585, 655, 730,
    810, 895, 985, 1080, 1180,
    1290, 1410, 1540, 1680, 1830,
    1990, 2160, 2340, 2530, 2730
])

Z = np.array([
    152.3, 149.1, 146.8, 144.9, 142.0,
    139.5, 137.9, 136.1, 134.8, 133.6,
    132.7, 131.9, 131.4, 131.1, 130.9,
    131.0, 131.3, 131.9, 132.7, 133.8,
    135.2, 136.9, 138.9, 141.1, 143.5,
    146.1, 149.0, 152.2, 155.6, 159.2
])

# umbral
Z_th = 150

# spline cubico natural
spline = CubicSpline(f, Z, bc_type='natural')

# fun para las raices
def funcion(x):
    return spline(x) - Z_th

# lista
raices = []

# intervalos
for i in range(len(f)-1):

    # cambio de signo 
    if funcion(f[i]) * funcion(f[i+1]) < 0:

        # raiz con Brentq
        raiz = brentq(funcion, f[i], f[i+1])

        raices.append(raiz)

# grafica

f_suave = np.linspace(min(f), max(f), 2000)

plt.figure(figsize=(10,6))

# spline
plt.plot(
    f_suave,
    spline(f_suave),
    linewidth=2,
    label='Spline cúbico'
)

# linea umbral
plt.axhline(
    Z_th,
    linestyle='--',
    label='Z_th = 150 Ω'
)

# raices puntos
for r in raices:
    plt.scatter(r, Z_th, s=120)

plt.xlabel('Frecuencia (Hz)')
plt.ylabel('|Z| (Ohm)')

plt.title('Raíces de |Z|(f) - Z_th')

plt.grid(True)

plt.legend()

plt.show()

# resultados

print("Raíces encontradas:\n")

for i, r in enumerate(raices):
    print(f"Raíz {i+1}: f = {r:.4f} Hz")
