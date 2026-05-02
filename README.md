# Semana 05: Ensamblaje de genomas

## Logro de la sesión: 

Al finalizar la sesión, el estudiante utiliza herramientas bioinformaticas para obtener un genoma ensamblado y evaluar su integridad.

# Estructura de la práctica:

1. Acceso al servidor de cómputo
2. Ensamblaje de genomas de datos de secuenciación Illumina
3. Ensamblaje de genomas de datos de secuenciación Nanopore
4. Obtención de las metricas de los genomas ensamblados
5. Clasificación taxonómica a nivel de género en base a la secuencia 16S
6. Validación de los genomas ensamblados
7. Clasificación taxonómica a nivel de especie mediante ANI (Average Nucleotide Identity)
8.	Ensamblaje del genoma de los datos de secuenciación Nanopore generados en el curso

## Programas requeridos:

### Programas de acceso al servidor:

PuTTY v0.79 https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
   - **Descripción:** PuTTY es un cliente SSH, Telnet y Rlogin gratuito y de código abierto para Windows y sistemas Unix. Se utiliza principalmente para establecer conexiones seguras de línea de comandos a servidores remotos.

WinSCP v6.1 https://winscp.net/eng/download.php
   - **Descripción:** WinSCP es un cliente SFTP, FTP, WebDAV, Amazon S3 y SCP gratuito y de código abierto para Windows. Permite la transferencia segura de archivos entre un ordenador local y servidores remotos mediante una interfaz gráfica de usuario. 

### Programas bioinformáticos:

Bandage v0.8.1 http://rrwick.github.io/Bandage/
   - **Descripción:** Bandage es una herramienta para visualizar grafos de ensamblaje de genomas. Permite explorar las relaciones entre los contigs (fragmentos de ADN ensamblados) y puede ayudar a identificar problemas en el ensamblaje, como colapsos de repeticiones o errores. Su nombre es un acrónimo de "Bandage is a nice de novo assembly graph explorer".

Barrnap v0.9 https://github.com/tseemann/barrnap
   - **Descripción:** Barrnap (Bacterial rRNA prediction program) es un programa que predice las secuencias de ARN ribosomal (rRNA) en genomas bacterianos y arqueales. La identificación de los genes de rRNA es importante para estudios filogenéticos y metagenómicos.

CheckM v1.2.2 https://ecogenomics.github.io/CheckM/
   - **Descripción:** CheckM es una herramienta que evalúa la calidad de los metagenomas ensamblados y de los genomas ensamblados a partir de metagenomas (MAGs). Proporciona estimaciones de completitud y contaminación basadas en marcadores genéticos.

Flye v2.9.2 https://github.com/fenderglass/Flye/
   - **Descripción:** Flye es un ensamblador de novo enfocado en lecturas largas. Se destaca por su velocidad y eficiencia en el uso de memoria, lo que lo hace adecuado para ensamblar genomas grandes en recursos computacionales limitados.

Minimap2 v2.29.0 https://github.com/lh3/minimap2
   - **Descripción:** es un alineador de secuencias rápido y versátil diseñado para alinear secuencias largas de ADN o ARN, como lecturas de Nanopore y PacBio contra genomas de referencia o ensamblajes, así como lecturas largas entre sí para el ensamblaje de novo y lecturas cortas contra genomas; se destaca por su velocidad, sensibilidad robusta frente a errores en lecturas largas, su formato de salida PAF y una amplia gama de opciones de personalización mediante indexación eficiente basada en minimizadores, siendo una herramienta fundamental para diversas tareas de análisis genómico.

Quast v5.2.0 http://quast.sourceforge.net/
   - **Descripción:** QUAST (Quality Assessment Tool for Genome Assemblies) es una herramienta que calcula una amplia variedad de métricas para evaluar la calidad de los ensamblajes de genomas. Proporciona estadísticas detalladas sobre la contigüidad, la precisión y la completitud del ensamblaje.

Racon v1.5.0 https://github.com/lbcb-sci/racon
   - **Descripción:** Racon es una herramienta para el pulido (polishing) de ensamblajes de genomas, especialmente aquellos generados a partir de lecturas largas. Utiliza las lecturas originales para corregir errores y mejorar la precisión del ensamblaje final.

Unicycler v0.5.1 https://github.com/rrwick/Unicycler
   - **Descripción:** Unicycler es una herramienta bioinformática de código abierto diseñada para ensamblar genomas bacterianos (y otros genomas pequeños) a partir de datos de secuenciación. Su principal fortaleza radica en su capacidad para manejar conjuntos de datos híbridos, que combinan lecturas cortas y precisas (como las de Illumina) con lecturas largas que abarcan más distancia (como las de Oxford Nanopore o PacBio). Al aprovechar las ventajas de ambos tipos de datos, Unicycler puede generar ensamblajes más completos y contiguos, especialmente en regiones complejas como repeticiones.
     
### Herramientas bioinformáticas en línea:

16S-based ID https://www.ezbiocloud.net/identify
   - **Descripción:** Esta es una herramienta en línea proporcionada por EzBioCloud que permite la identificación taxonómica de bacterias y arqueas basada en la secuencia del gen 16S rRNA, un marcador molecular comúnmente utilizado en estudios de diversidad microbiana.

blastn https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&BLAST_SPEC=GeoBlast&PAGE_TYPE=BlastSearch
   - **Descripción:** BLASTn (Basic Local Alignment Search Tool - nucleotide) es una herramienta en línea del NCBI (National Center for Biotechnology Information) que permite buscar secuencias de nucleótidos (ADN o ARN) contra bases de datos de secuencias de nucleótidos. Encuentra regiones de similitud local entre tu secuencia de consulta y las secuencias en la base de datos, lo que te permite identificar secuencias relacionadas o similares. 

## Metodología:

## 1.	Acceso al servidor de cómputo:

### Abrir el programa PuTTY, colocar el hostname ( 10.142.250.66 ) y port ( 22 ), y dar clic en Open:

<img width="500" alt="image" src="https://github.com/user-attachments/assets/92f89dbb-1a21-411d-adb5-38fe486a5567" />



### En la terminal abierta, escribir su usuario y contraseña correspondiente para tener acceso al servidor de cómputo Tensor:
 
<img width="700" alt="image" src="https://github.com/user-attachments/assets/4d246e93-c59c-4749-a2dd-03db25c53654" />



### Abrir el programa WinSCP, colocar el hostname ( 10.142.250.66 ) y port ( 22 ), escribir su usuario y contraseña correspondiente para tener acceso al servidor de cómputo Tensor, y hacer clic en Login:

<img width="500" alt="image" src="https://github.com/user-attachments/assets/ef4dc253-ce4a-417d-b761-39692d2a011a" />

<img width="500" alt="image" src="https://github.com/user-attachments/assets/577debca-6085-47c5-9bbd-73688bfa8bb0" />


## 2. Ensamblaje de genomas de datos de secuenciación Illumina

### Crear los directorios assembly e illumina

```bash
cd ~/genomics

mkdir assembly

cd assembly

mkdir illumina

cd illumina
```

### Ensamblaje de novo del genoma con unicycler

```bash
conda activate unicycler

unicycler -t 10 --kmers 21,51,71,91,111 -1 /data/2025_1/database/illumina/SRR19551969_R1.trim.fastq.gz -2 /data/2025_1/database/illumina/SRR19551969_R2.trim.fastq.gz -o m01_unicycler_illumina
```

> **Comentario:** 
> - `-t 10`: Estás pidiendo a Unicycler que utilice hasta 10 hilos (núcleos de CPU) para el proceso de ensamblaje. Esto puede ayudar a acelerar las cosas.
> - `--kmers 21,51,71,91,111`: Esta opción proporciona una estimación del tamaño del genoma que se va a ensamblar. Estás proporcionando una lista específica de tamaños de k-meros para que Unicycler los utilice. Los k-meros son secuencias cortas de ADN que se utilizan en el proceso de ensamblaje. Proporcionar un rango de k-meros a veces puede mejorar la calidad del ensamblaje, especialmente para genomas complejos.
> - `-1 /data/2025_1/database/illumina/SRR19551969_R1.trim.fastq.gz`: Esto especifica la ruta a tu primer archivo de lectura de extremo pareado (forward) en formato FASTQ (que también ha sido recortado). La extensión .gz indica que es un archivo comprimido con gzip, que Unicycler puede manejar directamente.
> - `-2 /data/2025_1/database/illumina/SRR19551969_R2.trim.fastq.gz`: Esto especifica la ruta a tu segundo archivo de lectura de extremo pareado (reverse), también en formato FASTQ recortado y comprimido con gzip.
> - `-o m01_unicycler_illumina`: Esto le dice a Unicycler que cree un nuevo directorio de salida llamado m01_unicycler_illumina donde se almacenarán todos los resultados del ensamblaje.

### Cambiar los nombres a los archivos .fasta y .gfa

```bash
mv m01_unicycler_illumina/assembly.fasta m01_unicycler.fasta

mv m01_unicycler_illumina/assembly.gfa m01_unicycler.gfa
```

### Exportar y visualizar el archivo .gfa en el programa bandage

## 3. Ensamblaje de genomas de datos de secuenciación Nanopore

### Crear el directorio nanopore

```bash
cd ~/genomics/assembly

mkdir nanopore

cd nanopore
```

### Ensamblaje de novo del genoma con unicycler

```bash
conda activate unicycler

unicycler -t 10 -l /data/2025_1/database/nanopore/fastq/m01_trim.fastq.gz -o m01_unicycler_nanopore
```

> **Comentario:** 
> - `-l`: Especifica la ruta hacia tus lecturas largas (Nanopore o PacBio).

```bash
grep ">" m01_unicycler_nanopore/assembly.fasta 
>1
>2
>3
```

```bash
tail -n 20 m01_unicycler_nanopore/unicycler.log

Saving /data/fguzman/m01_genome/assembly/m01_unicycler_nanopore/miniasm_assembly/13_racon_polished.gfa
Saving /data/fguzman/m01_genome/assembly/m01_unicycler_nanopore/003_racon_polished.gfa

Rotating completed replicons (2026-05-02 08:55:31)
--------------------------------------------------
    Any completed circular contigs (i.e. single contigs which have one link connecting end to start) can have their start position changed without altering the sequence. For consistency, Unicycler now searches for a starting gene (dnaA or repA) in each such contig, and if one is found, the contig is rotated to start with that gene on the forward strand.

Segment   Length      Depth   Starting gene         Position    Strand    Identity   Coverage
      1   4,872,717   1.00x   UniRef90_Q8XBZ3       1,233,907   reverse      93.8%     100.0%
      2     133,133   1.16x   UniRef90_A0A0F4AY34      98,723   reverse      99.1%     100.0%
      3       6,862   0.98x   none found                                                     

Saving /data/fguzman/m01_genome/assembly/m01_unicycler_nanopore/004_rotated.gfa


Assembly complete (2026-05-02 08:57:15)
---------------------------------------
Saving /data/fguzman/m01_genome/assembly/m01_unicycler_nanopore/assembly.gfa
```

### Cambiar los nombres a los archivos .fasta y .gfa 

```bash
mv m01_unicycler_nanopore/assembly.fasta m01_unicycler.fasta

mv m01_unicycler_nanopore/assembly.gfa m01_unicycler.gfa
```

### Exportar y visualizar el archivo .gfa en el programa bandage

<img width="3014" height="1737" alt="image" src="https://github.com/user-attachments/assets/98a2151b-9785-4613-a1c7-1daee187b70e" />

### Ensamblaje de novo del genoma con flye

```bash
conda activate shotgun

flye --nano-hq /data/2025_1/database/nanopore/fastq/m01_trim.fastq.gz --threads 10 --genome-size 5m --out-dir m01_flye_nanopore
```

> **Comentario:** 
> - `--nano-hq`: Indica que las lecturas son datos de Nanopore del tipo R10. 
> - `--genome-size 5m`: Esta opción proporciona una estimación del tamaño del genoma que se va a ensamblar.

```bash
tail -n 20 m01_flye_nanopore/flye.log

[2026-05-02 08:53:07] root: DEBUG:         4.0 M       contigs.fasta
[2026-05-02 08:53:07] root: DEBUG:         84.0 B      contigs.fasta.fai
[2026-05-02 08:53:07] root: DEBUG:         0.0 B       scaffolds_links.txt
[2026-05-02 08:53:07] root: DEBUG:         4.0 M       graph_final.fasta
[2026-05-02 08:53:07] root: DEBUG:         425.0 B     graph_final.gv
[2026-05-02 08:53:07] root: DEBUG:     10-consensus/
[2026-05-02 08:53:07] root: DEBUG:         958.0 B     minimap.stderr
[2026-05-02 08:53:07] root: DEBUG:         4.0 M       consensus.fasta
[2026-05-02 08:53:07] root: DEBUG:         265.0 K     minimap.bam.bai
[2026-05-02 08:53:07] root: DEBUG: --------------------------
[2026-05-02 08:53:07] root: INFO: Assembly statistics:

        Total length:   5012708
        Fragments:      3
        Fragments N50:  4872715
        Largest frg:    4872715
        Scaffolds:      0
        Mean coverage:  157

[2026-05-02 08:53:07] root: INFO: Final assembly: /data/fguzman/m01_genome/assembly/m01_flye_nanopore/assembly.fasta
```

```bash
cat m01_flye_nanopore/assembly_info.txt 

#seq_name       length  cov.    circ.   repeat  mult.   alt_group       graph_path
contig_1        4872715 157     Y       N       1       *       1
contig_2        133133  180     Y       N       1       *       2
contig_3        6860    153     Y       N       1       *       3
```

> **Comentario:** 
> - `seq_name`: El identificador del contig. En este caso, contig_1, contig_3, contig_4 y contig_2.
> - `length`: La longitud de cada contig en bases.
> - `cov.`: La profundidad estimada para cada contig, que indica cuántas veces, en promedio, cada base del contig fue cubierta por las lecturas de entrada. Una profundidad más alta generalmente indica una mayor confianza en la secuencia del contig.
> - `circ.`: Indica si el contig se predice que es circular (Y para sí, N para no).
> - `repeat`: Indica si el contig se identificó como una región repetitiva (Y para sí, N para no).
> - `mult.`: Un factor que indica la multiplicidad estimada de la secuencia en el genoma. Un valor de 1 sugiere una única copia, mientras que valores mayores indican posibles repeticiones.
> - `alt_group`: Identifica grupos de contigs que representan posibles ensamblajes alternativos de la misma región genómica. Un * indica que no pertenece a ningún grupo alternativo.
Todos los contigs tienen *, lo que sugiere que Flye no identificó ensamblajes alternativos significativos para estas regiones.
> - `graph_path`: El índice del camino en el grafo de ensamblaje que corresponde a este contig.

```bash
grep ">" m01_flye_nanopore/assembly.fasta

>contig_1
>contig_2
>contig_3
```
### Cambiar los nombres a los archivos .fasta y .gfa 

```bash
mv m01_flye_nanopore/assembly.fasta m01_flye.fasta

mv m01_flye_nanopore/assembly_graph.gfa m01_flye.gfa
```

### Exportar y visualizar el archivo .gfa en el programa bandage

<img width="3021" height="1783" alt="image" src="https://github.com/user-attachments/assets/fa0f690d-5f27-478f-bc5e-1fcdbd19466d" />

## 4. Obtención de las metricas de los genomas ensamblados

### Crear el directorio validation

```bash
cd ~/genomics/

mkdir validation

cd validation
```

### Calculo de las metricas de los genomas ensamblados

```bash
quast.py -m 1000 -o m01_quast ~/genomics/assembly/nanopore/m01_flye.fasta ~/genomics/assembly/nanopore/m01_unicycler.fasta
```

> **Comentario:** 
> - `-m 1000`: Esta opción establece la longitud mínima de contig para ser considerada en la evaluación a 1000 pares de bases. Solo los contigs que tengan al menos 1000 pares de bases de longitud se incluirán en el análisis. Esto filtra contigs cortos y potencialmente poco fiables.

```bash
cat m01_quast/report.txt

All statistics are based on contigs of size >= 1000 bp, unless otherwise noted (e.g., "# contigs (>= 0 bp)" and "Total length (>= 0 bp)" include all contigs).

Assembly                    m01_flye   m01_unicycler
# contigs (>= 0 bp)         3          3            
# contigs (>= 1000 bp)      3          3            
# contigs (>= 5000 bp)      3          3            
# contigs (>= 10000 bp)     2          2            
# contigs (>= 25000 bp)     2          2            
# contigs (>= 50000 bp)     2          2            
Total length (>= 0 bp)      5012708    5012712      
Total length (>= 1000 bp)   5012708    5012712      
Total length (>= 5000 bp)   5012708    5012712      
Total length (>= 10000 bp)  5005848    5005850      
Total length (>= 25000 bp)  5005848    5005850      
Total length (>= 50000 bp)  5005848    5005850      
# contigs                   3          3            
Largest contig              4872715    4872717      
Total length                5012708    5012712      
GC (%)                      55.30      55.30        
N50                         4872715    4872717      
N90                         4872715    4872717      
auN                         4740177.0  4740177.1    
L50                         1          1            
L90                         1          1            
# N's per 100 kbp           0.00       0.00         
```

> **Comentario:** 
> - `contigs (>= X bp)`: Número de contigs mayores o iguales a X pares de bases. Esta métrica indica cuántas secuencias contiguas (contigs) tiene tu ensamblaje que cumplen con una longitud mínima específica (X). QUAST reporta esto para varios umbrales de longitud (0 bp, 1000 bp, 5000 bp, etc.). Un número menor de contigs más largos generalmente se considera un mejor ensamblaje, ya que indica una mayor contigüidad (menos fragmentación).
> - `Total length (>= X bp)`: Longitud total de los contigs mayores o iguales a X pares de bases. Similar a la métrica anterior, pero en lugar de contar, suma la longitud de todos los contigs que cumplen con el umbral de longitud especificado. La longitud total del ensamblaje debería ser cercana al tamaño esperado del genoma.
> - `contigs`: Este es el número total de contigs en el ensamblaje que tienen al menos 1000 pares de bases de longitud (esta es la convención predeterminada de QUAST para esta métrica).
> - `Largest contig`: La longitud del contig más largo en el ensamblaje. Un contig más largo es deseable, ya que sugiere que se han podido resolver regiones más complejas del genoma en una sola pieza.
> - `Total length`: La suma de las longitudes de todos los contigs en el ensamblaje que tienen al menos 1000 pares de bases de longitud (nuevamente, el comportamiento predeterminado de QUAST para esta métrica).
> - `GC (%)`: El porcentaje de bases guanina (G) y citosina (C) en el ensamblaje. Este valor suele ser característico de la especie o linaje que se está secuenciando y puede utilizarse para verificar la consistencia con otros ensamblajes o datos conocidos.
> - `N50`: Esta es una métrica clave para evaluar la contigüidad de un ensamblaje. Se define como la longitud del contig más corto en el conjunto de contigs cuya longitud acumulada representa al menos el 50% del tamaño total del ensamblaje. Un N50 más alto indica que una porción significativa del ensamblaje está contenida en contigs más largos, lo cual es generalmente mejor. Para entenderlo mejor: imagina ordenar todos tus contigs de mayor a menor longitud. El N50 es la longitud del contig en el punto donde, al sumar las longitudes de los contigs desde el más largo, alcanzas o superas la mitad del tamaño total del ensamblaje.
> - `L50`: El número de contigs cuya longitud es mayor o igual al N50. Un L50 más bajo es mejor, ya que significa que se necesita un número menor de contigs para alcanzar el 50% del tamaño del ensamblaje.
> - `N's per 100 kbp`: La cantidad de bases 'N' (que representan bases desconocidas o ambiguas) en el ensamblaje, normalizada por cada 100,000 pares de bases. Un valor más bajo es mejor, ya que indica una mayor resolución de la secuencia.

## 5. Clasificación taxonómica a nivel de género en base a la secuencia 16S

### Crear el directorio taxonomy

```bash
cd ~/genomics/

mkdir taxonomy

cd taxonomy
```

### Identificación de las secuencias de rRNA

```bash
conda activate genome

barrnap ~/genomics/assembly/nanopore/m01_flye.fasta --threads 10 --outseq m01_rna.fasta
```

```bash
grep ">" m01_rna.fasta

>16S_rRNA::contig_1:1506039-1507577(+)
>16S_rRNA::contig_1:1106359-1107897(-)
>16S_rRNA::contig_1:1613691-1615229(+)
>16S_rRNA::contig_1:1217311-1218849(-)
>16S_rRNA::contig_1:3458-4996(-)
>16S_rRNA::contig_1:1026393-1027929(-)
>16S_rRNA::contig_1:2122113-2123649(+)
>16S_rRNA::contig_1:784699-786237(-)
>23S_rRNA::contig_1:2124163-2127065(+)
>23S_rRNA::contig_1:199-3102(-)
>23S_rRNA::contig_1:1615585-1618487(+)
>23S_rRNA::contig_1:781440-784343(-)
>23S_rRNA::contig_1:1103010-1105912(-)
>23S_rRNA::contig_1:1214053-1216955(-)
>23S_rRNA::contig_1:1507788-1510691(+)
>23S_rRNA::contig_1:1023044-1025946(-)
>5S_rRNA::contig_1:781005-781116(-)
>5S_rRNA::contig_1:1510766-1510877(+)
>5S_rRNA::contig_1:1618566-1618677(+)
>5S_rRNA::contig_1:2127143-2127254(+)
>5S_rRNA::contig_1:9-120(-)
>5S_rRNA::contig_1:781254-781365(-)
>5S_rRNA::contig_1:1022858-1022969(-)
>5S_rRNA::contig_1:1102820-1102931(-)
>5S_rRNA::contig_1:1213863-1213974(-)
```

```bash
head -n 10 m01_rna.fasta

>16S_rRNA::contig_1:1506039-1507577(+)
TTGAAGAGTTTGATCATGGCTCAGATTGAACGCTGGCGGCAGGCCTAACACATGCAAGTCGAGCGGCAGCGGGAAGTAGCTTGCTACTTTGCCGGCGAGCGGCGGACGGGTGAGTAATGTCTGGGAAACTGCCTGATGGAGGGGGATAACTACTGGAAACGGTAGCTAATACCGCATAATGTCGCAAGACCAAAGAGGGGGACCTTCGGGCCTCTTGCCATCAGATGTGCCCAGATGGGATTAGCTAGTAGGTGGGGTAATGGCTCACCTAGGCGACGATCCCTAGCTGGTCTGAGAGGATGACCAGCCACACTGGAACTGAGACACGGTCCAGACTCCTACGGGAGGCAGCAGTGGGGAATATTGCACAATGGGCGCAAGCCTGATGCAGCCATGCCGCGTGTATGAAGAAGGCCTTCGGGTTGTAAAGTACTTTCAGCGGGGAGGAAGGTGCTGAGGTTAATAACCTCAGCAATTGACGTTACCCGCAGAAGAAGCACCGGCTAACTCCGTGCCAGCAGCCGCGGTAATACGGAGGGTGCAAGCGTTAATCGGAATTACTGGGCGTAAAGCGCACGCAGGCGGTCTGTCAAGTCGGATGTGAAATCCCCGGGCTCAACCTGGGAACTGCATTCGAAACTGGCAGGCTAGAGTCTTGTAGAGGGGGGTAGAATTCCAGGTGTAGCGGTGAAATGCGTAGAGATCTGGAGGAATACCGGTGGCGAAGGCGGCCCCCTGGACAAAGACTGACGCTCAGGTGCGAAAGCGTGGGGAGCAAACAGGATTAGATACCCTGGTAGTCCACGCCGTAAACGATGTCGACTTGGAGGTTGTGCCCTTGAGGCGTGGCTTCCGGAGCTAACGCGTTAAGTCGACCGCCTGGGGAGTACGGCCGCAAGGTTAAAACTCAAATGAATTGACGGGGGCCCGCACAAGCGGTGGAGCATGTGGTTTAATTCGATGCAACGCGAAGAACCTTACCTACTCTTGACATCCAGAGAACTTTCCAGAGATGGATTGGTGCCTTCGGGAACTCTGAGACAGGTGCTGCATGGCTGTCGTCAGCTCGTGTTGTGAAATGTTGGGTTAAGTCCCGCAACGAGCGCAACCCTTATCCTTTGTTGCCAGCGGTTCGGCCGGGAACTCAAAGGAGACTGCCAGTGATAAACTGGAGGAAGGTGGGGATGACGTCAAGTCATCATGGCCCTTACGAGTAGGGCTACACACGTGCTACAATGGCGCATACAAAGAGAAGCGACCTCGCGAGAGCAAGCGGACCTCATAAAGTGCGTCGTAGTCCGGATTGGAGTCTGCAACTCGACTCCATGAAGTCGGAATCGCTAGTAATCGTAGATCAGAATGCTACGGTGAATACGTTCCCGGGCCTTGTACACACCGCCCGTCACACCATGGGAGTGGGTTGCAAAAGAAGTAGGTAGCTTAACCTTCGGGAGGGCGCTTACCACTTTGTGATTCATGACTGGGGTGAAGTCGTAACAAGGTAACCGTAGGGGAACCTGCGGTTGGATCACCTCCTT
>16S_rRNA::contig_1:1106359-1107897(-)
TTGAAGAGTTTGATCATGGCTCAGATTGAACGCTGGCGGCAGGCCTAACACATGCAAGTCGAGCGGCAGCGGGAAGTAGCTTGCTACTTTGCCGGCGAGCGGCGGACGGGTGAGTAATGTCTGGGAAACTGCCTGATGGAGGGGGATAACTACTGGAAACGGTAGCTAATACCGCATAATGTCGCAAGACCAAAGAGGGGGACCTTCGGGCCTCTTGCCATCAGATGTGCCCAGATGGGATTAGCTAGTAGGTGGGGTAATGGCTCACCTAGGCGACGATCCCTAGCTGGTCTGAGAGGATGACCAGCCACACTGGAACTGAGACACGGTCCAGACTCCTACGGGAGGCAGCAGTGGGGAATATTGCACAATGGGCGCAAGCCTGATGCAGCCATGCCGCGTGTATGAAGAAGGCCTTCGGGTTGTAAAGTACTTTCAGCGGGGAGGAAGGTGCTGAGGTTAATAACCTCAGCAATTGACGTTACCCGCAGAAGAAGCACCGGCTAACTCCGTGCCAGCAGCCGCGGTAATACGGAGGGTGCAAGCGTTAATCGGAATTACTGGGCGTAAAGCGCACGCAGGCGGTCTGTCAAGTCGGATGTGAAATCCCCGGGCTCAACCTGGGAACTGCATTCGAAACTGGCAGGCTAGAGTCTTGTAGAGGGGGGTAGAATTCCAGGTGTAGCGGTGAAATGCGTAGAGATCTGGAGGAATACCGGTGGCGAAGGCGGCCCCCTGGACAAAGACTGACGCTCAGGTGCGAAAGCGTGGGGAGCAAACAGGATTAGATACCCTGGTAGTCCACGCCGTAAACGATGTCGACTTGGAGGTTGTGCCCTTGAGGCGTGGCTTCCGGAGCTAACGCGTTAAGTCGACCGCCTGGGGAGTACGGCCGCAAGGTTAAAACTCAAATGAATTGACGGGGGCCCGCACAAGCGGTGGAGCATGTGGTTTAATTCGATGCAACGCGAAGAACCTTACCTACTCTTGACATCCAGAGAACTTTCCAGAGATGGATTGGTGCCTTCGGGAACTCTGAGACAGGTGCTGCATGGCTGTCGTCAGCTCGTGTTGTGAAATGTTGGGTTAAGTCCCGCAACGAGCGCAACCCTTATCCTTTGTTGCCAGCGGTTCGGCCGGGAACTCAAAGGAGACTGCCAGTGATAAACTGGAGGAAGGTGGGGATGACGTCAAGTCATCATGGCCCTTACGAGTAGGGCTACACACGTGCTACAATGGCGCATACAAAGAGAAGCGACCTCGCGAGAGCAAGCGGACCTCATAAAGTGCGTCGTAGTCCGGATTGGAGTCTGCAACTCGACTCCATGAAGTCGGAATCGCTAGTAATCGTAGATCAGAATGCTACGGTGAATACGTTCCCGGGCCTTGTACACACCGCCCGTCACACCATGGGAGTGGGTTGCAAAAGAAGTAGGTAGCTTAACCTTCGGGAGGGCGCTTACCACTTTGTGATTCATGACTGGGGTGAAGTCGTAACAAGGTAACCGTAGGGGAACCTGCGGTTGGATCACCTCCTT
>16S_rRNA::contig_1:1613691-1615229(+)
TTGAAGAGTTTGATCATGGCTCAGATTGAACGCTGGCGGCAGGCCTAACACATGCAAGTCGAGCGGCAGCGGGAAGTAGCTTGCTACTTTGCCGGCGAGCGGCGGACGGGTGAGTAATGTCTGGGAAACTGCCTGATGGAGGGGGATAACTACTGGAAACGGTAGCTAATACCGCATAACGTCGCAAGACCAAAGAGGGGGACCTTCGGGCCTCTTGCCATCAGATGTGCCCAGATGGGATTAGCTAGTAGGTGGGGTAACGGCTCACCTAGGCGACGATCCCTAGCTGGTCTGAGAGGATGACCAGCCACACTGGAACTGAGACACGGTCCAGACTCCTACGGGAGGCAGCAGTGGGGAATATTGCACAATGGGCGCAAGCCTGATGCAGCCATGCCGCGTGTATGAAGAAGGCCTTCGGGTTGTAAAGTACTTTCAGCGGGGAGGAAGGTGTTGAGGTTAATAACCTCAGCAATTGACGTTACCCGCAGAAGAAGCACCGGCTAACTCCGTGCCAGCAGCCGCGGTAATACGGAGGGTGCAAGCGTTAATCGGAATTACTGGGCGTAAAGCGCACGCAGGCGGTCTGTCAAGTCGGATGTGAAATCCCCGGGCTCAACCTGGGAACTGCATTCGAAACTGGCAGGCTAGAGTCTTGTAGAGGGGGGTAGAATTCCAGGTGTAGCGGTGAAATGCGTAGAGATCTGGAGGAATACCGGTGGCGAAGGCGGCCCCCTGGACAAAGACTGACGCTCAGGTGCGAAAGCGTGGGGAGCAAACAGGATTAGATACCCTGGTAGTCCACGCCGTAAACGATGTCGACTTGGAGGTTGTGCCCTTGAGGCGTGGCTTCCGGAGCTAACGCGTTAAGTCGACCGCCTGGGGAGTACGGCCGCAAGGTTAAAACTCAAATGAATTGACGGGGGCCCGCACAAGCGGTGGAGCATGTGGTTTAATTCGATGCAACGCGAAGAACCTTACCTACTCTTGACATCCAGAGAACTTTCCAGAGATGGATTGGTGCCTTCGGGAACTCTGAGACAGGTGCTGCATGGCTGTCGTCAGCTCGTGTTGTGAAATGTTGGGTTAAGTCCCGCAACGAGCGCAACCCTTATCCTTTGTTGCCAGCGGTTCGGCCGGGAACTCAAAGGAGACTGCCAGTGATAAACTGGAGGAAGGTGGGGATGACGTCAAGTCATCATGGCCCTTACGAGTAGGGCTACACACGTGCTACAATGGCGCATACAAAGAGAAGCGACCTCGCGAGAGCAAGCGGACCTCATAAAGTGCGTCGTAGTCCGGATTGGAGTCTGCAACTCGACTCCATGAAGTCGGAATCGCTAGTAATCGTAGATCAGAATGCTACGGTGAATACGTTCCCGGGCCTTGTACACACCGCCCGTCACACCATGGGAGTGGGTTGCAAAAGAAGTAGGTAGCTTAACCTTCGGGAGGGCGCTTACCACTTTGTGATTCATGACTGGGGTGAAGTCGTAACAAGGTAACCGTAGGGGAACCTGCGGTTGGATCACCTCCTT
>16S_rRNA::contig_1:1217311-1218849(-)
TTGAAGAGTTTGATCATGGCTCAGATTGAACGCTGGCGGCAGGCCTAACACATGCAAGTCGAGCGGCAGCGGGAAGTAGCTTGCTACTTTGCCGGCGAGCGGCGGACGGGTGAGTAATGTCTGGGAAACTGCCTGATGGAGGGGGATAACTACTGGAAACGGTAGCTAATACCGCATAACGTCGCAAGACCAAAGAGGGGGACCTTCGGGCCTCTTGCCATCAGATGTGCCCAGATGGGATTAGCTAGTAGGTGGGGTAACGGCTCACCTAGGCGACGATCCCTAGCTGGTCTGAGAGGATGACCAGCCACACTGGAACTGAGACACGGTCCAGACTCCTACGGGAGGCAGCAGTGGGGAATATTGCACAATGGGCGCAAGCCTGATGCAGCCATGCCGCGTGTATGAAGAAGGCCTTCGGGTTGTAAAGTACTTTCAGCGGGGAGGAAGGTGCTGAGGTTAATAACCTCAGCAATTGACGTTACCCGCAGAAGAAGCACCGGCTAACTCCGTGCCAGCAGCCGCGGTAATACGGAGGGTGCAAGCGTTAATCGGAATTACTGGGCGTAAAGCGCACGCAGGCGGTCTGTCAAGTCGGATGTGAAATCCCCGGGCTCAACCTGGGAACTGCATTCGAAACTGGCAGGCTAGAGTCTTGTAGAGGGGGGTAGAATTCCAGGTGTAGCGGTGAAATGCGTAGAGATCTGGAGGAATACCGGTGGCGAAGGCGGCCCCCTGGACAAAGACTGACGCTCAGGTGCGAAAGCGTGGGGAGCAAACAGGATTAGATACCCTGGTAGTCCACGCCGTAAACGATGTCGACTTGGAGGTTGTGCCCTTGAGGCGTGGCTTCCGGAGCTAACGCGTTAAGTCGACCGCCTGGGGAGTACGGCCGCAAGGTTAAAACTCAAATGAATTGACGGGGGCCCGCACAAGCGGTGGAGCATGTGGTTTAATTCGATGCAACGCGAAGAACCTTACCTACTCTTGACATCCAGAGAACTTTCCAGAGATGGATTGGTGCCTTCGGGAACTCTGAGACAGGTGCTGCATGGCTGTCGTCAGCTCGTGTTGTGAAATGTTGGGTTAAGTCCCGCAACGAGCGCAACCCTTATCCTTTGTTGCCAGCGGTTCGGCCGGGAACTCAAAGGAGACTGCCAGTGATAAACTGGAGGAAGGTGGGGATGACGTCAAGTCATCATGGCCCTTACGAGTAGGGCTACACACGTGCTACAATGGCGCATACAAAGAGAAGCGACCTCGCGAGAGCAAGCGGACCTCATAAAGTGCGTCGTAGTCCGGATTGGAGTCTGCAACTCGACTCCATGAAGTCGGAATCGCTAGTAATCGTAGATCAGAATGCTACGGTGAATACGTTCCCGGGCCTTGTACACACCGCCCGTCACACCATGGGAGTGGGTTGCAAAAGAAGTAGGTAGCTTAACCTTCGGGAGGGCGCTTACCACTTTGTGATTCATGACTGGGGTGAAGTCGTAACAAGGTAACCGTAGGGGAACCTGCGGTTGGATCACCTCCTT
>16S_rRNA::contig_1:3458-4996(-)
TTGAAGAGTTTGATCATGGCTCAGATTGAACGCTGGCGGCAGGCCTAACACATGCAAGTCGAGCGGCAGCGGGAAGTAGCTTGCTACTTTGCCGGCGAGCGGCGGACGGGTGAGTAATGTCTGGGAAACTGCCTGATGGAGGGGGATAACTACTGGAAACGGTAGCTAATACCGCATAACGTCGCAAGACCAAAGAGGGGGACCTTCGGGCCTCTTGCCATCAGATGTGCCCAGATGGGATTAGCTAGTAGGTGGGGTAACGGCTCACCTAGGCGACGATCCCTAGCTGGTCTGAGAGGATGACCAGCCACACTGGAACTGAGACACGGTCCAGACTCCTACGGGAGGCAGCAGTGGGGAATATTGCACAATGGGCGCAAGCCTGATGCAGCCATGCCGCGTGTATGAAGAAGGCCTTCGGGTTGTAAAGTACTTTCAGCGGGGAGGAAGGTGTTGAGGTTAATAACCTCAGCAATTGACGTTACCCGCAGAAGAAGCACCGGCTAACTCCGTGCCAGCAGCCGCGGTAATACGGAGGGTGCAAGCGTTAATCGGAATTACTGGGCGTAAAGCGCACGCAGGCGGTCTGTCAAGTCGGATGTGAAATCCCCGGGCTCAACCTGGGAACTGCATTCGAAACTGGCAGGCTAGAGTCTTGTAGAGGGGGGTAGAATTCCAGGTGTAGCGGTGAAATGCGTAGAGATCTGGAGGAATACCGGTGGCGAAGGCGGCCCCCTGGACAAAGACTGACGCTCAGGTGCGAAAGCGTGGGGAGCAAACAGGATTAGATACCCTGGTAGTCCACGCCGTAAACGATGTCGACTTGGAGGTTGTGCCCTTGAGGCGTGGCTTCCGGAGCTAACGCGTTAAGTCGACCGCCTGGGGAGTACGGCCGCAAGGTTAAAACTCAAATGAATTGACGGGGGCCCGCACAAGCGGTGGAGCATGTGGTTTAATTCGATGCAACGCGAAGAACCTTACCTACTCTTGACATCCAGAGAACTTAGCAGAGATGCTTTGGTGCCTTCGGGAACTCTGAGACAGGTGCTGCATGGCTGTCGTCAGCTCGTGTTGTGAAATGTTGGGTTAAGTCCCGCAACGAGCGCAACCCTTATCCTTTGTTGCCAGCGGTTAGGCCGGGAACTCAAAGGAGACTGCCAGTGATAAACTGGAGGAAGGTGGGGATGACGTCAAGTCATCATGGCCCTTACGAGTAGGGCTACACACGTGCTACAATGGCGCATACAAAGAGAAGCGACCTCGCGAGAGCAAGCGGACCTCATAAAGTGCGTCGTAGTCCGGATTGGAGTCTGCAACTCGACTCCATGAAGTCGGAATCGCTAGTAATCGTAGATCAGAATGCTACGGTGAATACGTTCCCGGGCCTTGTACACACCGCCCGTCACACCATGGGAGTGGGTTGCAAAAGAAGTAGGTAGCTTAACCTTCGGGAGGGCGCTTACCACTTTGTGATTCATGACTGGGGTGAAGTCGTAACAAGGTAACCGTAGGGGAACCTGCGGTTGGATCACCTCCTT
```

### Realizar la identificación taxonómica de la cepa utilizando como referencia la secuencia 16S identificada previamente usando blastn del NCBI

<img width="3024" height="1423" alt="image" src="https://github.com/user-attachments/assets/2cf72e76-5aac-4fef-ae8c-ef7de9aa29f2" />

### Revisar los alineamientos y establecer la taxonomia de la cepa en base al 16S

<img width="1941" height="1280" alt="image" src="https://github.com/user-attachments/assets/23e0e54e-9c02-4952-b643-8a6c06b02f21" />

### Buscar genomas de referencia en https://www.ncbi.nlm.nih.gov/datasets/genome/

<img width="2447" height="1401" alt="image" src="https://github.com/user-attachments/assets/a4bb8921-2c75-4d4d-80d1-f319f7c024d9" />

## 6. Validación de los genomas ensamblados

### Crear los directorios checkm y m01_fasta

```bash
cd ~/genomics/validation

mkdir checkm

cd checkm 

mkdir m01_fasta
```

### Copiar los genomas en el directorio m01_fasta

```bash
cp ~/genomics/assembly/nanopore/m01_flye.fasta ~/genomics/assembly/nanopore/m01_unicycler.fasta m01_fasta
```

### Validación de los genomas ensamblados

```bash
conda activate checkm

checkm taxonomy_wf -t 10 -x fasta genus Enterobacter m01_fasta . > m01_checkm_enterobacter.txt
```

> **Comentario:** 
> - `taxonomy_wf`: Es el flujo de trabajo basado en taxonomía. En lugar de buscar marcadores universales de bacterias o arqueas, utiliza un conjunto de genes que son específicos y conservados para el taxón que tú definas.
> - `-x fasta`: Especifica el formato de los archivos de entrada. En este caso, los archivos de entrada son genomas ensamblados en formato FASTA.
> - `m01_fasta`: Es el directorio de entrada donde se encuentran los archivos FASTA de los genomas que se van a evaluar. CheckM buscará en este directorio todos los archivos con extensión ".fasta" y los analizará.
> - `.`: Indica el directorio de salida. En este caso, los resultados se guardarán en el directorio actual.
> - `m01_checkm_enterobacter.txt`: Es el nombre del archivo donde se guardará la salida del análisis de CheckM.

```bash
tail -n 10 m01_checkm_enterobacter.txt

--------------------------------------------------------------------------------------------------------------------------------------------------------------
  Bin Id           Marker lineage    # genomes   # markers   # marker sets   0    1     2   3   4   5+   Completeness   Contamination   Strain heterogeneity  
--------------------------------------------------------------------------------------------------------------------------------------------------------------
  m01_unicycler   Enterobacter (5)       13         1338          370        3   1331   4   0   0   0       99.87            0.48               0.00          
  m01_flye        Enterobacter (5)       13         1338          370        4   1330   4   0   0   0       99.76            0.48               0.00          
--------------------------------------------------------------------------------------------------------------------------------------------------------------
```

> **Comentario:** 
> - `Bin Id`: Identificador del ensamblaje del genoma.
> - `Marker lineage`: Linaje del marcador utilizado para la evaluación. 
> - `# genomes`: Número de genomas de referencia utilizados en la evaluación.
> - `# markers`: Número total de marcadores genéticos (genes) usados en la evaluación.
> - `# marker sets`: Número de conjuntos de marcadores usados.
> - `0, 1, 2, 3, 4, 5+`: Distribución de los marcadores en los conjuntos.
> - `Completeness`: Porcentaje de marcadores esperados que se encontraron en el ensamblaje. Un valor alto indica un ensamblaje más completo.
> - `Contamination`: Porcentaje de marcadores duplicados o inesperados, lo que sugiere posible contaminación. Un valor bajo es mejor.
> - `Strain heterogeneity`: Indica la posible presencia de múltiples cepas en el ensamblaje. Un valor alto sugiere heterogeneidad.

## 7.	Clasificación taxonómica a nivel de especie mediante ANI (Average Nucleotide Identity)

### Exportar el mejor ensamblaje obtenido

### Ir a la herramienta ANI calculator de GTDB (https://gtdb.ecogenomic.org/tools/skani), cargar el archivo FASTA y seleccionar en GTDB TAXON el genero obtenido con la secuencia de 16S

<img width="2540" height="1488" alt="image" src="https://github.com/user-attachments/assets/2ada3415-bc8b-4d17-99da-598240129ac9" />

### Analizar los resultados obtenidos

<img width="2300" height="1304" alt="image" src="https://github.com/user-attachments/assets/1facc443-c73c-492a-b3ae-6bf14ef283ba" />

### Buscar el genoma de referencia

<img width="3024" height="1435" alt="image" src="https://github.com/user-attachments/assets/fdbe5d17-1df7-4d14-a852-0d18dbd99c44" />

## 8.	Ensamblaje del genoma de los datos de secuenciación Nanopore generados en el curso

> **Localización de los archivos:**

```bash
(base) alumno01@bio-SYS-7049GP-TRT:~$ tree -h genomics/trimming/nanopore/
[4.0K]  genomics/trimming/nanopore/
├── [205M]  b09_cup_nanofilt.fastq.gz
├── [236M]  b09_cup_porechop.fastq.gz
├── [546M]  b09_overlap.paf
├── [   0]  b09_porechop.err
├── [291K]  b09_porechop.log
├── [209M]  b09_rename.fastq.gz
├── [1.7M]  b09_report.yacrd
├── [ 895]  b09_stats_fastq.txt
└── [281M]  b09_yacrd.fastq.gz
```

```bash
(base) alumno02@bio-SYS-7049GP-TRT:~$ tree -h genomics/trimming/nanopore/
[4.0K]  genomics/trimming/nanopore/
├── [195M]  b10_nanofilt.fastq.gz
├── [816M]  b10_overlap.paf
├── [   0]  b10_porechop.err
├── [226M]  b10_porechop.fastq.gz
├── [370K]  b10_porechop.log
├── [198M]  b10_rename.fastq.gz
├── [2.2M]  b10_report.yacrd
├── [ 855]  b10_stats_fastq.txt
├── [269M]  b10_yacrd.fastq.gz
└── [1.6K]  historial_S04_G2.txt
```

```bash
(base) alumno03@bio-SYS-7049GP-TRT:~$ tree -h genomics/trimming/nanopore/
[4.0K]  genomics/trimming/nanopore/
├── [239M]  b11_overlap.paf
├── [   0]  b11_porechop.err
├── [130K]  b11_porechop.log
├── [ 88M]  b11_rename.fastq.gz
├── [679K]  b11_report.yacrd
├── [1.7K]  b11_stats_fastq.txt
├── [ 87M]  b11_sup_nanofilt.fastq.gz
├── [ 97M]  b11_sup_porechop.fastq.gz
├── [114M]  b11_yacrd.fastq.gz
├── [3.2M]  b15_overlap.paf
├── [   0]  b15_porechop.err
├── [ 60K]  b15_porechop.log
├── [1.1M]  b15_rename.fastq.gz
├── [221K]  b15_report.yacrd
├── [ 865]  b15_stats_fastq.txt
├── [1.0M]  b15_sup_nanofilt.fastq.gz
├── [7.8M]  b15_sup_porechop.fastq.gz
├── [3.1M]  b15_yacrd.fastq.gz
├── [ 97M]  barcode11.fastq.gz
└── [5.8K]  history.txt
```

```bash
(base) alumno04@bio-SYS-7049GP-TRT:~$ tree -h genomics/trimming/nanopore/
[4.0K]  genomics/trimming/nanopore/
├── [746M]  b12_overlap.paf
├── [   0]  b12_porechop.err
├── [273K]  b12_porechop.log
├── [173M]  b12_rename.fastq.gz
├── [1.6M]  b12_report.yacrd
├── [ 885]  b12_stats_fastq.gz
├── [ 885]  b12_stats_fastq.txt
├── [170M]  b12_sup_nanofilt.fastq.gz
├── [190M]  b12_sup_porechop.fastq.gz
└── [223M]  b12_yacrd.fastq.gz
```

```bash
file                 format  type  num_seqs      sum_len  min_len  avg_len  max_len     Q1     Q2     Q3  sum_gap    N50  N50_num  Q20(%)  Q30(%)  AvgQual  GC(%)  sum_n
b09_rename.fastq.gz  FASTQ   DNA     43,382  265,963,262    1,000  6,130.7   63,862  2,556  4,452  8,002        0  8,672    3,881   93.79   87.49    21.38  51.89      0
b10_rename.fastq.gz  FASTQ   DNA     48,826  249,960,072    1,000  5,119.4   62,371  2,127  3,595  6,429        0  7,176    4,044   94.02   86.08    21.56  35.21      0
b11_rename.fastq.gz  FASTQ   DNA     18,034  108,401,386    1,002  6,010.9   83,812  2,327  4,058  7,902        0  9,124    1,705   94.18   86.27    21.83  37.84      0
b12_rename.fastq.gz  FASTQ   DNA     40,008  211,655,500    1,000  5,290.3   48,632  2,149  3,631  6,817        0  7,723    3,469   94.13    86.2     21.8  38.09      0
```

| Columna | Descripción |
| :--- | :--- |
| **file** | Nombre del archivo analizado. |
| **format** | Formato de la secuencia (FASTQ/FASTA). |
| **type** | Tipo de molécula (DNA/RNA). |
| **num_seqs** | Cantidad total de lecturas (reads). |
| **sum_len** | Total de bases secuenciadas (Yield). |
| **min_len** | Longitud de la lectura más corta. |
| **avg_len** | Longitud promedio de las lecturas. |
| **max_len** | Longitud de la lectura más larga. |
| **Q1 / Q2 / Q3** | Cuartiles de longitud (25%, 50% [Mediana], 75%). |
| **sum_gap** | Cantidad de bases desaparecidas (Gaps/N's). |
| **N50** | Longitud mínima del 50% de las bases más largas. |
| **N50_num** | Número de lecturas necesarias para alcanzar el N50 (L50). |
| **Q20(%)** | Porcentaje de bases con precisión $\ge$ 99%. |
| **Q30(%)** | Porcentaje de bases con precisión $\ge$ 99.9%. |
| **AvgQual** | Calidad Phred promedio de la corrida. |
| **GC(%)** | Contenido de Guanina-Citosina (indicador taxonómico). |
| **sum_n** | Total de bases ambiguas (N). |


> **Bitácora bioinformática:** 
> - `Sorpresa!!!!`

