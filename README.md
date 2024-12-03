# TPHI (Transcriptomic Prediction of Human IRESs)

## Related paper:
Tzu-Hsien Yang*, Chin-Cheng Lee, Yu-Huai Yu, "TPHI: identifying human internal ribosome entry sites via integrating the sequence information and RNA binding protein targeting signals", 2024 (Submitted).

## Prepare the Environment

Suggested running environments: Linux Ubuntu 16.04.6, Python 3.8.13

We recommend that you can use the conda package to create a new environment. This will automatically install the required python packages. 

Here is an example: 

1. Install the Conda package for you system. The installation of the package can be found <a href="https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html">here</a>. 

2. Create the TPHI Conda environment. This may take a while, depending on the network status.

```
conda create -n "TPHI" python=3.8.13
```

3. Activate your CFA Conda environment. 

```
conda activate TPHI
```

## Steps to Use TPHI

1. Download the codes from the following link and unzip the file. Please skip it if you have done this step.

```
wget https://cobis-fs.bme.ncku.edu.tw/TPHI/TPHI.tar.gz
```

2. Unzip the file.

```
tar -zxvf TPHI.tar.gz
```

3. Change the working directory.

```
cd TPHI_Model
```

4. Download the processed RBP score datasets from the following link.

```
wget https://cobis-fs.bme.ncku.edu.tw/TPHI/SCORES.tar.gz
```

5. Unzip the file.

```
tar -zxvf SCORES.tar.gz
```

6. If this is the first time you use TPHI, run the following command to install necessary packages. 

```
pip install -r requirements.txt
```

TPHI can also support GPU acceleration. If you want to utilize GPU, please run the following command instead:

```
pip install -r requirements_gpu.txt
```


7. Prepare the input human transcript segment locations (ver. hg38).
   Multiple transcript segments can be provided in the same input file.
   
   The input format **SHOULD** followed the following formats:
   transcript_name,start,end
   
   For example: (as the input file named input_example.csv) 
   
   ```
   XM_017015164.1,1233,1744
   NM_001349460.2,774,1285
   ```
 Note: TPHI accepts transcript segments with length < 512 nts. If a segment with length < 512 nts is provided, it will be zero-padded into 512 nts. 

8. Predict the probability of transcript segments to have IRES elements in them.

```
python main.py -i <input_file> -o <output_file>
```
>**Required arguments:**
>
>* -i: The input file for TPHI.
>
>* -o: The output file name of the predicted results.

## Output Results
If the following examples are used as the input:

```
python main.py -i input_example.csv -o example_results.csv
```

** example_results.csv :**

```
XM_017015164.1,1233,1744
NM_001349460.2,774,1285
```

Output formats:
[transcript_name$start$end] [probability of having IRES elements]

```
XM_017015164$1233$1744  0.9999996423721313
NM_001349460$774$1285   0.4256390631198883
```

