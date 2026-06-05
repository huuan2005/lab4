The Zynq Book Tutorials - Tutorial 4: IP Creation

---

## Nội dung thực hành

### Exercise 4A - Creating IP in HDL

Tạo custom IP core dùng ngôn ngữ mô tả phần cứng (Verilog), tích hợp giao tiếp AXI-Lite để điều khiển LED trên board Zynq thông qua phần mềm chạy trên PS.

**Các bước thực hiện:**
- Tạo Vivado project mới (`led_controller`)
- Dùng **Create and Package IP Wizard** để tạo AXI4-Lite IP template
- Chỉnh sửa file VHDL (`led_controller_v1_0_S00_AXI.v` và `led_controller_v1_0.v`) để thêm port `LEDs_out`
- Repackage IP và thêm vào IP Catalog
- Tạo Block Design (`led_test_system`), kết nối LED Controller với Zynq Processing System
- Thêm XDC constraints file để map port `LEDs_out` ra chân vật lý trên board
- Generate Bitstream, Export Hardware và Launch SDK
- Tạo C application để điều khiển LED từ Zynq PS
- Chạy thử nghiệm trên phần cứng, xác nhận LED hoạt động đúng

**Cấu trúc thư mục:**
```
Exercise4A_Vivado_IP/
├── block_design/        # Block design files (.bd)
├── constraints/         # XDC constraints file (led_constraints.xdc)
├── screenshots/         # Ảnh chụp màn hình các bước thực hành
├── sdk/                 # SDK project (C application điều khiển LED)
└── src/                 # VHDL source files (led_controller IP)
```

---

### Exercise 4B - Creating IP in MathWorks HDL Coder

> **Không thực hiện** 

---

### Exercise 4C - Creating IP in Vivado HLS

Tạo IP core cho bộ **Numerically Controlled Oscillator (NCO)** từ mã nguồn C++ sử dụng Vivado HLS, sau đó export thành IP block tương thích với IP Integrator.

**Các bước thực hiện:**
- Tạo Vivado HLS project mới (`hls_nco`)
- Thêm source file `nco.cpp` (dùng thư viện `ap_fixed.h` cho kiểu dữ liệu fixed-point)
- Thêm testbench file `nco_tb.cpp`
- Chạy **C Simulation** để kiểm tra chức năng thuật toán NCO
- Thêm **HLS Directives** để định nghĩa giao tiếp AXI-Lite slave:
  - `HLS INTERFACE s_axilite` cho function `nco`
  - `HLS INTERFACE ap_ctrl_none` để loại bỏ control signals không cần thiết
  - `HLS INTERFACE s_axilite` cho `sine_sample` và `step_size`
- Chạy **C Synthesis**
- Export RTL dưới dạng **IP Catalog** (format Verilog)

**Kết quả:**
- C Simulation hoàn thành thành công (0 errors)
- IP core được export tại `solution1/impl/ip/`
- IP tương thích với Vivado IP Catalog, sẵn sàng tích hợp vào IP Integrator

**Cấu trúc thư mục:**
```
Exercise4C_HLS/
├── directives/          # HLS directives file (directives.tcl)
├── export_ip/ip/        # Exported IP package
├── screenshots/         # Ảnh chụp màn hình các bước thực hành
├── src/                 # C++ source (nco.cpp, nco_tb.cpp)
└── tb/                  # Testbench files
```

---

## Công cụ sử dụng

| Công cụ | 
|---|
| Vivado Design Suite | 
| Vivado HLS | 
| Xilinx SDK | 
