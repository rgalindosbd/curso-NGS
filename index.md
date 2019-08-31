![alt text](https://solariabiodata.com.mx/images/solaria_banner.png "Soluciones de Siguiente Generación")
# Curso de Análisis de Datos de NGS en GNU/Linux - Módulo 2

## Ejercicios de Sesión Práctica - Comandos de Linux

### Descripción
En este ejercicio veremos cómo usar algunos comandos útiles para la visualización de datos de NGS

### Requisitos

Para poder realizar este ejercicio, necesitaremos:

1. Datos de Secuenciación masiva:
  - Puedes usar el del presente repositorios
  - Puedes usar los que tengas
2. Acceso a una computadora con GNU/Linux


### 1.1 Visualizar el contenido de una carpeta

Usando este comando, observaremos el contenido de una carpeta en orden por modificación y en formato legible:

    ls -ltrh

### 1.2 Visualizar solo un tipo de extensión de archivo

Usando este comando, podemos ver formatos compatibles con el patrón de expresión regular respecto a la carpeta:

    ls -ltrh *fastq*

### 1.3 Visualizar Secuencias en la Terminal

Recordemos, que los comandos para ver parcialmente las secuencias pueden ser:

    cat *fastq* | less

### 1.4 Contar el número de secuencias

Si nuestro archivo está en formato FASTA:

    grep -c ">" secuencias.fasta

Si nuestro archivo es un FASTQ:

    grep -c "^@" libs.fastq

 Si nuestro archivo es un FASTQ.GZ:

    zgrep -c "^@" rawq.fastq.gz

### 1.5 Comprimir Secuencias de Secuenciación Masiva

Esta utilidad nos puede ahorrar espacio en disco:

    gzip -c libs.fastq > libs.fastq.gz

Para descomprimir, se utiliza:

    gunzip -d libs.fastq.gz

## Filtro de secuencias con Trimmomatic

### Descripción

En los presentes ejercicios, aprenderemos a utilizar Trimmomatic para hacer la remoción de secuencias de baja calidad.

### Requisitos

Para comprender cómo funciona Trimmomatic, debemos tener a consideración la estructura básica del comando:

    java -jar trimmomatic.jar  <SE | PE> <Secuencias de Entrada> <Prefijos de Salida> INSTRUCCIÓN_DE_FILTRADO

Las instrucciones que revisaremos, se encuentran desglosadas en el presente ejercicio. Ten la libertad de jugar con tus secuencias propias. Si tienes dificultades para teclear el comando completo, puedes copiar y pegar las instrucciones en tu terminal.

### 2.1 Remoción de Adaptadores de Secuenciación

Teclear lo siguiente:

    Trimmomatic SE raw_01_R1.fastq.gz trimmed_01_R1.fastq.gz ILLUMINACLIP:adapters.fa:2:30:10


### 2.2 Cortes Fijos de Librerías

Este comando realiza cortes fijos en el inicio de todas las secuencias. Teclear lo siguiente:

    Trimmomatic SE raw_01_R1.fastq.gz headcrop_01_R1.fastq.gz HEADCROP:<bases>

Este comando realiza cortes fijos en el final de todas las secuencias. Teclear lo siguiente:

    Trimmomatic SE raw_01_R1.fastq.gz crop_01_R1.fastq.gz CROP:<bases>

### 2.3 Trimming por método de Ventana Deslizante

Este comando realiza la búsqueda por ventana. Teclear lo siguiente:

    Trimmomatic SE raw_01_R1.fastq.gz sliding_01_R1.fastq.gz SLIDINGWINDOW:<tamaño de ventana>:<calidad>


### 2.4 Trimming de secuencias con un mínimo de tamaño

    Trimmomatic SE raw_01_R1.fastq.gz minlen_01_R1.fastq.gz MINLEN:<tamaño mínimo>

### 2.5 Filtro por Media de Calida

Este comando realiza la remoción desde el principio de las Secuencias:

    Trimmomatic SE raw_01_R1.fastq.gz leading_01_R1.fastq.gz LEADING:10

Este comando realiza la remoción a partir del final de las secuencias:

    Trimmomatic SE raw_01_R1.fastq.gz trailing_01_R1.fastq.gz TRAILING:10

### 2.6 Trimming de Secuencias Pareadas

Teclear lo siguiente:

    Trimmomatic PE raw_01_R1.fastq.gz raw_01_R2.fastq.gz paired_01_R1.fq.gz unpaired_01_R1.fq.gz paired_01_R2.fq.gz unpaired_01_R2.fq.gz ILLUMINACLIP:TruSeq3-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:25 MINLEN:50
