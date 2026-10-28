# ARX-MFCM hydraulic propulsion dataset

Original Excel simulation records for fault diagnosis of shield tunneling machine hydraulic propulsion systems.

## Files and classes

The `data/` directory contains **50 original `.xlsx` files**, with 10 records for each of five operating states. Original file names, worksheet headers, and file bytes are preserved.

| Class ID | Operating state | Original filename prefix |
| --- | --- | --- |
| 0 | Normal operation | 正常状态 |
| 1 | Hydraulic cylinder leakage | 液压缸泄露 |
| 2 | Directional valve leakage | 换向阀泄漏 |
| 3 | Flow control valve damage | 调速阀损坏 |
| 4 | Relief valve damage | 溢流阀损坏 |

Each record contains 6001 sampling points, covering approximately 0–60 seconds with a nominal sampling interval of 0.01 seconds. Eight named columns describe simulation time, cylinder displacement and velocity, two chamber pressures, valve outlet flow, load force, and system pressure. Preserve any additional unnamed worksheet columns when reproducing the original records. Physical units are not explicitly stored in the original column headers; no units have been inferred for those variables here.

`data_dictionary.csv` lists the original named columns. `records.csv` provides class IDs, record numbers, numeric duplicate groups, and file checksums. `checksums.sha256` can be used to verify the original Excel bytes.

## Record numbering and duplicate awareness

The record-number split used with this dataset assigns records 1–6 from each class to training and records 7–10 to testing, producing 30 training records and 20 test records. This split is recorded as metadata, not asserted to be statistically independent.

The 50 files contain **30 unique complete numeric records**; some differently named files have identical numeric content. **11 numeric duplicate groups cross the record-number training/test split.** For evaluation that requires independent records, account for these duplicate groups before creating partitions. The supplied files have not been deduplicated or modified.

## Read a record

```python
import pandas as pd

record = pd.read_excel("data/正常状态数据样本1.xlsx")
print(record.head())
```

Dependencies for this example: `pandas` and `openpyxl`.

## 数据说明

本仓库提供五种运行状态的50个原始Excel仿真记录，每类10个文件。各记录含6001个采样点，时间约为0–60秒，名义采样间隔0.01秒。文件名、表头及文件内容均保持不变。

五类状态依次为正常运行、液压缸泄漏、换向阀泄漏、调速阀损坏及溢流阀损坏。`records.csv`列出类别、记录编号、数值重复组和校验值；`data_dictionary.csv`列出有名称的数据列。

按每类1–6号训练、7–10号测试可得到30/20记录划分，但其中存在跨集合数值重复。进行独立泛化评价时，应先检查重复分组，再确定适当的数据划分。
