# Protocolos terapéuticos — agentes físicos y electroterapia

App de consulta con **3.517 protocolos** extraídos del tratado *Agentes Físicos Terapéuticos y Electroterapia* y de las doce obras de referencia que lo sostienen.

Funciona **sin conexión**: una vez abierta la primera vez, los datos quedan en el dispositivo.

---

## Qué hace

- **Busca** en todo el contenido a la vez: patología, agente, parámetro, técnica. Sin acentos también encuentra (`epicondilalgia`, `laser`).
- **Agrupa por cuadro clínico**: al buscar una condición aparecen juntos todos los agentes aplicables a ella, uno por fila, y arriba un resumen con cada agente y cuántos protocolos aporta. Pulsando ese resumen se filtra por ese agente.
- **Parámetros en columnas fijas**: frecuencia, onda y modo, pulso, intensidad, potencia y dosis, longitud de onda, tiempo, temperatura y otros. Las nueve **aparecen siempre**, aunque estén vacías, para que se vea de un vistazo qué no consigna la fuente; un punto gris significa que ese dato no figura en el original. Nada del texto se pierde: lo que no encaja en ninguna columna va a «Otros».
- **Técnica y sesiones al hacer clic** en el protocolo. Las advertencias quedan siempre a la vista.
- **Lo que no está dosificado va aparte**: los 656 agentes que la obra señala como posible aplicación sin dar ningún parámetro no se mezclan con los protocolos; van en un bloque propio al final, con su nota.
- **Filtra** por región anatómica, familia de agentes, modalidad y fase del proceso.
- Cada ficha lleva **parámetros, técnica, sesiones, fuente, capítulo y hoja** del tratado, para poder volver al razonamiento completo. «Hoja» es el número de hoja del PDF —el que se teclea en el lector para saltar—; entre paréntesis va el número impreso en esa página, 26 unidades menor.
- Las **advertencias** —nivel de evidencia, discrepancias entre obras, lagunas declaradas— viajan con cada protocolo, en el recuadro ámbar.

---

## Ponerlo en marcha

### 1. Subir el repositorio

Crea en GitHub un repositorio llamado **`protocolos-terapeuticos`** y sube el contenido de esta carpeta (los ficheros sueltos, no la carpeta dentro de otra carpeta).

Si prefieres hacerlo sin consola: en GitHub, *Add file* → *Upload files*, arrastra todo y confirma.

### 2. Activar la web

En el repositorio: **Settings → Pages**. En *Source* elige **GitHub Actions**. En un par de minutos la app estará en:

```
https://grana2jorgel.github.io/protocolos-terapeuticos/
```

### 3. Instalarla en el móvil

Abre esa dirección en Chrome en el móvil y usa **Añadir a pantalla de inicio**. Queda como una app, con su icono, y funciona sin datos ni wifi.

### 4. Conseguir el APK

Cada vez que subas un cambio, GitHub construye el APK solo. Lo encuentras en:

- **Releases**, en la portada del repositorio, o
- **Actions** → la última ejecución → *Artifacts* → `protocolos-terapeuticos-apk`

El APK **lleva los datos dentro**: no necesita conexión ni siquiera la primera vez. Para instalarlo, el móvil pedirá permiso para *instalar apps de origen desconocido*; está firmado con una clave de depuración, que es suficiente para uso propio pero no sirve para publicar en Google Play.

---

## Actualizar los datos

Todos los protocolos están en **`datos.js`**, en un único array. Para cambiar, añadir o corregir uno, se edita ese fichero.

Después de editarlo hay que **subir el número de versión** en la primera línea de `sw.js`:

```js
const VERSION = 'protocolos-v5';   // antes v4
```

Sin ese cambio, los móviles que ya tengan la app seguirán viendo los datos antiguos, porque la caché está pensada para funcionar sin conexión.

---

## Qué contiene cada ficha

| Campo | Qué es |
|---|---|
| `region` | Región anatómica o ámbito clínico |
| `cuadro` | Patología u objetivo terapéutico |
| `fase` | Aguda, subaguda, crónica |
| `modalidad` | Agente físico concreto |
| `familia` | Grupo al que pertenece el agente |
| `parametros` | Todos los valores con su unidad |
| `tecnica` | Colocación, montaje, método |
| `sesiones` | Duración, número y periodicidad |
| `fuente` | Sigla de la obra de origen |
| `cap` | Capítulo del tratado |
| `pag`, `pimp` | Hoja del PDF y número impreso en esa página |
| `origen` | Cuerpo del tratado, Anexo B o Volumen de casos |
| `notas` | Advertencias, discrepancias, evidencia |
| `p` | Los parámetros ya repartidos en columnas (`frec`, `onda`, `pulso`, `inten`, `dosis`, `lambda`, `tiempo`, `temp`, `otros`) |
| `sd` | Vale 1 cuando la fuente no consigna ningún parámetro: va al bloque aparte |

### Siglas de las obras

**RM** Rodríguez Martín · **MC** Martín Cordero · **MA** Maya y Albornoz · **KR** Krusen · **AT** Atlas de fotobiomodulación · **WH** Whitten · **SE** y **SE2** Simplificando la Electro · **MMSS** E-book Electro MMSS · **FRN** Stokes y Stack · **FN** Bisbe y cols. · **BC** corpus público de tecarterapia · **EV** literatura indexada · **TQ** documentación técnica.

---

## Advertencia de uso clínico

Un protocolo no es una indicación. Antes de aplicar cualquiera:

- Verifica las **contraindicaciones** en el capítulo 42 del tratado.
- Comprueba **en qué unidades** expresa cada magnitud el equipo que utilizas: entre fabricantes hay diferencias de hasta veinte veces en potencia.
- Recuerda que buena parte de estos parámetros procede de **consenso clínico y no de evidencia contrastada**, y que cuando dos obras discrepan aquí figuran las dos cifras, nunca un promedio.

La responsabilidad de la indicación y de la dosis es siempre de quien prescribe.
