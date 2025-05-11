# Phân Cụm Khách Hàng bằng K-Means

## Giới thiệu
Dự án sử dụng thuật toán K-Means để phân cụm khách hàng từ tệp `Cust_Segmentation.csv`, nhằm phân nhóm dựa trên tuổi, thu nhập, nợ thẻ tín dụng, và các đặc trưng khác.

## Cấu trúc thư mục
- `data/`
  - `Cust_Segmentation.csv`: Dữ liệu đầu vào.
- `results/`
  - `du_lieu_ban_dau.png`: Phân bố dữ liệu.
  - `phan_bo_dac_trung.png`: Phân bố đặc trưng.
  - `kmeans_result.png`: Kết quả phân cụm.
- `K-Mean-Clustering.ipynb`: Mã nguồn Jupyter Notebook.

## Yêu cầu
Cần các thư viện Python:
- pandas
- numpy
- matplotlib
- seaborn

Cài đặt:
```bash
pip install pandas numpy matplotlib seaborn
```

## Hướng dẫn sử dụng
1. **Chuẩn bị**:
   - Đặt `Cust_Segmentation.csv` vào `data/` trên Google Drive.
   - Kết nối Google Drive trong Google Colab.

2. **Thực thi**:
   - Mở `K-Mean-Clustering.ipynb`.
   - Chạy các cell để tải dữ liệu, tiền xử lý, áp dụng K-Means, và tạo biểu đồ.

3. **Kết quả**:
   - Biểu đồ lưu tại `results/`.
   - Tệp `results.zip` chứa các hình ảnh.

## Dữ liệu
`Cust_Segmentation.csv` (850 bản ghi):
- `Customer Id`: Mã khách hàng.
- `Age`: Tuổi.
- `Edu`: Học vấn.
- `Years Employed`: Năm làm việc.
- `Income`: Thu nhập.
- `Card Debt`: Nợ thẻ.
- `Other Debt`: Nợ khác.
- `Defaulted`: Vỡ nợ (0/1, có giá trị thiếu).
- `Address`: Địa chỉ (mã hóa).
- `DebtIncomeRatio`: Tỷ lệ nợ/thu nhập.

## Kết quả phân cụm
K-Means dựa vào các đặc trưng Age, Income, Years Employed, DebtIncomeRatio và phân thành 4 cụm như sau:  
- **Cụm 0 (Red)**: Trung niên, thu nhập trung bình, nợ thấp, có nhiều năm kinh nghiệm
- **Cụm 1 (Green)**: Trẻ, thu nhập thấp, tỉ lệ nợ cao, có ít năm kinh nghiệm
- **Cụm 2 (Blue)**: Trẻ, thu nhập thấp, tỉ lệ nợ thấp, có ít năm kinh nghiệm
- **Cụm 3 (Orange)**: Lớn tuổi, thu nhập cao, ít nợ, có nhiều năm kinh nghiệm


## Tác giả
Nếu bạn có thắc mắc hoặc cần hỗ trợ, vui lòng liên hệ qua email: [nductrien.ai@gmail.com].