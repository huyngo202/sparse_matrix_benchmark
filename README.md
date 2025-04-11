# Đo lường Hiệu năng Ma trận Thưa cho Dữ liệu Sinh học (Phiên bản CPU)

## Mục tiêu Dự án

Dự án này nhằm mục đích đo lường hiệu năng (chủ yếu là tốc độ tính toán) của các định dạng lưu trữ ma trận thưa khác nhau trên CPU khi xử lý các bộ dữ liệu sinh học lớn và thưa, chẳng hạn như ma trận biểu hiện gen từ thí nghiệm giải trình tự đơn bào (scRNA-seq). Dự án được triển khai bằng C++ và CMake.

## Các Định dạng Đã Hiện thực

Hiện tại, các định dạng ma trận thưa sau đã được triển khai:

1.  **COO (Coordinate List):** Định dạng đơn giản lưu trữ các bộ `(hàng, cột, giá trị)`. Thường dùng để tải dữ liệu ban đầu.
2.  **CSR (Compressed Sparse Row):** Lưu trữ `giá_trị`, `chỉ_số_cột`, và `con_trỏ_hàng`. Tối ưu cho các thao tác trên hàng.
3.  **ELL (ELLPACK):** Sử dụng các mảng dày đặc dựa trên số lượng phần tử khác không tối đa trên mỗi hàng (`k`). Có thể hiệu quả nhưng tốn bộ nhớ nếu `k` lớn hoặc không đồng đều.


## Thao tác Chính Được Đo lường

Benchmark chính tập trung vào phép toán **Nhân Ma trận Thưa-Vector (SpMV): `y = A * x`**. Các chỉ số hiệu năng bao gồm:

*   **Thời gian Chuyển đổi:** Thời gian cần thiết để chuyển đổi dữ liệu COO ban đầu sang định dạng CSR và ELL (tính bằng mili giây).
*   **Thời gian Thực thi SpMV:** Thời gian trung bình cho mỗi phép toán SpMV qua nhiều lần lặp (tính bằng mili giây).
*   **GFLOPS Ước tính:** Số phép toán dấu phẩy động trên giây (Giga) gần đúng đạt được trong quá trình SpMV.

Thông tin cơ bản về mỗi ma trận (kích thước, số phần tử khác không) cũng được in ra.

## Yêu cầu Hệ thống

*   **Trình biên dịch C++:** Hỗ trợ tiêu chuẩn C++17 (ví dụ: GCC 7+, Clang 5+).
*   **CMake:** Phiên bản 3.10 trở lên.
*   **Git:** (Tùy chọn).

## Xây dựng Dự án

1.  **Clone repo (nếu có):** `git clone <url>` rồi `cd sparse_matrix_benchmark`
2.  **Tạo thư mục build:** `mkdir build && cd build`
3.  **Cấu hình:** `cmake ..`
4.  **Biên dịch:** `cmake --build .` (hoặc `make` trên Linux/macOS)

    Lệnh này sẽ tạo file thực thi `benchmark` trong thư mục `build`.

## Chạy Benchmark

**Sử dụng:**

```bash
./benchmark <đường_dẫn_đến_file.mtx> [số_lần_lặp_spmv]