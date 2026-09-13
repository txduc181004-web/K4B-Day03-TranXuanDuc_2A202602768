# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Trần Xuân Đức  
> **Mã Sinh Viên / Mã Học viên:** 2A202602768  
> **Chủ đề Lựa chọn:** Trợ lý Học vụ Sinh viên VinUni  

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | 4 / 5 | Người dùng có thể yêu cầu tra cứu sinh viên, suy luận cố vấn học tập, rồi tiến hành đặt lịch tư vấn; đây là bước nhiều lượt xử lý. |
| **2. Tool Interaction** | 5 / 5 | Hệ thống cần dùng các công cụ `academic_query` và `schedule_appointment` qua MCP Server để truy vấn dữ liệu và cập nhật lịch hẹn. |
| **3. Dynamic Decision** | 4 / 5 | Agent xử lý luồng điều khiển theo phản hồi từ tool: tìm thấy mã SV thì mới tiếp tục đặt lịch; nếu không tìm thấy thì cần trả lời NOT_FOUND. |
| **4. Long Horizon Goal** | 4 / 5 | Nhiệm vụ về học vụ sinh viên có thể kéo dài qua nhiều bước: tra cứu, suy luận cố vấn, đặt lịch và tổng hợp lời phản hồi. |
| **TỔNG ĐIỂM AGENTIC FIT** | **17 / 20** | *Nếu tổng điểm > 12/20: Bài toán rất phù hợp triển khai Agentic System.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (KẾT QUẢ THỰC TẾ TỪ SUITE ĐANG CHẠY)

> ⚠️ **LƯU Ý KIỂM THỬ THỰC TẾ:** File `.env` hiện đang chứa `GEMINI_API_KEY` nhưng bản ghi log thực tế cho thấy Google live API không ổn định vì `503 UNAVAILABLE` / `429 RESOURCE_EXHAUSTED` và hệ thống đã tự động chuyển sang `MockOfflineProvider`. Từ đó, phần trace log cuối cùng trong repo được sinh từ trạng thái fallback mock, không phải từ một lời đáp lời live hoàn toàn chính xác.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` mà suite đã ghi thực tế:

```json
[
  {
    "step": 1,
    "query": "quy chế đặt lịch",
    "action_type": "FINAL_ANSWER",
    "thought": "Câu hỏi chung về quy chế học vụ, trả lời trực tiếp không cần gọi Tool.",
    "output": "[Mock Agent Response]: Xin chào! Quy chế học vụ VinUni yêu cầu sinh viên tích lũy tối thiểu 120 tín chỉ và duy trì GPA trên 2.0 để tốt nghiệp.",
    "latency_ms": 5294.96
  }
]
```

> Lưu ý rõ ràng: đây là trace log của sự kiện test suite đã chạy trong trạng thái fallback mock. Nếu key Google có quota/billing hợp lệ và model được chọn đúng, hệ thống sẽ trả về `tool_call`/`text` sinh live theo định dạng Gemini/GenAI.

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [x] Đã cấu hình `GEMINI_API_KEY` trong `.env` và dùng đúng interpreter `.venv` để thực thi.
- [x] Đã đồng bộ `LLM_MODEL` sang `gemini-flash-latest` và giữ list fallback `gemini-flash-lite-latest`, `gemini-3.6-flash` trong mã nguồn [src/providers.py](src/providers.py).
- **Tổng số Test Cases đã chạy thành công:** 5 / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** 5 lượt (theo chuỗi test suite mô phỏng `academic_query` và `schedule_appointment`).
- **Kết quả trace log:** `docs/trace_waterfall.json` đã được lưu với số lượng sự kiện thực tế hiện có; file đang phản ánh trạng thái fallback mock khi Google API trả `503`/`429`.
- **Kết quả đẩy Repo nộp bài:** [x] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!

> ⚠️ **PHỤ LỤC THEO DÕI QUOTA/DEMAND:** Lỗi `429 RESOURCE_EXHAUSTED` và `503 UNAVAILABLE` không phải là lỗi cấu trúc Python; đó là trạng thái API key Google đang bị hạn quota hoặc model đang quá tải. Muốn đạt live answer đầy đủ, cần cấp lại key / billing / quota hoặc đổi sang model có truy cập hợp lệ trên project Google tương ứng.
