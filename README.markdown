# Phân Cụm Khách Hàng bằng K-Means

## Giới thiệu
Dự án này sử dụng thuật toán **K-Means** để phân cụm khách hàng dựa trên dữ liệu từ tệp `Cust_Segmentation.csv`. Mục tiêu là phân nhóm khách hàng theo các đặc trưng như tuổi, thu nhập, nợ thẻ tín dụng, nợ khác, và tỷ lệ nợ/thu nhập.

## Mô tả Dataset
Dataset `Cust_Segmentation.csv` chứa thông tin về 850 khách hàng. Cấu trúc dataset bao gồm các cột sau:

- **Customer Id**: Mã định danh duy nhất cho mỗi khách hàng (số nguyên, từ 1 đến 850).
- **Age**: Tuổi của khách hàng (số nguyên, từ 20 đến 56).
- **Edu**: Mức độ học vấn (số nguyên, từ 1 đến 5, đại diện cho các cấp học vấn khác nhau).
- **Years Employed**: Số năm làm việc (số nguyên, từ 0 đến 33).
- **Income**: Thu nhập hàng năm của khách hàng (nghìn USD, từ 13 đến 446).
- **Card Debt**: Số nợ thẻ tín dụng (triệu USD, từ 0.012 đến 20.561).
- **Other Debt**: Số nợ khác (triệu USD, từ 0.046 đến 35.197).
- **Defaulted**: Trạng thái vỡ nợ (0: không vỡ nợ, 1: vỡ nợ, có một số giá trị thiếu).
- **Address**: Địa chỉ của khách hàng (mã hóa dưới dạng chuỗi, ví dụ: NBA001, NBA021,...).
- **DebtIncomeRatio**: Tỷ lệ nợ/thu nhập (phần trăm, từ 0.1 đến 41.3).


### Đặc điểm dataset
- **Số lượng mẫu**: 850 bản ghi.
- **Đặc trưng**: Các cột `Age`, `Income`, `Years Employed`, `Card Debt`, `Other Debt`, và `DebtIncomeRatio` là các giá trị số, được sử dụng làm đặc trưng chính cho phân cụm. Các cột `Edu` và `Defaulted` có thể được sử dụng để phân tích bổ sung nhưng không phải đặc trưng chính trong thuật toán K-Means.
- **Vấn đề tiềm ẩn**:
  - Cột `Defaulted` có giá trị thiếu (NaN), cần được xử lý trong bước tiền xử lý (ví dụ: thay thế bằng giá trị trung bình hoặc loại bỏ).
  - Cột `Address` là chuỗi mã hóa, không được sử dụng trực tiếp trong phân cụm.
  - Một số đặc trưng như `Income` và `DebtIncomeRatio` có phân bố không đều, cần chuẩn hóa để đảm bảo hiệu suất của thuật toán K-Means.

## Cấu trúc thư mục
- **`data/`**:
  - `Cust_Segmentation.csv`: Tệp dữ liệu đầu vào chứa thông tin khách hàng.
- **`results/`**:
  - `du_lieu_ban_dau.png`: Biểu đồ phân bố dữ liệu ban đầu (ví dụ: scatter plot của `Age` và `Income`).
  - `phan_bo_dac_trung.png`: Biểu đồ phân bố của các đặc trưng chính (histogram hoặc boxplot).
  - `kmeans_result.png`: Biểu đồ kết quả phân cụm (scatter plot với các cụm được đánh dấu màu).
- **`K-Mean-Clustering.ipynb`**: File Jupyter Notebook chứa mã nguồn thực hiện toàn bộ quy trình.

## Các thành phần chính của mã nguồn
1. **Tiền xử lý dữ liệu**:
   - Dữ liệu được tải từ Google Drive bằng `pandas`.
   - Xử lý giá trị thiếu trong cột `Defaulted` (thay thế bằng 0 hoặc loại bỏ các bản ghi).
   - Chuẩn hóa các đặc trưng số (`Age`, `Income`, `Years Employed`, `DebtIncomeRatio`) bằng `StandardScaler` từ `scikit-learn` để đảm bảo các đặc trưng có cùng thang đo.
   - Lựa chọn các đặc trưng chính cho phân cụm: `Age`, `Income`, `Years Employed`, `DebtIncomeRatio`.

2. **Áp dụng thuật toán K-Means**:
   - Sử dụng `KMeans` từ `scikit-learn` với số cụm được chọn là 4 (dựa trên phân tích hoặc phương pháp Elbow).
   - Huấn luyện mô hình trên các đặc trưng đã chuẩn hóa.
   - Gán nhãn cụm cho mỗi khách hàng và lưu kết quả vào một cột mới trong dataframe.

3. **Đánh giá và trực quan hóa**:
   - Tạo biểu đồ phân bố dữ liệu ban đầu bằng `matplotlib` hoặc `seaborn` để kiểm tra phân bố của các đặc trưng.
   - Vẽ scatter plot của các cụm (ví dụ: `Age` vs. `Income`) với màu sắc khác nhau cho từng cụm (`Red`, `Green`, `Blue`, `Orange`).
   - Lưu các biểu đồ vào thư mục `results/` dưới dạng file PNG.

4. **Kết quả phân cụm**:
   - **Cụm 0 (Red)**: Khách hàng trung niên, thu nhập trung bình, nợ thấp, nhiều năm kinh nghiệm làm việc.
   - **Cụm 1 (Green)**: Khách hàng trẻ, thu nhập thấp, tỷ lệ nợ cao, ít kinh nghiệm làm việc.
   - **Cụm 2 (Blue)**: Khách hàng trẻ, thu nhập thấp, tỷ lệ nợ thấp, ít kinh nghiệm làm việc.
   - **Cụm 3 (Orange)**: Khách hàng lớn tuổi, thu nhập cao, nợ thấp, nhiều kinh nghiệm làm việc.

## Yêu cầu cài đặt
Cần cài đặt các thư viện Python sau:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

Nếu sử dụng Google Colab, cần kết nối với Google Drive để truy cập dataset:
```python
from google.colab import drive
drive.mount('/content/drive')
```

## Liên hệ
Nếu bạn có thắc mắc hoặc cần hỗ trợ, vui lòng liên hệ qua email: [nductrien.ai@gmail.com].