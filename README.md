# 🧬 Elementos de la sintaxis de Shell Scripting II

## 📚 Información del Curso
**Curso:** Principios de programación - Bioinformática  
**Universidad:** Universidad Peruana de Ciencias Aplicadas (UPC)  
**Programa:** Biología  
**Facultad:** Ciencias de la Salud  
**Semestre:** 2025-02  

### 👨‍🏫 Docentes:
- **Frank Guzman Escudero**
- **Manuel Ramírez Sáenz**

---

## 🎯 Objetivo de Aprendizaje

Al finalizar esta sesión, serás capaz de:

- ✅ **Crear scripts básicos** siguiendo las buenas prácticas
- ✅ **Usar el comando `read`** para obtener datos del usuario
- ✅ **Manipular cadenas de texto** (medir, extraer, reemplazar)
- ✅ **Aplicar estos conceptos** a secuencias biológicas (ADN, ARN, proteínas)
- ✅ **Procesar datos bioinformáticos** de forma automatizada

**Palabras clave:** Shell scripting, manipulación de texto, secuencias biológicas, automatización

---

## 📑 Contenido de la Clase

1. [Repaso: ¿Qué sabemos hasta ahora?](#-repaso-qué-sabemos-hasta-ahora)
2. [Anatomía de un Shell Script](#-anatomía-de-un-shell-script)
3. [Comando read: Interactuando con el usuario](#-comando-read-interactuando-con-el-usuario)
4. [Manipulación de texto en Bash](#-manipulación-de-texto-en-bash)
5. [Ejercicios paso a paso](#-ejercicios-paso-a-paso)
6. [Aplicaciones en Bioinformática](#-aplicaciones-en-bioinformática)

---

## 🧠 Repaso: ¿Qué sabemos hasta ahora?

### Variables en Bash
Las variables son como "cajas" donde guardamos información:

```bash
# Crear una variable (¡sin espacios alrededor del =!)
nombre="Juan"
edad=25
secuencia_dna="ATCGATCG"

# Usar una variable (con $)
echo $nombre
echo "La edad es: $edad años"
echo "ADN: $secuencia_dna"
```

**⚠️ Errores comunes:**
```bash
# ❌ INCORRECTO - espacios alrededor del =
nombre = "Juan"

# ❌ INCORRECTO - usar $ al asignar
$nombre="Juan"

# ✅ CORRECTO
nombre="Juan"
echo $nombre
```

### ¿Qué es un Script?
Un script es simplemente un archivo de texto que contiene comandos de Bash, como si escribieras los comandos uno por uno en la terminal, pero guardados para ejecutarlos después.

---

## 🏗️ Anatomía de un Shell Script

### Las 3 partes esenciales:

#### 1. 🔗 El Shebang (#!/bin/bash)
```bash
#!/bin/bash
```
- **¿Qué es?** La primera línea que le dice al sistema: "ejecuta este archivo con Bash"
- **¿Por qué es importante?** Sin esto, el sistema no sabe cómo interpretar tu script
- **Analogía:** Es como el encabezado de una carta que dice "escrito en español"

#### 2. 📝 Comentarios (líneas que empiezan con #)
```bash
#!/bin/bash
# Fecha de escritura: 12/06/2025
# Este script analiza una secuencia de insulina
# Autor: Mi nombre
```
- **¿Para qué sirven?** Para explicar qué hace el código (para ti y otros)
- **Regla de oro:** Si vuelves a leer tu script en 6 meses, ¿entenderías qué hace?
- **El computador los ignora** pero son esenciales para los humanos

#### 3. 💻 El código ejecutable
```bash
#!/bin/bash
# Análisis de insulina

# Guardar la secuencia en una variable
insulina="MALWMRLLPLLALLALWGPDPAAAFVNQHLCGSHLVEALYLVCGERGFFYTPKTRREAEDLQVGQVELGGGPGAGSLQPLALEGSLQKRGIVEQCCTSICSLYQLENYCN"

# Mostrar información
echo "Analizando secuencia de insulina..."
echo "Secuencia: $insulina"
echo "Análisis completado."
```

### 📋 Ejemplo completo paso a paso:

```bash
#!/bin/bash
#=============================================================================
# SCRIPT: analisis_basico.sh
# PROPÓSITO: Mostrar información básica de una proteína
# AUTOR: Estudiante de Bioinformática
# FECHA: 12 de junio, 2025
#=============================================================================

# Paso 1: Definir la secuencia de la proteína
proteina="MTESFAQLFEESLKEIETRPGSIVRGVVVAIDKDVV"

# Paso 2: Mostrar la secuencia
echo "=== ANÁLISIS DE PROTEÍNA ==="
echo "Secuencia: $proteina"

# Paso 3: Obtener la longitud
longitud=${#proteina}
echo "Longitud: $longitud aminoácidos"

# Paso 4: Mensaje final
echo "Análisis completado exitosamente."
```

### 🛠️ Cómo ejecutar el script:

```bash
# 1. Crear el archivo
nano mi_script.sh

# 2. Darle permisos de ejecución
chmod +x mi_script.sh

# 3. Ejecutarlo
./mi_script.sh
```

### 📏 Herramientas de calidad: ShellCheck

[ShellCheck](https://www.shellcheck.net/) es como un "corrector ortográfico" para scripts:

**Ejemplo de código con errores:**
```bash
#!/bin/bash
# ❌ Código con errores
insulina ="MALWMRLLPLLALLAL"  # Error: espacio antes del =
echo "$insulina"
```

**ShellCheck detecta:**
- ✋ Espacios incorrectos alrededor de `=`
- ✋ Variables no declaradas
- ✋ Comillas faltantes
- ✋ Y muchos otros errores comunes

---

## 📖 Comando read: Interactuando con el usuario

### ¿Qué hace el comando `read`?
El comando `read` **pausa** el script y espera que el usuario escriba algo, luego guarda esa información en una variable.

### Sintaxis básica:
```bash
read nombre_variable
```

### 🔍 Ejemplo básico:
```bash
#!/bin/bash

echo "¿Cómo te llamas?"
read nombre
echo "Hola, $nombre! Bienvenido al curso de bioinformática."
```

**¿Qué pasa cuando ejecutas esto?**
1. Aparece: "¿Cómo te llamas?"
2. El script **espera** a que escribas algo
3. Escribes tu nombre y presionas Enter
4. El script continúa y muestra: "Hola, [tu nombre]! Bienvenido..."

### 📝 Versión mejorada con `-p` (prompt):
```bash
#!/bin/bash

read -p "¿Cómo te llamas? " nombre
echo "Hola, $nombre!"
```
- `-p` permite mostrar el mensaje y leer la entrada en la misma línea

### 🧬 Ejemplo aplicado a bioinformática:
```bash
#!/bin/bash
#=============================================================================
# SCRIPT: info_proteina.sh  
# PROPÓSITO: Recopilar información sobre una proteína del usuario
#=============================================================================

# Secuencia predefinida de insulina
insulina="MALWMRLLPLLALLALWGPDPAAAFVNQHLCGSHLVEALYLVCGERGFFYTPKTRREAEDLQVGQVELGGGPGAGSLQPLALEGSLQKRGIVEQCCTSICSLYQLENYCN"

# Mostrar la secuencia
echo "=== ANÁLISIS DE PROTEÍNA ==="
echo "Secuencia de insulina: $insulina"

# Obtener información del usuario
read -p "¿Cuál es el nombre de esta proteína? " nombre_proteina
read -p "¿Cuántos aminoácidos crees que tiene? " estimacion

# Calcular la longitud real
longitud_real=${#insulina}

# Mostrar resultados
echo ""
echo "--- RESULTADOS ---"
echo "Proteína identificada como: $nombre_proteina"
echo "Tu estimación: $estimacion aminoácidos"
echo "Longitud real: $longitud_real aminoácidos"
```

### 📚 Múltiples variables con read:
```bash
#!/bin/bash

echo "Ingresa tres bases nitrogenadas separadas por espacios:"
read base1 base2 base3

echo "Las bases que ingresaste son:"
echo "1. $base1"
echo "2. $base2" 
echo "3. $base3"
```

---

## 📝 Manipulación de texto en Bash

### 🧭 Conceptos fundamentales

#### ¿Qué es una cadena?
Una **cadena** (string) es una secuencia de caracteres. En bioinformática:
- Secuencia de ADN: `"ATCGATCG"`
- Secuencia de ARN: `"AUGCUAGC"`
- Secuencia de proteína: `"MKTLRV"`

#### ¿Qué es una subcadena?
Una **subcadena** es una parte de una cadena más grande:

```
Cadena completa: "ATCGATCG"
                  01234567  ← posiciones (índices)

Subcadenas posibles:
- "ATC" (posiciones 0-2)
- "GAT" (posiciones 3-5)
- "TCG" (posiciones 5-7)
```

---

### 📏 1. Medir la longitud de una cadena

#### Sintaxis: `${#variable}`
```bash
secuencia="ATCGATCG"
longitud=${#secuencia}
echo "La secuencia tiene $longitud bases"
# Resultado: La secuencia tiene 8 bases
```

#### 🧪 Ejercicio práctico:
```bash
#!/bin/bash
# Comparar longitudes de diferentes secuencias

# Definir secuencias
adn="ATCGTACGATCGATCGATCG"
arn="AUGCGAUCGAUCGUACGUA"
proteina="MKTLRVQPSLQPIF"

# Calcular longitudes
long_adn=${#adn}
long_arn=${#arn}
long_proteina=${#proteina}

# Mostrar resultados
echo "=== COMPARACIÓN DE LONGITUDES ==="
echo "ADN: $long_adn nucleótidos"
echo "ARN: $long_arn nucleótidos"  
echo "Proteína: $long_proteina aminoácidos"

# Determinar cuál es más larga
echo ""
echo "La secuencia de ADN es la más larga: $long_adn nucleótidos"
```

#### 🔍 Métodos alternativos (para referencia):
```bash
# Método 1: Usando wc -c (cuenta caracteres + salto de línea)
echo $secuencia | wc -c

# Método 2: Usando wc -c sin salto de línea
echo -n $secuencia | wc -c

# Método 3: Usando awk
echo $secuencia | awk '{print length}'

# ✅ RECOMENDADO: ${#variable} - más eficiente y directo
longitud=${#secuencia}
```

---

### ✂️ 2. Extraer partes de una cadena (subcadenas)

#### Sintaxis básica: `${cadena:inicio:longitud}`

```bash
# Importante: Los índices empiezan en 0
secuencia="ATCGATCG"
#          01234567  ← posiciones

# Extraer los primeros 3 caracteres
primeros_tres=${secuencia:0:3}
echo $primeros_tres  # Resultado: ATC

# Extraer desde la posición 3, tomar 4 caracteres
medio=${secuencia:3:4}
echo $medio  # Resultado: GATC

# Extraer todo desde la posición 5
final=${secuencia:5}
echo $final  # Resultado: TCG
```

#### 🧬 Ejemplo biológico - Análisis de codones:
```bash
#!/bin/bash
# Análisis de codones en una secuencia de ARN

# Secuencia de ejemplo
arn_secuencia="AUGUCGAAACCCUAG"
echo "Secuencia de ARN: $arn_secuencia"
echo "Longitud total: ${#arn_secuencia} nucleótidos"

echo ""
echo "=== DIVISIÓN EN CODONES ==="

# Extraer codones (grupos de 3 nucleótidos)
codon1=${arn_secuencia:0:3}
codon2=${arn_secuencia:3:3}
codon3=${arn_secuencia:6:3}
codon4=${arn_secuencia:9:3}
codon5=${arn_secuencia:12:3}

echo "Codón 1: $codon1"
echo "Codón 2: $codon2"
echo "Codón 3: $codon3"
echo "Codón 4: $codon4"
echo "Codón 5: $codon5"
```

#### 🔬 Ejemplo avanzado - Extracción de dominios proteicos:
```bash
#!/bin/bash
# Análisis de dominios en la proteína ribosómica bS1

# Secuencia completa de la proteína (557 aminoácidos)
proteina_completa="MTESFAQLFEESLKEIETRPGSIVRGVVVAIDKDVVLVDAGLKSESAIPAEQFKNAQGELEIQVGDEVDVALDAVEDGFGETLLSREKAKRHEAWITLEKAYEDAETVTGVINGKVKGGFTVELNGIRAFLPGSLVDVRPVRDTLHLEGKELEFKVIKLDQKRNNVVVSRRAVIESENSAERDQLLENLQEGMEVKGIVKNLTDYGAFVDLGGVDGLLHITDMAWKRVKHPSEIVNVGDEITVKVLKFDRERTRVSLGLKQLGEDPWVAIAKRYPEGTKLTGRVTNLTDYGCFVEIEEGVEGLVHVSEMDWTNKNIHPSKVVNVGDVVEVMVLDIDEERRRISLGLKQCKANPWQQFAETHNKGDRVEGKIKSITDFGIFIGLDGGIDGLVHLSDISWNVAGEEAVREYKKGDEIAAVVLQVDAERERISLGVKQLAEDPFNNWVALNKKGAIVTGKVTAVDAKGATVELADGVEGYLRASEASRDRVEDATLVLSVGDEVEAKFTGVDRKNRAISLSVRAKDEADEKDAIATVNKQEDANFSNNAMAEAFKAAKGE"

echo "=== ANÁLISIS DE DOMINIOS PROTEICOS ==="
echo "Proteína: Subunidad ribosómica pequeña bS1 (E. coli)"
echo "Longitud total: ${#proteina_completa} aminoácidos"

# Extraer dominios según UniProt (posiciones 21-87, 105-171, etc.)
echo ""
echo "--- EXTRACCIÓN DE DOMINIOS ---"

# Dominio 1 (posiciones 21-87 en notación biológica = 20-86 en programación)
inicio_dom1=20
fin_dom1=87
longitud_dom1=$((fin_dom1 - inicio_dom1))
dominio1=${proteina_completa:$inicio_dom1:$longitud_dom1}

echo "Dominio 1 (posiciones 21-87):"
echo "Secuencia: $dominio1"
echo "Longitud: ${#dominio1} aminoácidos"

# Primeros y últimos aminoácidos del dominio
primer_aa=${dominio1:0:1}
ultimo_aa=${dominio1: -1}
echo "Primer aminoácido: $primer_aa"
echo "Último aminoácido: $ultimo_aa"
```

#### 📊 Extracción usando índices negativos:
```bash
secuencia="ATCGATCG"

# Últimos 3 caracteres
ultimos_tres=${secuencia: -3}
echo $ultimos_tres  # Resultado: TCG

# Desde el penúltimo hasta el final
final=${secuencia: -2}
echo $final  # Resultado: CG
```

---

### 🔍 3. Extracción usando patrones

#### Eliminar desde el principio hasta un patrón:

##### `${variable#*patron}` - Elimina hasta la PRIMERA aparición
```bash
genes="BRCA1,BRCA2,TP53,PTEN"

# Eliminar desde el inicio hasta la primera coma
sin_primer_gen=${genes#*,}
echo $sin_primer_gen  # Resultado: BRCA2,TP53,PTEN
```

##### `${variable##*patron}` - Elimina hasta la ÚLTIMA aparición
```bash
genes="BRCA1,BRCA2,TP53,PTEN"

# Eliminar desde el inicio hasta la última coma (obtener último elemento)
ultimo_gen=${genes##*,}
echo $ultimo_gen  # Resultado: PTEN
```

#### Eliminar desde el final hasta un patrón:

##### `${variable%patron*}` - Elimina desde el final hasta la PRIMERA aparición
```bash
archivo="secuencia.fasta.txt"

# Eliminar la extensión .txt
sin_txt=${archivo%.txt}
echo $sin_txt  # Resultado: secuencia.fasta
```

##### `${variable%%patron*}` - Elimina desde el final hasta la ÚLTIMA aparición
```bash
archivo="secuencia.fasta.txt"

# Eliminar todo después del primer punto
solo_nombre=${archivo%%.*}
echo $solo_nombre  # Resultado: secuencia
```

#### 🧬 Ejemplo práctico con genes:
```bash
#!/bin/bash
# Análisis de lista de genes relacionados con cáncer

genes_cancer="BRCA1,BRCA2,TP53,PTEN,CHEK2,PALB2,ATM,CDH1"
echo "Lista completa: $genes_cancer"

echo ""
echo "=== EXTRACCIÓN DE GENES ==="

# Obtener el primer gen
primer_gen=${genes_cancer%%,*}
echo "Primer gen: $primer_gen"

# Obtener el último gen  
ultimo_gen=${genes_cancer##*,}
echo "Último gen: $ultimo_gen"

# Obtener todos excepto el primero
resto_genes=${genes_cancer#*,}
echo "Resto de genes: $resto_genes"

# Obtener todos excepto el último
sin_ultimo=${genes_cancer%,*}
echo "Sin el último: $sin_ultimo"
```

---

### 🔄 4. Reemplazar texto en cadenas

#### Sintaxis básica:
```bash
${variable/buscar/reemplazar}    # Reemplaza solo la PRIMERA ocurrencia
${variable//buscar/reemplazar}   # Reemplaza TODAS las ocurrencias
```

#### 🧪 Ejemplos básicos:
```bash
secuencia="ATCGATCGATCG"

# Reemplazar solo la primera T por U
primera=${secuencia/T/U}
echo $primera  # Resultado: AUCGATCGATCG

# Reemplazar todas las T por U (ADN → ARN)
todas=${secuencia//T/U}
echo $todas    # Resultado: AUCGAUCGAUCG
```

#### 🧬 Aplicación práctica: Conversión ADN → ARN
```bash
#!/bin/bash
# Convertir secuencia de ADN a ARN mensajero

echo "=== CONVERSIÓN ADN → ARN ==="

# Secuencia de ADN de ejemplo
adn_secuencia="AAACGCGGCCTTTCCAACGGC"
echo "ADN original: 5'-$adn_secuencia-3'"

# Convertir T → U para obtener ARN
arn_secuencia=${adn_secuencia//T/U}
echo "ARN mensajero: 5'-$arn_secuencia-3'"
```

#### 💻 Ejemplo: Cambiar formato de archivos
```bash
#!/bin/bash
# Cambiar extensiones de archivos

archivo="datos_genomicos.txt"
echo "Archivo original: $archivo"

# Cambiar .txt por .csv
archivo_csv=${archivo/txt/csv}
echo "Nuevo nombre: $archivo_csv"

# Para múltiples archivos (simulado)
archivos="gen1.fasta gen2.fasta gen3.fasta"
echo "Archivos originales: $archivos"

# Cambiar todas las extensiones .fasta por .fa
archivos_cortos=${archivos//fasta/fa}
echo "Archivos renombrados: $archivos_cortos"
```

---

## 🧪 Ejercicios paso a paso

### 💡 Ejercicio 1: Análisis básico de codones

```bash
#!/bin/bash
# Ejercicio: Analizar secuencia de codones

codones="AUG UAC GCU UAA GCA UAG"
echo "Secuencia de codones: $codones"
echo "Longitud total: ${#codones} caracteres"

echo ""
echo "=== EXTRACCIÓN DE PARTES ==="

# Extraer diferentes partes
echo "Desde posición 3: ${codones:3}"        # " UAC GCU UAA GCA UAG"
echo "Primeros 3 caracteres: ${codones:0:3}" # "AUG"  
echo "Desde posición 11: ${codones:11}"      # "U UAA GCA UAG"

# Caracteres desde el final
echo "Últimos 4 caracteres: ${codones: -4}"  # " UAG"
echo "Penúltimos 2: ${codones: -4:2}"       # " U"
```

**🤔 Pregunta para reflexionar:** ¿Por qué `${codones:11}` no muestra exactamente lo que esperamos?

### 💡 Ejercicio 2: Manipulación con patrones

```bash
#!/bin/bash
# Ejercicio: Trabajar con patrones

codones="AUG UAC GCU UAA GCA UAG"

echo "=== ELIMINACIÓN CON PATRONES ==="

# Eliminar desde el principio
echo "Eliminar hasta primera 'C': ${codones#*C}"   # "U UAA GCA UAG"
echo "Eliminar hasta última 'C': ${codones##*C}"   # "U UAA GCA UAG"

# Nota: En este caso, el resultado es igual porque solo hay una secuencia A*C
```

### 💡 Ejercicio 3: Reemplazos en secuencias

```bash
#!/bin/bash
# Ejercicio: Modificar codones

codones="AUG UAC GCU UAA GCA UAG"
echo "Secuencia original: $codones"

echo ""
echo "=== REEMPLAZOS ==="

# Reemplazar solo la primera ocurrencia
primer_remplazo=${codones/UA/CC}
echo "Cambiar primera UA por CC: $primer_remplazo"

# Reemplazar codón completo
cambio_codon=${codones//AUG/Met}
echo "AUG → Met: $cambio_codon"

# Cambiar todos los números
cambio_numeros=${codones//2/1}
echo "Cambiar 2 por 1: $cambio_numeros"
```

---

## 🧪 Proyecto: Traductor de codones

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

## 📝 Actividad Asincrónica

### 🎬 MISIÓN IMPOSIBLE: OPERACIÓN BIOINFORMÁTICA

```
🎵 *Música de Misión Imposible sonando de fondo* 🎵
```

---

#### 📼 MENSAJE SECRETO

```
Buenos días, Agente [TU NOMBRE].

Tu misión, si decides aceptarla, consiste en infiltrarte en el laboratorio 
de bioinformática de la Universidad UPC y completar una serie de tareas 
críticas para salvar el mundo de una amenaza biológica.

Un científico malvado ha alterado secuencias genéticas críticas y solo 
TÚ puedes restaurarlas usando tus habilidades en Shell Scripting.

Este mensaje se autodestruirá en 10 segundos... 💥

Buena suerte, Agente.
```

---

#### 🎯 BRIEFING DE LA MISIÓN

##### 📋 **INFORMACIÓN CLASIFICADA:**
- **Código de Operación:** SHELL-SCRIPT-007
- **Nivel de Amenaza:** 🔴 CRÍTICO
- **Tiempo límite:** 7 días
- **Equipo requerido:** Terminal Linux/Mac o WSL en Windows
- **Arma secreta:** Comandos de manipulación de texto en Bash

##### 🕵️ **TU IDENTIDAD ENCUBIERTA:**
- **Nombre en clave:** Agente Bioinformático
- **Especialidad:** Manipulación de secuencias genéticas
- **Misión:** Restaurar la estabilidad genética mundial

---

#### 🚨 MISIONES A COMPLETAR

### 🧬 **MISIÓN 1: OPERACIÓN "INSULIN RESCUE"**
**📍 Localización:** Laboratorio de Endocrinología

El villano Dr. Chaos ha alterado la secuencia de insulina humana. Debes crear un script que analice la secuencia comprometida.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision1_insulina.sh`
2. Incluir la secuencia de insulina alterada:
   ```
   MALWMRLLPLLALLALWGPDPAAAFVNQHLCGSHLVEALYLVCGERGFFYTPKTRREAEDLQVGQVELGGGPGAGSLQPLALEGSLQKRGIVEQCCTSICSLYQLENYCN
   ```
3. Tu script debe mostrar:
   - Un mensaje de bienvenida estilo "agente secreto"
   - La secuencia completa
   - La longitud total de la secuencia
   - Los primeros 10 aminoácidos (posible región comprometida)
   - Los últimos 10 aminoácidos

##### 📝 **Código de ejemplo para empezar:**

```bash
#!/bin/bash
# MISIÓN IMPOSIBLE - OPERACIÓN INSULIN RESCUE
# Agente: [TU NOMBRE]
# Fecha: [FECHA ACTUAL]

echo "🕵️ ACCESO CONCEDIDO - BIENVENIDO AGENTE"
echo "======================================="
echo "🚨 INICIANDO ANÁLISIS DE SECUENCIA COMPROMETIDA..."

# Tu código aquí...
```

---

#### 🧬 **MISIÓN 2: OPERACIÓN "DNA TO RNA CONVERSION"**
**📍 Localización:** Centro de Investigación Genética

El Dr. Chaos ha mezclado secuencias de ADN con ARN. Debes crear un programa que convierta ADN a ARN para identificar las secuencias correctas.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision2_conversion.sh`
2. Usar esta secuencia de ADN comprometida:
   ```
   AAACGCGGCCTTTCCAACGGC
   ```
3. Tu script debe:
   - Mostrar la secuencia de ADN original
   - Convertir todas las T por U (ADN → ARN)
   - Mostrar la secuencia de ARN resultante
   - Verificar que la conversión fue exitosa (contar T's en ADN y U's en ARN)

##### 🎪 **Diálogo dramático requerido:**
```bash
echo "🔬 INICIANDO PROTOCOLO DE CONVERSIÓN..."
echo "⚗️  Analizando secuencia de ADN infiltrada..."
echo "🧬 Ejecutando conversión molecular..."
echo "✅ MISIÓN COMPLETADA - ARN RECUPERADO"
```

---

#### 🧬 **MISIÓN 3: OPERACIÓN "CODON TRANSLATOR"**
**📍 Localización:** Departamento de Traducción Genética

El villano ha encriptado un mensaje usando codones. Debes decodificarlo.

##### 🎯 **Objetivos:**
1. Crear un script llamado `mision3_traductor.sh`
2. Usar esta secuencia de codones encriptada:
   ```
   AUG UAC GCU UAA GCA UAG
   ```
3. Tu script debe:
   - Mostrar los codones originales
   - Extraer el primer codón (AUG)
   - Extraer el último codón (UAG)
   - Reemplazar AUG por "INICIO"
   - Reemplazar UAG por "FIN"
   - Mostrar el mensaje decodificado

##### 🎭 **Elemento dramático:**
```bash
echo "🔐 DESENCRIPTANDO MENSAJE MOLECULAR..."
echo "🧩 Separando codones de la secuencia..."
echo "🔓 MENSAJE DECODIFICADO EXITOSAMENTE"
```

#### 📋 INFORME DE MISIÓN (ENTREGABLE)

##### 📝 **Debes entregar:**

1. **📁 Carpeta con tus 4 scripts:**
   - `mision1_insulina.sh`
   - `mision2_conversion.sh`
   - `mision3_traductor.sh`
   - `mision4_escaner.sh`

2. **📸 Capturas de pantalla mostrando:**
   - La ejecución de cada script
   - Los resultados obtenidos
   - El comando `ls -la` mostrando los permisos de ejecución

3. **📄 Reporte de agente (`informe_mision.txt`):**
   ```
   ================================
   INFORME DE MISIÓN CLASIFICADO
   ================================
   Agente: [TU NOMBRE]
   Fecha: [FECHA]
   Operación: SHELL-SCRIPT-007

   MISIÓN 1 - STATUS: [COMPLETADA/FALLIDA]
   Resultado: [Descripción de lo que hizo tu script]
   
   MISIÓN 2 - STATUS: [COMPLETADA/FALLIDA]
   Resultado: [Descripción de lo que hizo tu script]
   
   MISIÓN 3 - STATUS: [COMPLETADA/FALLIDA]
   Resultado: [Descripción de lo que hizo tu script]
   
   MISIÓN 4 - STATUS: [COMPLETADA/FALLIDA]
   Resultado: [Descripción de lo que hizo tu script]

   LECCIONES APRENDIDAS:
   - [¿Qué comandos nuevos aprendiste?]
   - [¿Qué dificultades tuviste?]
   - [¿Cómo los resolviste?]

   REFLEXIÓN FINAL:
   - [¿Cómo te ayudará esto en tu carrera como biólogo?]
   
   FIN DEL INFORME
   ================================
   ```
---

## 📚 Referencias bibliográficas

- Blum, R., & Bresnahan, C. (2021). Linux command line and Shell scripting bible (Fourth edition). Wiley. Capítulo 11.

---






