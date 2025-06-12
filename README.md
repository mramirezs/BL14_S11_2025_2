# Elementos de la sintaxis de Shell Scripting II

## 📚 Curso: Principios de programación - Bioinformática
**Universidad Peruana de Ciencias Aplicadas (UPC)**  
**Programa de Biología - Facultad de Ciencias de la Salud**

### 👨‍🏫 Docentes:
- Frank Guzman Escudero
- Manuel Ramírez Sáenz

### 📅 Semestre: 2025-02

---

## 🎯 Logro de la sesión

Al finalizar la sesión, el estudiante utiliza expresiones regulares en shell scripting para el procesamiento, extracción y transformación de datos biológicos.

**Palabras clave:** Expresiones regulares, Comandos avanzados, Procesamiento de datos, Extracción de datos, Transformación de datos

---

## 📋 Contenido

1. [Partes básicas de un Shell script](#partes-básicas-de-un-shell-script)
2. [Comando read](#comando-read)
3. [Trabajar con textos en Bash](#trabajar-con-textos-en-bash)
4. [Ejercicios prácticos](#ejercicios-prácticos)

---

## 🔧 Partes básicas de un Shell script

Un script no es más que un archivo que contiene un conjunto de órdenes para realizar una tarea.

### Estructura básica:

```bash
#!/bin/bash
# Fecha de escritura: 31/10/2024
# Este programa te informa en que directorio se encuentra trabajando la terminal.

lugar=$(pwd)
echo "en este momento te encuentras trabajando en este $lugar, no vayas a perderte"
```

### Componentes principales:

1. **Shebang (`#!/bin/bash`)**: La primera línea indica al sistema que use shell BASH
2. **Comentarios**: Todo lo que está después del carácter `#` es ignorado por el interpretador
3. **Bloque del código**: Las instrucciones ejecutables del script

### 📝 Buenas prácticas y recursos:

La primera lìnea del script le indica al sistema que tiene que usar.

> Bash

```bash
$ cat my_script.sh
```

```
#!/bin/bash

echo "Hello world"
```

```bash
$ bash my_script.sh
$ Hello World
```

> Python

```bash
$ cat my_script.py
```

```
#!/usr/bin/python

print("Hello world")
```

```bash
$ python my_script.sh
$ Hello World
```

- [Google Shell Style Guide](https://google.github.io/styleguide/shellguide.html)
- [Anyone Can Write Good Bash](https://blog.yossarian.net/2020/01/23/Anybody-can-write-good-bash-with-a-little-effort)
- [Bash Style Guide and Coding Standard](https://lug.fh-swf.de/vim/vim-bash/StyleGuideShell.en.pdf)
- [Plantilla de script en GitHub](https://github.com/raupulus/bash-guide-style/blob/main/plantilla.sh)

### 🔍 Verificación con ShellCheck

Utiliza [ShellCheck](https://www.shellcheck.net/) para verificar y mejorar tus scripts:

```bash
# Ejemplo de script con errores
#!/bin/bash
#Fecha de escritura: 31/10/2024
insulina ="MALWMRLLPLLALLALWGPDPAAAFVNQHLCGSHLVEALYLVCGERGFFYTPKTRREAEDLQVGQVELGGGPGAGSLQPLALEGSLQKRGIVEQCCTSICSLYQLENYCN"
echo "$insulina"
```

---

## 📖 Comando read

El comando `read` lee la entrada estándar y asigna las palabras leídas en la(s) variable(s) cuyo nombre se pasa como argumento.

### Sintaxis:
```bash
read var1 var2 ...
```

### Ejemplo:
```bash
#!/bin/bash

echo "Escribamos una palabra"
read palabra
echo "Escribamos la $palabra"
```

### Ejemplo práctico con proteínas:
```bash
#!/bin/bash
# Fecha de escritura: 31/10/2024

insulina="MALWMRLLPLLALLALWGPDPAAAFVNQHLCGSHLVEALYLVCGERGFFYTPKTRREAEDLQVGQVELGGGPGAGSLQPLALEGSLQKRGIVEQCCTSICSLYQLENYCN"
echo "La proteína se llama insulina y es la siguiente $insulina"

read -p "Ingrese el nombre de la proteína:" PROTEINA
read -p "Ingrese el número de aminoácidos de la secuencia :" LONGITUD

echo "La siguiente proteína es $PROTEINA y su longitud es $LONGITUD"
```

---

## 📝 Trabajar con textos en Bash

### 1. 📏 Encontrar la longitud de una cadena

```bash
${#variable}
```

**Ejemplo:**
```bash
var="MaRSGyB"
echo ${#var}  # Resultado: 7
```

### Métodos alternativos:
```bash
echo $var | wc -c      # Cuenta caracteres incluyendo salto de línea
echo -n $var | wc -c   # Cuenta solo caracteres
echo $var | awk '{print length}'  # Usando awk
```

### Script de ejemplo con secuencias biológicas:
```bash
#!/bin/bash
# Cadenas biológicas
ADN="ATCGTACGATCGATCGATCG"
ARN="AUGCGAUCGAUCGUACGUA"

# Encontrar y mostrar la longitud de las cadenas
echo "La longitud de la cadena de ADN es: ${#ADN}"
echo "La longitud de la cadena de ARN es: ${#ARN}"
```

### 2. ✂️ Extracción de subcadenas

#### Sintaxis básica:
```bash
${cadena:posicion_caracter:longitud}
```

**Nota:** El índice comienza en 0.

#### Ejemplos:
```bash
string="ABCDEFGHIJKL"
echo ${string:0:3}   # ABC
echo ${string:3:3}   # DEF
echo ${string:6}     # GHIJKL
```

#### Ejemplo con proteínas:
```bash
proteina="MDLSPFLRINPCGYAGMEMAKISQWKPEATTNNIAPRLLENILALLNNPDFEYITA"
echo ${proteina:0:2}   # MD
echo ${proteina:3}     # SPFLRINPCGYAGMEMAKISQWKPEATTNNIAPRLLENILALLNNPDFEYITA
```

#### Extracción usando patrones:

**Eliminar desde el principio:**
```bash
${variable#*patron}    # Elimina hasta la primera aparición
${variable##*patron}   # Elimina hasta la última aparición
```

**Eliminar desde el final:**
```bash
${variable%patron*}    # Elimina desde el final hasta la primera aparición
${variable%%patron*}   # Elimina desde el final hasta la última aparición
```

#### Ejemplos prácticos:
```bash
var="uno;dos;tres"
echo ${var#*;}    # dos;tres
echo ${var##*;}   # tres
echo ${var%;*}    # uno;dos
echo ${var%%;*}   # uno
```

### 3. 🔄 Reemplazar subcadenas

```bash
${cadena/buscar/reemplazar}     # Sustituye la primera coincidencia
${cadena//buscar/reemplazar}    # Sustituye todas las coincidencias
```

#### Ejemplos:
```bash
var="uno;dos;tres"
echo ${var/uno/cuatro}    # cuatro;dos;tres
echo ${var//uno/cuatro}   # cuatro;dos;tres

# Cambiar extensión de archivo
var="image.png"
echo ${var/png/jpg}       # image.jpg
```

---

## 🧬 Ejercicios prácticos

### Ejercicio 1: Extracción de subcadenas
```bash
codones="AUG UAC GCU UAA GCA UAG"

# Diferentes extracciones
echo ${codones:3}      # " UAC GCU UAA GCA UAG"
echo ${codones:0:3}    # "AUG"
echo ${codones:11}     # "U UAA GCA UAG"
echo ${codones:-4}     # "U UAG"
echo ${codones:-4:2}   # "U "
```

### Ejercicio 2: Borrar cadenas
```bash
codones="AUG UAC GCU UAA GCA UAG"

echo ${codones#A*C}    # " GCU UAA GCA UAG"
echo ${codones##A*C}   # " GCU UAA GCA UAG"
```

### Ejercicio 3: Reemplazar cadenas
```bash
codones="AUG UAC GCU UAA GCA UAG"

echo ${codones/UA/CC}      # "AUG CCG CU UAA GCA UAG"
echo ${codones//AUG/Met}   # "Met UAC GCU UAA GCA UAG"
```

### 🧪 Proyecto: Traductor de codones

**Objetivo:** Crear un script que cambie todos los tripletes de codones a nombres de aminoácidos.

**Tabla de códigos genéticos (algunos ejemplos):**
- AUG → Met (Metionina)
- UUU, UUC → Phe (Fenilalanina)  
- UAA, UAG, UGA → Alto (Codón de parada)
- GCU, GCC, GCA, GCG → Ala (Alanina)

### 🧬 Ejercicio: Conversión DNA a RNA

**Objetivo:** Convertir secuencia de DNA a RNA mensajero reemplazando Timina (T) por Uracilo (U).

```bash
# DNA: 5´ AAACGCGGCCTTTCCAACGGC 3´
# RNA: 5' AAACGCGGCCUUUCCAACGGC 3'

#!/bin/bash
dna="AAACGCGGCCTTTCCAACGGC"
rna=${dna//T/U}
echo "DNA: $dna"
echo "RNA: $rna"
```

---

## 📚 Referencias bibliográficas

- Blum, R., & Bresnahan, C. (2021). Linux command line and Shell scripting bible (Fourth edition). Wiley. Capítulo 11.

---

## 📝 Actividad Asincrónica

Envíe el historial de los ejercicios realizados en esta sesión indicando TODOS sus resultados.

**Pregunta de reflexión:** ¿En qué podrían aplicar el reemplazo de cadenas en bioinformática?

---

## 🏷️ Tags

`#shell-scripting` `#bash` `#bioinformática` `#procesamiento-datos` `#UPC` `#biología`
