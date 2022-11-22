# Workshop1
## Установка программ и получение данных
1) Установить miniconda/anaconda 
```
https://docs.conda.io/en/latest/miniconda.html#linux-installers
```
2) Установить через conda fastq-dump, создав окружение
```
conda create -n workshop1 -c bioconda sra-tools
```
> войти в окружение 
```
conda activate workshop1
```
>> Доп задание: установить другим способом
4) Скачать данные через Fastq-dump
```
fasterq-dump -S SRR957824
```
>Запасной вариант:
```
curl -O -J -L https://osf.io/shqpv/download
curl -O -J -L https://osf.io/9m3ch/download
```
>>или с сайта https://www.ncbi.nlm.nih.gov/sra  / https://www.ebi.ac.uk/
>>> Доп задание: взять выборку из 500к ридов

## Оценка качества данных
5) установаить fastqc 
```
> https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
```
> conda install -c bioconda fastqc
6) проанализировать качество данных с помощью fastqc
```
fastqc -t 12 SRR957824_1.fastq SRR957824_2.fastq
```
## Удаление адаптеров и фильтрация по качеству
>>>Задача удалить адаптеры и сделать фильтрацию по качеству используя разные программы, после каждой надо запустить fastqc и сравнить с исходной

7) Установить и запустить Adapterremoval
```
https://adapterremoval.readthedocs.io/
AdapterRemoval --file1 reads_1.fq --file2 reads_2.fq --basename output_paired --trimns --trimqualities 
```
> Доп задание: определить адаптеры с помощью флага --identify-adapters

7) Установить и запустить fastp
``` 
https://github.com/OpenGene/fastp

fastp -i in.R1.fq.gz -I in.R2.fq.gz -o out.R1.fq.gz -O out.R2.fq.gz
```

7) Установаить и запустить cutadapt
```
https://cutadapt.readthedocs.io/en/stable/installation.html
```
> Доп задание: найти адаптеры с помощью cutadapt
>> Установить через pip
7) Установить scythe
```
https://github.com/vsbuffalo/scythe
conda install -c hcc scythe

scythe -a adapters.fasta -o SRR957824_adapt_R1.fastq SRR957824_500K_R1.fastq.gz
scythe -a adapters.fasta -o SRR957824_adapt_R2.fastq SRR957824_500K_R2.fastq.gz
```

```
Подсказка: Адаптеры - curl -O -J -L https://osf.io/v24pt/download
```

99) Сделать подвыборку fastq
```
seqtk sample -s100 read1.fq 10000 > sub1.fq
seqtk sample -s100 read2.fq 10000 > sub2.fq
```
>Использовать bbmap (https://sourceforge.net/projects/bbmap/)
>Использоать head


99) Запустить fastp через docker
```
>Установка докера 
sudo apt-get update
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin

Получение и запуска контейнера с fastp
docker pull chrishah/fastp
docker run --rm -v $(pwd):/in -w /in chrishah/fastp:0.23.1 fastp --version
```
