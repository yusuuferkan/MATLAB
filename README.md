<div align="center">

# 🌡️ Blackbody Radiation in MATLAB

**Planck's law, Wien's displacement law and Stefan–Boltzmann: plotting, band integration and radiance look-up tables.**

![MATLAB](https://img.shields.io/badge/MATLAB-0076A8?logo=mathworks&logoColor=white)
![Physics](https://img.shields.io/badge/topic-thermal%20radiation-orange)
![Use case](https://img.shields.io/badge/use%20case-IR%20sensing-red)

</div>

---

## 📐 The physics

**Planck's law** gives the spectral radiance of a blackbody at temperature *T*:

$$
B_\lambda(\lambda, T) = \frac{2hc^2}{\lambda^5}\,\frac{1}{e^{hc/(\lambda k T)} - 1}
$$

- **Wien's displacement law:** the peak wavelength shifts as $\lambda_{max} = b / T$, with $b \approx 2898\ \mu m \cdot K$
- **Stefan–Boltzmann law:** total emitted power grows as $M = \varepsilon \sigma T^4$

## 🧰 Scripts

All scripts are in [`Planck function, wien and stefan boltzman/`](Planck%20function,%20wien%20and%20stefan%20boltzman):

| Script | What it does |
|---|---|
| `planck_sabiti_grafik` (+ `_1` copy) | Plots Planck curves for **300, 400, 500 and 600 K** over 0.1–14 µm, which shows the Wien peak shift |
| `Planck_Fonksiyonunun_Girilen_Bant_Aralığı_için_İntegrali` | `dalgaboyu_integral(T, λ)`: spectral radiance at a given temperature and wavelength, in SI units and in µm-based units |
| `look-up_table` | `create_lookup_table(...)` **integrates Planck's law over a band** (e.g. the 8–14 µm LWIR window), applies emissivity and saves a **temperature → in-band radiance table** to a `.mat` file |

### Example: radiance look-up table

```matlab
% LWIR band 8–14 µm, emissivity 0.95, 250 K … 400 K in 1 K steps
create_lookup_table('lut_lwir.mat', 8e-6, 14e-6, 0.95, 250, 400, 1);
load('lut_lwir.mat');            % temperatures, radiance_values
plot(temperatures, radiance_values);
```

Tables like this are the basis of **radiometric calibration in thermal cameras**: a measured in-band radiance is mapped back to an object temperature.

## 🚀 Usage

The files are saved as `.txt`. Rename them to `.m` (or paste them into the MATLAB editor) and run:

```bash
cd "Planck function, wien and stefan boltzman"
for f in *.txt; do mv "$f" "${f%.txt}.m"; done
```

> Comments in the code are in Turkish.

---

<div align="center">

Made by **[Yusuf Erkan](https://www.linkedin.com/in/yusuferkan1/)**

</div>
