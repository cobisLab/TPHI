# TPHI (Transcriptomic Prediction of Human IRESs)

## Related paper:
Yu-Huai Yu, Zhi-Hao Jiang, Guan-Yi Zhou, and Tzu-Hsien Yang*, "TPHI: identifying human internal ribosome entry sites via integrating RNA binding protein targeting signals and sequence information
", 2026 (Submitted).

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
wget https://cobis-fs.bme.ncku.edu.tw/TPHI/TPHI_tool.tar.gz
```

2. Unzip the file.

```
tar -zxvf TPHI_tool.tar.gz
```

3. Change the working directory.

```
cd TPHI_tool
```

4. Download the processed RBP score datasets from the following link.

```
wget https://cobis-fs.bme.ncku.edu.tw/TPHI/resorces.tar.gz
```

5. Unzip the file.

```
tar -zxvf resorces.tar.gz
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
NM_000382.3,2479,2530
   ```
 Note: TPHI accepts transcript segments with length < 512 nts. If a segment with length < 512 nts is provided, it will be zero-padded into 512 nts. 

8. Predict the probability of transcript segments to have IRES elements in them.

```
python run_IRES.py -i <input_file> -o <output_directory>
```
>**Required arguments:**
>
>* -i: The input file for TPHI.
>
>* -o: The output directory for the predicted results.

## Output Results
If the following examples are used as the input:

```
python run_IRES.py -i ./example/input_example_1.csv -o ./example
```

** input_example.csv :**

```
NM_000382.3,2479,2530
```

Output formats:
[transcript_name@chromosome@start-end],[probability of having IRES elements]

```
NM_000382.3@chr17@2479-2530,0.800781786441803
```

