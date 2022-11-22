# Workshop1
1) Установить miniconda/anaconda (https://docs.conda.io/en/latest/miniconda.html#linux-installers)
2) Установить через conda fastq-dump, создав окружение
> conda create -n workshop1 -c bioconda sra-tools
> войти в окружение conda activate workshop1
>> Доп задание: установить другим способом
4) Скачать данные через Fastq-dump (fasterq-dump -S SRR957824)
>Запасной вариант:
>curl -O -J -L https://osf.io/shqpv/download
>curl -O -J -L https://osf.io/9m3ch/download
>>или с сайта https://www.ncbi.nlm.nih.gov/sra  / https://www.ebi.ac.uk/
5) установаить fastqc 
> https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
> conda install -c bioconda fastqc
