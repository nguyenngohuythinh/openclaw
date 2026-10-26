<!--
README tiếng Việt cho bản fork OpenClaw.
Dự án gốc: https://github.com/openclaw/openclaw
-->

<p align="center">
  <img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-banner-dark.png" alt="OpenClaw — Trợ lý AI cá nhân" width="900">
</p>

<h1 align="center">🦞 OpenClaw — Trợ lý AI của riêng bạn</h1>

<p align="center">
  <strong>Một trợ lý AI có thể chạy trên máy tính của bạn và kết nối với những ứng dụng nhắn tin bạn đang dùng.</strong>
</p>

<p align="center">
  <a href="https://github.com/openclaw/openclaw"><img src="https://img.shields.io/badge/Dự%20án%20gốc-OpenClaw-6f42c1?style=for-the-badge&logo=github" alt="Dự án gốc"></a>
  <a href="https://docs.openclaw.ai"><img src="https://img.shields.io/badge/Tài%20liệu-Official%20Docs-0ea5e9?style=for-the-badge&logo=readthedocs&logoColor=white" alt="Tài liệu"></a>
  <img src="https://img.shields.io/badge/Ngôn%20ngữ-Tiếng%20Việt-ef4444?style=for-the-badge" alt="Tiếng Việt">
</p>

<p align="center">
  <a href="#-openclaw-là-gì">Giới thiệu</a> •
  <a href="#-cài-đặt-trên-windows">Cài đặt</a> •
  <a href="#-dùng-api-ai-miễn-phí">API miễn phí</a> •
  <a href="#-khởi-động-và-sử-dụng">Sử dụng</a> •
  <a href="#-sửa-lỗi-thường-gặp">Sửa lỗi</a>
</p>

---

## 🌟 OpenClaw là gì?

**OpenClaw** là dự án trợ lý AI mã nguồn mở. Bạn có thể chạy Gateway trên máy tính của mình, chọn nhà cung cấp mô hình AI, rồi kết nối trợ lý với các kênh như Telegram, Discord, WhatsApp và những nền tảng được hỗ trợ.

Hãy hình dung đơn giản:

- 🧠 **Mô hình AI/API** — phần tạo câu trả lời và suy luận.
- 🦞 **OpenClaw Gateway** — bộ phận điều phối trợ lý, phiên trò chuyện, công cụ và kết nối.
- 💬 **Kênh trò chuyện** — nơi bạn nhắn tin với trợ lý.
- 🧰 **Tools, Skills và Plugins** — tính năng bổ sung cho những tác vụ được cấu hình.

> **Lưu ý:** README này là hướng dẫn tiếng Việt dành cho người dùng repo này. OpenClaw gốc được phát triển tại [openclaw/openclaw](https://github.com/openclaw/openclaw). Hãy xem tài liệu chính thức để kiểm tra các thay đổi mới nhất.

## ✨ Điểm nổi bật

| Tính năng | Mô tả |
|---|---|
| 🤖 Nhiều mô hình AI | Chọn nhà cung cấp được hỗ trợ; có thể đổi mô hình khi cần. |
| 💬 Nhiều kênh chat | Kết nối các nền tảng nhắn tin được OpenClaw hỗ trợ. |
| 🖥️ Giao diện điều khiển | Quản lý và trò chuyện qua Control UI trên trình duyệt. |
| 🧠 Bộ nhớ và phiên làm việc | Quản lý ngữ cảnh theo cấu hình của trợ lý. |
| 🧩 Có thể mở rộng | Bổ sung tools, skills và plugins phù hợp. |
| 🔐 Tự cấu hình | Bạn quyết định nhà cung cấp, kênh và thông tin xác thực sử dụng. |

## 🧰 Chuẩn bị trước khi cài

- Máy tính Windows 10/11.
- Kết nối Internet.
- Quyền chạy PowerShell.
- Một tài khoản nhà cung cấp AI nếu muốn dùng API trực tuyến.
- Không chia sẻ API key, token bot hoặc file cấu hình có bí mật lên GitHub.

OpenClaw có thể gọi công cụ trên máy chủ đang chạy nó. Chỉ kết nối những kênh và người dùng bạn tin tưởng; đọc hướng dẫn [bảo mật chính thức](https://docs.openclaw.ai/gateway/security) trước khi mở Gateway ra Internet.

## 🚀 Cài đặt trên Windows

### Cách 1 — Dùng trình cài đặt chính thức (khuyến nghị)

1. Mở **Windows PowerShell**.
2. Chạy lệnh sau để bắt đầu cài đặt:

```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

3. Làm theo các bước hướng dẫn trên màn hình.
4. Khi trình cài đặt yêu cầu cấu hình, chọn nhà cung cấp AI và xác thực theo hướng dẫn của nhà cung cấp đó.

> Chỉ chạy trình cài đặt mà bạn đã kiểm tra và tin tưởng. Nếu muốn xem các phương án cài đặt khác, đọc [tài liệu cài đặt chính thức](https://docs.openclaw.ai/install).

### Cách 2 — Cài bằng npm

Dùng cách này nếu bạn đã cài phiên bản Node.js được OpenClaw hỗ trợ và npm phù hợp:

```powershell
npm install -g openclaw@latest --allow-scripts=openclaw
```

Nếu npm báo tùy chọn `--allow-scripts` không được hỗ trợ, hãy kiểm tra phiên bản npm và làm theo [hướng dẫn cài đặt](https://docs.openclaw.ai/install) tương ứng.

Sau khi cài bằng npm, chạy trình thiết lập:

```powershell
openclaw onboard --install-daemon
```

## 🆓 Dùng API AI miễn phí

OpenClaw là phần mềm; **API của mô hình AI có thể có giới hạn riêng**. Miễn phí thường có nghĩa là có hạn mức sử dụng miễn phí, không phải dùng vô hạn. Hạn mức, mô hình và điều kiện có thể thay đổi theo tài khoản/khu vực.

### 1. Google Gemini API — lựa chọn nên thử đầu tiên

- 🌐 Trang tạo API key: [Google AI Studio](https://aistudio.google.com/app/apikey)
- 💵 Có gói miễn phí cho một số mô hình và hạn mức; xem [bảng giá chính thức](https://ai.google.dev/gemini-api/docs/pricing).
- 🔑 OpenClaw hỗ trợ xác thực bằng API key Gemini.

**Các bước:**

1. Mở Google AI Studio và tạo API key.
2. Giữ key ở nơi riêng tư; không gửi key cho người khác.
3. Trong PowerShell, chạy trình thiết lập OpenClaw:

```powershell
openclaw onboard
```

4. Chọn phương thức xác thực Google Gemini API key nếu được hỏi, rồi nhập key theo hướng dẫn.
5. Xem các mô hình có sẵn và chọn một mô hình được tài khoản của bạn hỗ trợ:

```powershell
openclaw models list
```

**Chú ý:** hạn mức miễn phí không áp dụng cho mọi mô hình hoặc tính năng. Trên trang giá, kiểm tra đúng tên mô hình và mục Free Tier trước khi sử dụng. Không đưa dữ liệu nhạy cảm vào yêu cầu nếu bạn chưa đọc chính sách dữ liệu của nhà cung cấp.

### 2. OpenRouter — thử nhiều mô hình từ một nơi

- 🌐 Trang chủ: [OpenRouter](https://openrouter.ai/)
- 🧾 Danh sách mô hình miễn phí: [Free Models](https://openrouter.ai/collections/free-models)
- 💵 Gói miễn phí có các mô hình được đánh dấu miễn phí, nhưng giới hạn yêu cầu và tốc độ có thể thấp hơn gói trả phí. Xem [bảng giá và giới hạn hiện tại](https://openrouter.ai/pricing).

**Các bước:**

1. Tạo tài khoản và API key tại OpenRouter.
2. Chạy:

```powershell
openclaw onboard
```

3. Chọn OpenRouter làm nhà cung cấp và xác thực theo hướng dẫn.
4. Chạy lệnh sau để xem các mô hình mà cấu hình hiện tại nhận diện được:

```powershell
openclaw models list
```

5. Chọn mô hình miễn phí đang khả dụng trong danh sách. Kiểm tra nhãn giá của mô hình tại trang OpenRouter trước khi dùng.

> **Mẹo:** tên và số lượng mô hình miễn phí thay đổi thường xuyên. Đừng sao chép một model ID cũ từ hướng dẫn trên mạng mà chưa kiểm tra danh mục hiện tại.

### 3. Groq — một lựa chọn khác có hạn mức miễn phí

- 🌐 Trang tạo API key: [Groq Console](https://console.groq.com/keys)
- 📏 Xem giới hạn theo mô hình: [Groq Rate Limits](https://console.groq.com/docs/rate-limits)
- 🔌 OpenClaw có tài liệu tích hợp Groq: [Hướng dẫn Groq của OpenClaw](https://docs.openclaw.ai/providers/groq)

Tạo API key, sau đó chạy `openclaw onboard` và chọn Groq nếu tùy chọn này có trong phiên bản bạn đang dùng. Hạn mức phụ thuộc mô hình và tài khoản; khi vượt giới hạn, API có thể trả lỗi giới hạn tốc độ (`429`).

### Nên chọn API nào?

| Nhu cầu | Nên thử | Ghi chú |
|---|---|---|
| Bắt đầu đơn giản | **Gemini API** | Tạo key qua Google AI Studio; kiểm tra mô hình có Free Tier. |
| Muốn thử nhiều mô hình | **OpenRouter** | Lọc mô hình miễn phí và kiểm tra hạn mức trước khi dùng. |
| Muốn thêm lựa chọn | **Groq** | Hạn mức khác nhau tùy mô hình và tài khoản. |
| Muốn không phụ thuộc API cloud | **Mô hình chạy local** | Có thể dùng Ollama/LM Studio nếu phần cứng đáp ứng; chi phí API có thể bằng 0 nhưng vẫn tốn điện và tài nguyên máy. |

Các dịch vụ trên là những lựa chọn để bắt đầu, không phải cam kết miễn phí vô hạn. Luôn kiểm tra điều khoản, hạn mức và giá hiện tại trên trang chính thức.

## 💬 Khởi động và sử dụng

Sau khi hoàn thành onboarding, kiểm tra Gateway:

```powershell
openclaw gateway status
```

Mở giao diện điều khiển:

```powershell
openclaw dashboard
```

Trình duyệt sẽ mở Control UI nếu cấu hình đã sẵn sàng. Gửi một tin nhắn thử để xác nhận mô hình AI hoạt động.

### Kết nối Telegram hoặc kênh chat khác

1. Mở [danh sách kênh được hỗ trợ](https://docs.openclaw.ai/channels).
2. Chọn kênh bạn muốn dùng và làm theo hướng dẫn chính thức của kênh đó.
3. Cất token bot trong phần cấu hình an toàn, không commit vào repository.
4. Với kênh hỗ trợ ghép đôi (pairing), chỉ phê duyệt người gửi bạn biết và tin tưởng.

Xem thêm: [Getting Started](https://docs.openclaw.ai/start/getting-started).

## 🧯 Sửa lỗi thường gặp

| Lỗi | Cách kiểm tra |
|---|---|
| Lệnh `openclaw` không được nhận diện | Đóng/mở lại PowerShell; kiểm tra cài đặt và PATH. |
| Không xác thực được API | Kiểm tra API key, nhà cung cấp đã chọn và hướng dẫn xác thực tương ứng. |
| Hết hạn mức hoặc lỗi `429` | Đợi hạn mức hồi phục, giảm tần suất gọi hoặc chọn mô hình khác có hạn mức phù hợp. |
| Không mở được Dashboard | Chạy `openclaw gateway status`, rồi xem log và [tài liệu khắc phục sự cố](https://docs.openclaw.ai/help/faq). |
| Kênh chat không phản hồi | Kiểm tra token, quyền bot, trạng thái Gateway và quy trình pairing. |

Nếu vẫn gặp lỗi, hãy tìm thông báo lỗi chính xác trong [FAQ](https://docs.openclaw.ai/help/faq) và tài liệu chính thức. Trước khi chia sẻ log để nhờ hỗ trợ, hãy xóa API key, token, thông tin cá nhân và dữ liệu nhạy cảm.

## 🔐 Bảo mật — đừng bỏ qua

- ❌ Không commit API key, token Telegram/Discord, mật khẩu hoặc file `.env` có bí mật.
- 🔒 Không đăng ảnh chụp màn hình có lộ token hoặc thông tin tài khoản.
- 👥 Không mở quyền sử dụng trợ lý cho người lạ khi chưa hiểu quyền của tools.
- 🌐 Không phơi bày Gateway trực tiếp ra Internet nếu chưa đọc hướng dẫn bảo mật.
- 🧪 Chỉ cài skills/plugins từ nguồn bạn tin tưởng và kiểm tra quyền chúng yêu cầu.
- 📚 Đọc [Security Guide](https://docs.openclaw.ai/gateway/security) và [Sandboxing](https://docs.openclaw.ai/gateway/sandboxing).

## 📚 Tài liệu hữu ích

| Nội dung | Liên kết |
|---|---|
| Trang dự án gốc | [openclaw/openclaw](https://github.com/openclaw/openclaw) |
| Hướng dẫn bắt đầu | [Getting Started](https://docs.openclaw.ai/start/getting-started) |
| Cài đặt | [Installation](https://docs.openclaw.ai/install) |
| Mô hình và nhà cung cấp | [Model Providers](https://docs.openclaw.ai/concepts/model-providers) |
| Kênh chat | [Channels](https://docs.openclaw.ai/channels) |
| Cấu hình Gateway | [Gateway Configuration](https://docs.openclaw.ai/gateway/configuration) |
| Bảo mật | [Security Guide](https://docs.openclaw.ai/gateway/security) |
| Câu hỏi thường gặp | [FAQ](https://docs.openclaw.ai/help/faq) |

## 🤝 Đóng góp và giấy phép

Để đóng góp mã nguồn, hãy đọc hướng dẫn tại repository gốc: [CONTRIBUTING.md](https://github.com/openclaw/openclaw/blob/main/CONTRIBUTING.md).

OpenClaw được phân phối theo giấy phép MIT tại dự án gốc. Hãy đọc tệp [LICENSE](LICENSE) trong repository này để biết chính xác điều khoản áp dụng cho bản mã nguồn bạn đang sử dụng.

---

<p align="center">
  <strong>🦞 Bắt đầu nhỏ, bảo mật trước, rồi mở rộng trợ lý theo nhu cầu của bạn.</strong>
  <br>
  <sub>Tài liệu API miễn phí và hạn mức có thể thay đổi — hãy kiểm tra nguồn chính thức trước khi cấu hình.</sub>
</p>
