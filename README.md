# Day 10 Lab: Data Pipeline & Data Observability

**Student ID**: AI20K-0313 (full: AI20K-2A202600313)  
**Student Email**: 26ai.sonttt@vinuni.edu.vn  
**Name**: Tran Thuong Truong Son

---

## Mo ta

Project nay xay dung mot ETL pipeline co ban de xu ly du lieu san pham:
- **Extract** tu `raw_data.json`
- **Validate** de loai record khong hop le (gia <= 0 hoac category rong)
- **Transform** gom chuan hoa category (Title Case), tinh `discounted_price` giam 10%, va them `processed_at`
- **Load** ket qua ra `processed_data.csv`

Ngoai ra, project co phan mo phong agent (`agent_simulation.py`) de so sanh tac dong cua:
- du lieu sach (`processed_data.csv`)
- du lieu ban/co loi (`garbage_data.csv`)

---

## Cach chay (How to Run)

### 1) Prerequisites
```bash
pip install pandas
```

Neu may dung `python3`:
```bash
pip3 install pandas
```

### 2) Chay ETL Pipeline
```bash
python solution.py
```

Hoac:
```bash
python3 solution.py
```

### 3) Tao du lieu garbage (neu chua co)
```bash
python generate_garbage.py
```

### 4) Chay Agent Simulation (Clean vs Garbage)
```bash
python agent_simulation.py
```

Expected output:
```text
Testing with CLEAN data:
Agent: Based on my data, the best choice is Laptop at $1200.

Testing with GARBAGE data:
Agent: Based on my data, the best choice is Nuclear Reactor at $999999.
```

---

## Cau truc thu muc

```text
data-pipeline-observability-TruongSon421/
├── solution.py              # ETL pipeline chinh
├── raw_data.json            # Input goc
├── processed_data.csv       # Output sau ETL
├── generate_garbage.py      # Tao bo du lieu loi de stress test
├── garbage_data.csv         # Du lieu ban (sinh ra boi generate_garbage.py)
├── agent_simulation.py      # Mo phong agent tra loi tu CSV
├── experiment_report.md     # Bao cao ket qua thuc nghiem
├── tests/
│   └── test_autograder.py   # Test tu dong
└── README.md                # Tai lieu huong dan
```

---

## Ket qua

### ETL Pipeline
- Input: `raw_data.json` co **5** records.
- Sau validate:
  - **3 valid** records duoc giu lai.
  - **2 records** bi loai (1 record gia am, 1 record category rong).
- Output `processed_data.csv` chua cac cot:
  - `id`, `product`, `price`, `category`, `discounted_price`, `processed_at`.

### Agent Simulation
- Voi clean data, agent dua ra ket qua hop ly: **Laptop ($1200)**.
- Voi garbage data, agent van chay nhung de xuat phi thuc te: **Nuclear Reactor ($999999)** do outlier.

Dieu nay cho thay chat luong du lieu anh huong truc tiep den chat luong cau tra loi cua agent (garbage in, garbage out).
