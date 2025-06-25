
# 💡 Specular Lighting with Phong Model

Specular lighting adalah bagian dari model pencahayaan **Phong** yang mensimulasikan highlight (kilau cahaya) pada permukaan objek, khususnya pada permukaan yang halus dan reflektif.

---

## 📌 Komponen Phong Lighting Model

Model Phong terdiri dari tiga komponen utama:

1. **Ambient**: Cahaya latar umum di seluruh scene.
2. **Diffuse**: Cahaya menyebar akibat permukaan yang kasar.
3. **Specular**: Cahaya terpantul tajam seperti cermin – *fokus utama di sini*.

---

## 🔦 Rumus Specular Phong Lighting

```math
I_{specular} = k_s \cdot I_L \cdot (\text{max}(0, \vec{R} \cdot \vec{V}))^n
```

### Keterangan:
- `k_s` : koefisien specular (seberapa reflektif permukaan)
- `I_L` : intensitas cahaya
- `\vec{R}` : vektor refleksi cahaya terhadap normal
- `\vec{V}` : arah menuju kamera (viewer)
- `n` : shininess exponent (mengontrol fokus highlight)

---

## 🔁 Langkah Perhitungan

1. Hitung **vektor normal** permukaan (`N`)
2. Hitung **vektor cahaya** dari titik ke sumber (`L`)
3. Hitung **vektor refleksi**:
```math
\vec{R} = 2(\vec{N} \cdot \vec{L})\vec{N} - \vec{L}
```
4. Hitung **vektor ke kamera** (`V`)
5. Lakukan **dot product** `R • V` (nilai antara 0–1)
6. Pangkatkan hasil dengan **shininess exponent `n`**

---

## 🧠 Intuisi Fisik

- `n` tinggi → highlight tajam (seperti logam)
- `n` rendah → highlight menyebar (seperti plastik)

---

## ✍️ Contoh GLSL (Dari OGLDev)

```glsl
vec3 LightDirection = normalize(LightPosition - FragPos);
vec3 ReflectDir = reflect(-LightDirection, Normal);
vec3 ViewDir = normalize(CameraPos - FragPos);
float spec = pow(max(dot(ViewDir, ReflectDir), 0.0), Shininess);
vec3 Specular = LightColor * spec * SpecularStrength;
```

---

## 🧾 Kesimpulan

Specular lighting pada model Phong menciptakan highlight tajam tergantung arah pandang dan permukaan objek. Ini sangat penting untuk menciptakan efek visual realistis, khususnya pada objek reflektif.

---

## 📚 Referensi

- [OGLDev - Tutorial 19](https://www.ogldev.org/www/tutorial19/tutorial19.html)
