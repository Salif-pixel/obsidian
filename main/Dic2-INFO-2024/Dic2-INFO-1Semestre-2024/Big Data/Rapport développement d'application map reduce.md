

## Introduction

  

Le but de cet atelier est de développer une application Big Data capable de traiter les données issues de la plateforme GDELT. Ces données, qui représentent des événements mondiaux, doivent être analysées pour :

  

- Calculer le nombre total d’événements recensés par pays.

- Fournir une répartition des événements par type d’événement pour chaque pays.

  

L’application sera déployée sur un cluster Hadoop/HDFS de 10 nœuds, configuré à l’aide de Docker.

  

---

  

## Objectifs

  

1. Télécharger et comprendre les données issues de la plateforme GDELT.

2. Configurer un cluster Hadoop de 10 nœuds avec Docker pour simuler un environnement distribué.

3. Développer une application MapReduce pour analyser les données.

4. Exécuter et tester l’application sur le cluster Hadoop.

5. Généralisation

6. Difficultés rencontrées et conclusion

  

---

  

## Étape 1 : Compréhension des données GDELT

  

### Description des données

  

Les données GDELT se trouvent à GDELT Data et sont au format CSV. Chaque ligne représente un événement, avec plus de 50 colonnes. Voici les colonnes importantes pour notre projet :

  

- **EventCode** (colonne 26) : Type d’événement (par exemple, 10 = protestations, 20 = conflits armés).

- **ActionGeo_CountryCode** (colonne 51) : Le nom du pays où l’événement a eu lieu.

  

### Action :

  

1. Télécharge un fichier GDELT récent (exemple : `20231201.export.CSV`).

2. Étudie la structure des colonnes en ouvrant le fichier dans un tableur ou un éditeur de texte.

  

---

  
## Étape 2 : Configuration du cluster Hadoop (10 nœuds)

### Utilisation de Docker

  
Nous utiliserons l’image Docker **BigDataEurope Hadoop** pour configurer un cluster avec :

- 1 **Namenode** : Gère le système de fichiers HDFS.

- 10 **Datanodes** : Stockent les données et exécutent les calculs.

### Commandes pour configurer le cluster :

####  Télécharger l'image docker uploadée sur dockerhub:
  
```bash

docker pull liliasfaxi/spark-hadoop:hv-2.7.2

```
  
#### Créer les 11 contenaires à partir de l'image téléchargée. Pour cela:

1. Créer un réseau qui permettra de relier les 11 contenaires:

```bash

docker network create --driver=bridge hadoop

  ```
  
2. Lancer le namenode

```bash

docker run -itd --net=hadoop -p 50070:50070 -p 8088:8088 -p 707 --name hadoop-master --hostname hadoop-master liliasfaxi/spark-hadoop:hv-2.7.2

```

3. Configurer le nombre de datanodes

```bash

 vi $HADOOP_HOME/etc/hadoop/slaves

hadoop-slave1
hadoop-slave2
hadoop-slave3
hadoop-slave4
hadoop-slave5
hadoop-slave6
hadoop-slave7
hadoop-slave8
hadoop-slave9
hadoop-slave10                                                                                                                                                                                                                
```


4. Lancer les 10 Datanodes :
  
```bash

docker run -itd -p 8040:8042 --net=hadoop --name hadoop-slave1 --hostname hadoop-slave1 liliasfaxi/spark-hadoop:hv-2.7.2
1d9c4ff20cd16cadcbd60b657f94e589b2356ccadc3a308e4a863548c62e064f

docker run -itd -p 8041:8042 --net=hadoop --name hadoop-slave2 --hostname hadoop-slave2 liliasfaxi/spark-hadoop:hv-2.7.2
a21ec4aad3b2425eb91ad38916a94a0a38f31bf41d396ca024d8b6de75eedd87

docker run -itd -p 8042:8042 --net=hadoop --name hadoop-slave3 --hostname hadoop-slave3 liliasfaxi/spark-hadoop:hv-2.7.2
1fef704cca3de702a991a8b19ab1978ae0c583488793c727ba19e351d0a29790

docker run -itd -p 8043:8042 --net=hadoop --name hadoop-slave4 --hostname hadoop-slave4 liliasfaxi/spark-hadoop:hv-2.7.2
9cfb01f90de72ebbe1dda9650fc95b0471cef9f1d4bab0129a479b3c23a8a941

docker run -itd -p 8044:8042 --net=hadoop --name hadoop-slave5 --hostname hadoop-slave5 liliasfaxi/spark-hadoop:hv-2.7.2
eeec221ec4f1f0c22a73c57c09c58d9261d544eae38f92246fbd48e36458af8f

docker run -itd -p 8045:8042 --net=hadoop --name hadoop-slave6 --hostname hadoop-slave6 liliasfaxi/spark-hadoop:hv-2.7.2
f2d84ab62a4d723bf1fe9d983843498cc90f59680d8e59bfe855de9313560912

docker run -itd -p 8046:8042 --net=hadoop --name hadoop-slave7 --hostname hadoop-slave7 liliasfaxi/spark-hadoop:hv-2.7.2
2698706b5e8d7e5e0c86c6363f5af20354048c155d3b0785c75241645d71e6e3

docker run -itd -p 8047:8042 --net=hadoop --name hadoop-slave8 --hostname hadoop-slave8 liliasfaxi/spark-hadoop:hv-2.7.2
9404f677298ab0cb57477318d550961caf65a24a0e52f71e655295bc2aac3ead

docker run -itd -p 8048:8042 --net=hadoop --name hadoop-slave9 --hostname hadoop-slave9 liliasfaxi/spark-hadoop:hv-2.7.2
3d12b09e4a361a9051a3d7d08538a157aa70b7fa19be2b283ce483a33cf6aa43

docker run -itd -p 8049:8042 --net=hadoop --name hadoop-slave10 --hostname hadoop-slave10 liliasfaxi/spark-hadoop:hv-2.7.2
b4d382ec0e161c0d849db57147e024bbe34e3a36a3395c1b0c4f4b0616613274

  
```

5. Entrer dans le contenaire master pour commencer à l'utiliser.

```bash

docker exec -it hadoop-master bash
root@hadoop-master:~#

```

6. Lancer le script start-hadoop.sh

```bash
./start-hadoop.sh

Starting namenodes on [hadoop-master]
hadoop-master: Warning: Permanently added 'hadoop-master,172.19.0.2' (ECDSA) to the list of known hosts.
hadoop-master: namenode running as process 3619. Stop it first.
hadoop-slave2: Warning: Permanently added 'hadoop-slave2,172.19.0.10' (ECDSA) to the list of known hosts.
hadoop-slave1: Warning: Permanently added 'hadoop-slave1,172.19.0.11' (ECDSA) to the list of known hosts.
hadoop-slave7: Warning: Permanently added 'hadoop-slave7,172.19.0.16' (ECDSA) to the list of known hosts.
hadoop-slave4: Warning: Permanently added 'hadoop-slave4,172.19.0.13' (ECDSA) to the list of known hosts.
hadoop-slave5: Warning: Permanently added 'hadoop-slave5,172.19.0.14' (ECDSA) to the list of known hosts.
hadoop-slave3: Warning: Permanently added 'hadoop-slave3,172.19.0.12' (ECDSA) to the list of known hosts.
hadoop-slave6: Warning: Permanently added 'hadoop-slave6,172.19.0.15' (ECDSA) to the list of known hosts.
hadoop-slave8: Warning: Permanently added 'hadoop-slave8,172.19.0.17' (ECDSA) to the list of known hosts.
hadoop-slave9: Warning: Permanently added 'hadoop-slave9,172.19.0.18' (ECDSA) to the list of known hosts.
hadoop-slave10: Warning: Permanently added 'hadoop-slave10,172.19.0.19' (ECDSA) to the list of known hosts.

```

8. Vérifie que le cluster est actif :

• Accède à l’interface web HDFS : http://localhost:50070.

![[2024-12-28 22_57_51-.png]]


• Vérifie que les 10 nœuds  sont opérationnels: 
http://localhost:8040
http://localhost:8041
http://localhost:8042
http://localhost:8043
http://localhost:8044
http://localhost:8045
http://localhost:8046
http://localhost:8047
http://localhost:8048
http://localhost:8049

![[2024-12-28 22_48_45-.png]]
  
---
## Étape 3 : Développement de l’application MapReduce

### L’application analysera les données GDELT et produira pour chaque pays 

- Le nombre total d’événements recensés.

-  La répartition des événements par type.

#### Ouvrir le chier pom.xml, et ajouter les dépendances suivantes pour Hadoop, HDFS et Map Reduce:

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<project xmlns="http://maven.apache.org/POM/4.0.0"  
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0   http://maven.apache.org/xsd/maven-4.0.0.xsd">  
    <modelVersion>4.0.0</modelVersion>  
  
    <groupId>hadoop.mapreduce</groupId>  
    <artifactId>CountTypeEvent</artifactId>  
    <version>1.0</version>  
  
    <properties>        
        <maven.compiler.source>1.8</maven.compiler.source>  
        <maven.compiler.target>1.8</maven.compiler.target>  
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  
    </properties>  
    
    <dependencies>        
    
       <dependency>           
            <groupId>org.apache.hadoop</groupId>  
            <artifactId>hadoop-common</artifactId>  
            <version>2.7.2</version>  
        </dependency> 
         
        <dependency>            
            <groupId>org.apache.hadoop</groupId>  
            <artifactId>hadoop-mapreduce-client-core</artifactId>  
            <version>2.7.2</version>  
        </dependency>  
        
        <dependency>           
            <groupId>org.apache.hadoop</groupId>  
            <artifactId>hadoop-hdfs</artifactId>  
            <version>2.7.2</version>  
        </dependency>  
        
        <dependency>            
            <groupId>org.apache.hadoop</groupId>  
            <artifactId>hadoop-mapreduce-client-common</artifactId>  
            <version>2.7.2</version>  
        </dependency>  
          
    </dependencies>
    
</project>

```

#### Créer un package tn.insat.tp sous le répertoire src/main/java puis créer la classe `GDELTMapper`

Le mapper lit chaque ligne du fichier CSV, extrait le code pays et le type d’événement, puis les émet sous la forme :
(Pays:Type, 1)

Exemple de code (Java) :

```java

package tn.insat;  
  
import java.io.IOException;  
import org.apache.hadoop.io.IntWritable;  
import org.apache.hadoop.io.Text;  
import org.apache.hadoop.mapreduce.Mapper;  
import java.io.IOException;  
public class GDELTMapper extends Mapper<Object, Text, Text, IntWritable> {  
    private Text countryEvent = new Text();  
    private final static IntWritable one = new IntWritable(1);  
    public void map(Object key, Text value, Context context) throws IOException, InterruptedException {  
        String[] fields = value.toString().split("\\t"); // Les données GDELT sont tabulées  
        if (fields.length > 51 && !fields[51].isEmpty()) {  
            String country = fields[51];  
            String eventType = fields[26];  
            countryEvent.set(country + "-" + eventType);  
            context.write(countryEvent, one);  
        }  
    }  
}

  
```

#### Créer la classe `GDELTReducer`

Le reducer agrège les occurrences pour chaque clé (Pays:Type) et produit le total :

(Pays:Type, Total)

Exemple de code (Java) :
  
```java

package tn.insat;  
  
import org.apache.hadoop.io.IntWritable;  
import org.apache.hadoop.io.Text;  
import org.apache.hadoop.mapreduce.Reducer;  
  
import java.io.IOException;  
  
public class GDELTReducer extends Reducer<Text, IntWritable, Text, IntWritable> {  
    public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {  
        int sum = 0;  
        for (IntWritable val : values) {  
            sum += val.get();  
        }  
        context.write(key, new IntWritable(sum));  
    }  
}

 ```


#### Créer la classe `GDELTDriver`

Le driver configure le job Hadoop, spécifie le mapper/reducer et lance le traitement.

Exemple de code (Java) :

  
```java

package tn.insat;  
  
import org.apache.hadoop.conf.Configuration;  
import org.apache.hadoop.fs.Path;  
import org.apache.hadoop.io.IntWritable;  
import org.apache.hadoop.io.Text;  
import org.apache.hadoop.mapreduce.Job;  
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;  
import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;  
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;  
import tn.insat.GDELTMapper;  
import tn.insat.GDELTReducer;  
  
public class GDELTDriver {  
    public static void main(String[] args) throws Exception {  
        Configuration conf = new Configuration();  
        Job job = Job.getInstance(conf, "GDELT Event Analysis");  
        job.setJarByClass(GDELTDriver.class);  
        job.setMapperClass(GDELTMapper.class);  
        job.setReducerClass(GDELTReducer.class);  
        job.setOutputKeyClass(Text.class);  
        job.setOutputValueClass(IntWritable.class);  
  
        // Utilisez TextInputFormat pour les fichiers texte  
        job.setInputFormatClass(TextInputFormat.class);  
  
        // Définir les chemins d'entrée et de sortie  
        FileInputFormat.addInputPath(job, new Path(args[0]));  
        FileOutputFormat.setOutputPath(job, new Path(args[1]));  
  
        // Lancer le job  
        System.exit(job.waitForCompletion(true) ? 0 : 1);  
    }  
}
  
```

---
## Étape 4 : Exécution du programme

### Créer une configuration Maven avec la ligne de commande: ==package install== 

#### Lancer la configuration. Un fichier CountTypeEvent-1.0.jar sera créé dans le répertoire target du projet

1. Copier le fichier jar créé dans le contenaire master.

```bash


docker cp target/CountTypeEvent-1.0.jar hadoop-master:/root

```

#### Charge les données GDELT sur HDFS :

  ```bash


docker exec -it hadoop-master bash

hdfs dfs -mkdir /input

hdfs dfs -put /path/to/20231201.export.CSV /input/

  ```

#### Lance le job Hadoop :

  ```bash


hadoop jar CountTypeEvent-1.0.jar tn.insat.GDELTDriver /input /output

  ```

#### Vérifie les résultats :

  ```bash


hdfs dfs -tail /output/part-r-00000
```

#### Résultat attendu

Pour chaque pays, le rapport inclura des lignes comme :

```bash

US-023  25  

US-045  100

FR-060  19  

FR-095  13  

CA-079  28  

CA-035  26

```

---
## Étape 5 : Généralisation

### Télécharger le fichier html ayant l'ensemble des fichiers csv et extraire les liens fichiers zip dans un fichier .txt 
#### On crée un script download_html.sh

```bash
#!/bin/bash

# URL de base pour les fichiers
base_url="http://data.gdeltproject.org/events/"

# Télécharger le contenu de la page web contenant les fichiers
wget -q -O index.html ${base_url}

# Extraire les liens des fichiers ZIP depuis la page HTML
grep -oP 'HREF="\K[^"]+\.zip' index.html > files.txt

```
#### Télécharger les fichier csv via le files.txt en créant un script download_csv.sh

```bash
#!/bin/bash

base_url="http://data.gdeltproject.org/events/"
files="files.txt"

# Télécharger chaque fichier ZIP et supprimer la ligne correspondante après téléchargement
while read -r file; do
    # Télécharger le fichier
    if wget "${base_url}${file}" -P ./upload; then
        # Supprimer la ligne correspondante du fichier si le téléchargement a réussi
        sed -i "/^${file}$/d" "$files"
        echo "Téléchargement terminé et ligne supprimée : $file"
    else
        echo "Échec du téléchargement : $file"
    fi
done < "$files"

```

#### Exécuter le script `./download_csv.sh`

![[Pasted image 20250106122556.png]]

#### `unziper` les fichiers dans `upload` en créant un script unzip.sh

```bash
#!/bin/bash

# unzip
for file in ./upload/*.zip; do
    unzip "$file" -d ./upload
done

```

#### Exécuter le script `./unzip.sh`

![[2024-12-28 19_41_01-.png]]

#### Copier les fichiers CSV dans input

```bash

hadoop fs -put ./upload/*.CSV input

```

#### Vérifier le contenu de input `hadoop fs -ls input`

![[2024-12-28 19_43_41-C__Users_DELL_OneDrive_Documents_Rainmeter_Skins_Mond_Settings_Settings.ini.png]]

#### Exécuter le job

  ```bash


hadoop jar CountTypeEvent-1.0.jar tn.insat.GDELTDriver input output

  ```

![[Pasted image 20250106111543.png]]

#### Vérifier les sorties au niveau du dossier output 

```bash

root@hadoop-master:~# hadoop fs -ls output
Found 2 items
-rw-r--r--   2 root supergroup          0 2025-01-06 11:13 output/_SUCCESS
-rw-r--r--   2 root supergroup    3732043 2025-01-06 11:13 output/part-r-00000

```

#### vérifier si on a le résultat attendu 

![[Pasted image 20250106113817.png]]

---
## Etape 6 difficultés rencontrées et conclusion
### Difficultés rencontrées :

L'une des principales difficultés rencontrées lors de l'étape 5 était la gestion du grand nombre de fichiers CSV disponibles sur la plateforme GDELT. Avec des milliers de fichiers à traiter, il a été nécessaire de se concentrer sur un sous-ensemble des fichiers plutôt que de tous les télécharger et traiter en une seule fois. Pour cela, j'ai téléchargé et extrait les liens de fichiers CSV en les organisant dans un fichier texte, puis j'ai utilisé des scripts pour télécharger les fichiers ZIP et les extraire avant de les charger sur HDFS. Ce processus a permis d'éviter de surcharger le cluster Hadoop avec un trop grand nombre de fichiers simultanément.

### Conclusion :

En conclusion, l'atelier a permis de mettre en place une application Big Data fonctionnelle pour analyser les données mondiales issues de la plateforme GDELT. Grâce à l'utilisation de Hadoop et Docker, nous avons pu simuler un environnement distribué sur 10 nœuds, ce qui a facilité le traitement des grandes quantités de données. Le projet a été une excellente occasion d'explorer le traitement parallèle et les principes du Big Data tout en surmontant des défis liés à la gestion de données massives.

  



