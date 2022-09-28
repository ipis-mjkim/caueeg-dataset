# caueeg-dataset

**CAUEEG**: **C**hung-**A**ng **U**niversity Hospital **EEG** dataset for automatic EEG diagnosis research

This repository is the official page of the CAUEEG dataset presented in "Deep learning-based EEG analysis to classify mild cognitive impairment for early detection of dementia: algorithms and benchmarks."

---

## Detailed information

An academic paper including all the detailed information will be upcoming soon.

---

## Dataset access

> ❗ Note: The use of the CAUEEG dataset is allowed for only academic and research purposes 👩‍🎓👨🏼‍🎓.

- Researchers wishing to utilize the CAUEEG dataset should turn out [this form](https://forms.gle/gqas9pXfDZLPWqX97) as approval from the local ethics committee is required.
- After reviewing the response, we will send you a mail with a download link and password.
<!-- - If someone has trouble using the form, please mail to neudoc@gmail.com -->

---

## File components

The file tree for the CAUEEG data set is as follows:

```tree
caueeg-dataset
|   annotation.json
|   annotation.xlsx
|   dementia.json
|   abnormal.json
|   
+---event
|       00001.json
|       00002.json
|           ...
|       01388.json
|       
\---signal
    +---edf
    |       00001.edf
    |       00002.edf
    |           ...
    |       01388.edf
```

- `caueeg-dataset/annotation.json`: Diagnostic annotation file for each EDF and event pair.
- `caueeg-dataset/annotation.xlsx`: Excel version of `annotation.json` for visualization.
- `caueeg-dataset/dementia.json`: Annotation file for the `CAUEEG-Dementia` benchmark.
- `caueeg-dataset/abnormal.json`: Annotation file for the `CAUEEG-Abnormal` benchmark.
- `caueeg-dataset/event/*.json`: Event descriptions during EEG recording.
- `caueeg-dataset/signal/edf/*.edf`: EEG signals written in European data format (EDF).

---

## Usage

### Requirements

The implementation code for using the CAUEEG dataset and benchmarks via the PyTorch library is available in a public repository at [caueeg-ceednet](https://github.com/ipis-mjkim/caueeg-ceednet).

### CAUEEG dataset

With [caueeg-ceednet](https://github.com/ipis-mjkim/caueeg-ceednet), here is an example of loading the CAUEEG dataset:

```python
import pprint
from datasets.caueeg_script import *

config_data, full_eeg_dataset = load_caueeg_full_dataset(dataset_path='local/dataset/caueeg-dataset/', 
                                                         load_event=False)

pprint.pprint(config_data, width=250)
print('\n', '-' * 100, '\n')
pprint.pprint(full_eeg_dataset[0])
print('\n', '-' * 100, '\n')
pprint.pprint(full_eeg_dataset[3])
```

```pprint
{'dataset_name': 'CAUEEG dataset',
 'signal_header': ['Fp1-AVG', 'F3-AVG', 'C3-AVG', 'P3-AVG', 'O1-AVG', 'Fp2-AVG', 'F4-AVG', 'C4-AVG', 'P4-AVG', 'O2-AVG', 'F7-AVG', 'T3-AVG', 'T5-AVG', 'F8-AVG', 'T4-AVG', 'T6-AVG', 'FZ-AVG', 'CZ-AVG', 'PZ-AVG', 'EKG', 'Photic']}

 ---------------------------------------------------------------------------------------------------- 

{'age': 78,
 'serial': '00001',
 'signal': array([[  0., -11., -13., ...,   0.,   0.,   0.],
       [ 29.,  33.,  34., ...,   0.,   0.,   0.],
       [ -3.,  -6.,  -3., ...,   0.,   0.,   0.],
       ...,
       [ -4.,  -2.,   1., ...,   0.,   0.,   0.],
       [112.,  67.,  76., ...,   0.,   0.,   0.],
       [ -1.,  -1.,  -1., ...,   0.,   0.,   0.]]),
 'symptom': ['mci', 'mci_amnestic', 'mci_amnestic_rf']}

 ---------------------------------------------------------------------------------------------------- 

{'age': 78,
 'serial': '00004',
 'signal': array([[ 30.,  34.,  36., ...,   0.,   0.,   0.],
       [ 34.,  25.,  24., ...,   0.,   0.,   0.],
       [ 11.,  15.,  15., ...,   0.,   0.,   0.],
       ...,
       [-10.,  -6.,  -4., ...,   0.,   0.,   0.],
       [ 23.,  32.,  30., ...,   0.,   0.,   0.],
       [ -1.,   0.,  -1., ...,   0.,   0.,   0.]]),
 'symptom': ['dementia', 'ad', 'load']}
```

---

With `load_event` option triggered, the dataset also loads event data, as follows:

```python
config_data, full_eeg_dataset = load_caueeg_full_dataset(dataset_path='local/dataset/caueeg-dataset/', 
                                                         load_event=True)

pprint.pprint(config_data, width=250)
print('\n', '-' * 100, '\n')
pprint.pprint(full_eeg_dataset[0])
```

```text
{'dataset_name': 'CAUEEG dataset',
 'signal_header': ['Fp1-AVG', 'F3-AVG', 'C3-AVG', 'P3-AVG', 'O1-AVG', 'Fp2-AVG', 'F4-AVG', 'C4-AVG', 'P4-AVG', 'O2-AVG', 'F7-AVG', 'T3-AVG', 'T5-AVG', 'F8-AVG', 'T4-AVG', 'T6-AVG', 'FZ-AVG', 'CZ-AVG', 'PZ-AVG', 'EKG', 'Photic']}

 ---------------------------------------------------------------------------------------------------- 

{'age': 78,
 'event': [[0, 'Start Recording'],
           [0, 'New Montage - Montage 002'],
           [36396, 'Eyes Open'],
           [72518, 'Eyes Closed'],
           [73862, 'Eyes Open'],
           [75248, 'Eyes Closed'],
           [76728, 'swallowing'],
           [77978, 'Eyes Open'],
           [79406, 'Eyes Closed'],
           [79996, 'Photic On - 3.0 Hz'],
           [80288, 'Eyes Open'],
           [81296, 'Eyes Closed'],
           [82054, 'Photic Off'],
           [84070, 'Photic On - 6.0 Hz'],
           [84488, 'Eyes Open'],
           [85538, 'Eyes Closed'],
           [86086, 'Photic Off'],
           [88144, 'Photic On - 9.0 Hz'],
           [90160, 'Photic Off'],
           [91458, 'Eyes Open'],
           [92218, 'Photic On - 12.0 Hz'],
           [92762, 'Eyes Closed'],
           [94198, 'Photic Off'],
           [94742, 'Eyes Open'],
           [95708, 'Eyes Closed'],
           [96256, 'Photic On - 15.0 Hz'],
           [98272, 'Photic Off'],
           [100330, 'Photic On - 18.0 Hz'],
           [102346, 'Photic Off'],
           [102596, 'Eyes Open'],
           [103856, 'Eyes Closed'],
           [104361, 'Photic On - 21.0 Hz'],
           [106420, 'Photic Off'],
           [106880, 'Eyes Open'],
           [107804, 'Eyes Closed'],
           [108435, 'Photic On - 24.0 Hz'],
           [110452, 'Photic Off'],
           [111080, 'Eyes Open'],
           [112004, 'Eyes Closed'],
           [112509, 'Photic On - 27.0 Hz'],
           [114528, 'Photic Off'],
           [114864, 'Eyes Open'],
           [116124, 'Eyes Closed'],
           [116544, 'Photic On - 30.0 Hz'],
           [118602, 'Photic Off'],
           [126672, 'artifact'],
           [134030, 'Move'],
           [135584, 'Eyes Open'],
           [136668, 'Eyes Closed'],
           [139818, 'Eyes Open'],
           [141414, 'Eyes Closed'],
           [145000, 'Paused']],
 'serial': '00001',
 'signal': array([[  0., -11., -13., ...,   0.,   0.,   0.],
       [ 29.,  33.,  34., ...,   0.,   0.,   0.],
       [ -3.,  -6.,  -3., ...,   0.,   0.,   0.],
       ...,
       [ -4.,  -2.,   1., ...,   0.,   0.,   0.],
       [112.,  67.,  76., ...,   0.,   0.,   0.],
       [ -1.,  -1.,  -1., ...,   0.,   0.,   0.]]),
 'symptom': ['mci', 'mci_amnestic', 'mci_amnestic_rf']}
```

### CAUEEG-Dementia benchmark

Here is an example of loading the CAUEEG-Dementia benchmark:

```python
config_data, train_dataset, val_dataset, test_dataset = load_caueeg_task_datasets(dataset_path='local/dataset/caueeg-dataset/', 
                                                                                  task='dementia',
                                                                                  load_event=False)
pprint.pprint(config_data)
print('\n', '-' * 100, '\n')

pprint.pprint(train_dataset[0])
print('\n', '-' * 100, '\n')

pprint.pprint(val_dataset[0])
print('\n', '-' * 100, '\n')

pprint.pprint(test_dataset[0])
```

Similarly, the CAUEEG-Abnormal benchmark is loaded as follows:

```python
config_data, train_dataset, val_dataset, test_dataset = load_caueeg_task_datasets(dataset_path='local/dataset/caueeg-dataset/', 
                                                                                  task='abnormal',
                                                                                  load_event=False)
pprint.pprint(config_data)
print('\n', '-' * 100, '\n')

pprint.pprint(train_dataset[0])
print('\n', '-' * 100, '\n')

pprint.pprint(val_dataset[0])
print('\n', '-' * 100, '\n')

pprint.pprint(test_dataset[0])
```

### Advanced usage

For more advanced usages of the CAUEEG dataset and two corresponding benchmarks, refer to [this notebook](https://github.com/ipis-mjkim/caueeg-ceednet/notebook/01_DataSet_DataLoader.ipynb).

---

## Citation

If you found this dataset helpful, please cite the paper below.

```bib
An academic paper will be upcoming soon.
```
