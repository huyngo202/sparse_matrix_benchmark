cmake_minimum_required(VERSION 3.10) # Yêu cầu phiên bản CMake tối thiểu

project(SparseMatrixBenchmark VERSION 1.0 LANGUAGES CXX) # Đặt tên dự án và ngôn ngữ

set(CMAKE_CXX_STANDARD 17) # Sử dụng tiêu chuẩn C++17 (hoặc 11, 14, 20)
set(CMAKE_CXX_STANDARD_REQUIRED True) # Bắt buộc sử dụng chuẩn này

# Tìm các file nguồn
# Thêm các file .cpp khác vào đây khi bạn tạo chúng
set(SOURCES
        src/main.cpp
        src/formats/coo.cpp
        src/formats/csr.cpp
        src/formats/ell.cpp
        src/utils/mtx_reader.cpp
)

# Tạo file thực thi
add_executable(benchmark ${SOURCES})

# (Optional) Thêm các thư viện cần link sau này (ví dụ: cho HDF5, threading, etc.)
# target_link_libraries(benchmark PRIVATE ...)

# In ra đường dẫn file thực thi sau khi build xong (tiện lợi)
message(STATUS "Executable will be built in: ${CMAKE_BINARY_DIR}")