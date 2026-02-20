# F4NT4SM4 – Strudel en local y en la nube

Live coding con [Strudel](https://strudel.cc) usando la pista **F4NT4SM4BASE.mp3** como sample, con **visuales** (oscilloscope, punchcard, etc.).

---

## Opción A: Jugar en el REPL de Strudel (strudel.cc) con samples desde GitHub

1. Sube el repo a GitHub (ver más abajo).
2. Abre **[strudel.cc](https://strudel.cc)** en el navegador.
3. Pega y evalúa (Ctrl+Enter / Cmd+Enter) para cargar tus samples:

```javascript
samples('https://raw.githubusercontent.com/m1gue21/F4NT4SM4/main/strudel.json')
```

4. Luego usa el tema con base + ritmo + visuales (copia el bloque del [index.html](index.html) o el ejemplo de “Ejemplo con visuales” más abajo).

No necesitas levantar ningún servidor: los samples se sirven desde GitHub.

---

## Opción B: Correr todo en local

1. **Terminal 1** – servidor de samples (puerto 5432):
   ```bash
   npm run samples
   ```

2. **Terminal 2** – servidor web (puerto 3000):
   ```bash
   npm run serve
   ```

3. Abre **http://localhost:3000** y en el código usa:
   ```javascript
   samples('http://localhost:5432/')
   ```

---

## Subir el proyecto a GitHub

Si ya tienes el repo creado en GitHub (p. ej. `m1gue21/F4NT4SM4`), en la raíz del proyecto ejecuta:

```bash
git init
git add .
git commit -m "first commit: Strudel + base F4NT4SM4 + visuales"
git branch -M main
git remote add origin https://github.com/m1gue21/F4NT4SM4.git
git push -u origin main
```

A partir de ahí puedes seguir trabajando con `git add`, `git commit` y `git push`.

---

## Estructura del repo

| Qué | Dónde |
|-----|--------|
| Sample base | `samples/base.mp3` |
| Mapa de samples para GitHub | `strudel.json` (raíz) |
| Página con REPL embebido | `index.html` |

El REPL ya incluye un tema de ejemplo con **visuales**: oscilloscope en la base (`. _scope()`), punchcard en una línea de notas (`. _punchcard()`). Puedes añadir `. _pianoroll()`, `. _spiral()`, `. _spectrum()`, `. _pitchwheel()` a cualquier patrón.

---

## Ejemplo con visuales (para strudel.cc o local)

```javascript
samples('https://raw.githubusercontent.com/m1gue21/F4NT4SM4/main/strudel.json')
// o en local: samples('http://localhost:5432/')

setcps(0.5)

stack(
  s("base").loop(1).gain(0.7)._scope(),
  s("bd sd bd sd").gain(0.4),
  s("hh*8").gain(0.15),
  note("<c2 eb2 g2 bb2>/4").scale("d3:minor").s("sawtooth").lpf(800).gain(0.25)._punchcard({ fill: 1, active: "#FFCA28", inactive: "#7491D2", cycles: 4 })
)
```

---

## Ideas para el tema

- Cambiar `setcps(0.5)` para ajustar tempo.
- Probar `s("base").chop(16)` o `.striate(8)` para efectos granulares.
- Más capas con `stack()` o líneas con `$:`.
- Visuales: `. _spectrum()` (espectro), `. _spiral()`, `. _pitchwheel()` (círculo de afinación).
