---
title: "Event 2"
date: 2026-05-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Báo cáo tham dự: FCAJ Community Day / AWS Community Day

**Sự kiện:** FCAJ Community Day (AWS Community Day)  
**Thời gian:** 23/05/2026  
**Địa điểm:** Không gian FCAJ (sảnh chính + tầng 36 xem stream)  
**Vai trò:** Người tham dự

## Tổng quan

Community day cả ngày với các phiên về AI, platform engineering, Amazon Quick agents, CloudFront pricing, dự án hackathon, độ xác định của LLM và hệ thống multi-agent đánh giá tín dụng startup tại ngân hàng.

## Diễn giả

| # | Diễn giả | Chức danh / tổ chức |
|---|----------|---------------------|
| 1 | **Nguyễn Gia Hưng** | Head of Solution Architect, **AWS Vietnam**; Founder **FCAJ** |
| 2 | **Tịnh Trương** | Platform Engineer, **GothamX** |
| 3 | **Hải Anh** | **Pacific Vietnam** |
| 4 | **Nguyễn Hấn Thịnh** | DevOps Engineer (cựu học viên FCAJ) |
| 5 | **Uyển** | Đội thắng hackathon — **UTMorph** (cùng **Thảo**, **MCH**) |
| 6 | **Thảo** | Đồng trình bày, **UTMorph** |
| 7 | **Đức Đào** | Engineer |
| 8 | **Vy Lâm** | Engineer, **VPBank** (~2 năm) |

---

## Nội dung trình bày

### Nguyễn Gia Hưng — AI, nghề nghiệp & xây dựng sản phẩm thực

AI làm rẻ chi phí sản xuất phần mềm → nhu cầu phần mềm tăng (hiệu ứng Jevons) → cầu engineer **ship, vận hành và sửa** sản phẩm AI-assisted tăng. Tuyển dụng ngắn hạn khó do macro AI, nhưng cầu dài hạn cho người build vẫn lớn tại VN nhờ outsourcing toàn cầu.

**Đại học một mình chưa đủ:** (1) nền tảng kỹ thuật vững, (2) use case ngành thật, (3) **sản phẩm** chứ không chỉ demo — thứ show được với director ngày đầu. AI nhảy bậc ~4 tháng/lần; trì hoãn học kỹ năng khiến thị trường khó hơn. Ngân hàng vẫn tuyển Dev team lớn nhưng ngày càng cần platform/operations engineer.

### Tịnh Trương — Context engineering & platform engineering (GothamX)

Platform engineer: tiến hóa từ DevOps ticket sang nền tảng self-service an toàn ở quy mô lớn.

**Context là chìa khóa:** Một chat trộn du lịch, nghề nghiệp và code làm model rối — tách session, scope context có chủ đích. Với banking/fintech, cần **context nội bộ** (blueprint, chuẩn công ty). Giữ ~70% session cho một việc; tiếp nối context thay vì restart.

**Nghề nghiệp:** Trong khóa 120–140 người, engineer **áp dụng AI với context domain** nổi bật khi phỏng vấn. Đề cập AI second brain (Obsidian).

### Hải Anh — Amazon Quick & agent BI (Pacific Vietnam)

Kinh nghiệm trình bày tại **AWS Summit Singapore** và **Silicon Valley** — giải bài toán người dùng thật hơn seniority.

**Vấn đề:** Manager mất nhiều thời gian tổng hợp báo cáo tuần từ file rải rác.

**Amazon Quick / Quick Desktop:** Tích hợp Microsoft 365, Google, Teams, Gmail… để inbox dữ liệu và nhờ agent phân tích, tạo dashboard, tóm tắt họp. **Agent = LLM + hành động (MCP/tools).** Doanh nghiệp cần shared responsibility bảo mật và quản trị dữ liệu.

### Nguyễn Hấn Thịnh — CloudFront flat-rate pricing

Trọng tâm **CloudFront flat-rate pricing** — giải quyết hóa đơn CDN pay-as-you-go khó dự báo khi traffic spike (viral, DDoS).

**Gói flat-rate** (Free/Pro/Business/Premium): gói WAF, Route 53, credit S3; **overage throttle băng thông**. Một distribution/plan/website; Terraform/CDK có thể mặc định classic pricing.

**Chiều sâu kỹ thuật:** PoP toàn cầu + backbone, bảo vệ DDoS nhanh hơn Shield mặc định, tối ưu chi phí S3/ALB, nén, HTTPS/ACM, VPC origin, multi-tier cache, HTTP/3, tái sử dụng TCP, **CloudFront Functions** tại edge.

### Uyển & Thảo — Hành trình hackathon UTMorph (36 giờ)

Đội **UTMorph** (Uyển, Thảo, MCH) thắng **hackathon quốc gia 36 giờ** (~2 tháng trước sự kiện).

**Ý tưởng:** AI sinh UI nhưng chỉnh màu/khoảng cách phải regenerate — xây editor tương tác trực tiếp UI (kéo component, sửa CSS, lịch sử phiên bản, publish link HTML).

**Bài học:** Bắt đầu từ nỗi đau hàng ngày; cắt scope khi thời gian cố định; token limits và mệt gần deadline là rủi ro thật; đồng đội quen thế mạnh nhau ship nhanh hơn.

**Kiến trúc (Thảo):** Serverless AWS; **pipeline 3 agent** — vision → layout/CSS → code theo design system; demo dashboard + visual editor. Chia việc theo thế mạnh, sync định kỳ; quản lý sức khỏe suốt 36 giờ.

### Đức Đào — LLM temperature, độ xác định & thiết kế production

Đức Đào trình bày nghiên cứu đã sharing nội bộ công ty về việc **temperature = 0 không đảm bảo output LLM giống hệt** trên API hosted.

**Cách model chọn token:** Chấm điểm logits, xếp hạng, sampling — temperature, top-p, top-k điều khiển ngẫu nhiên vs. sáng tạo.

**Hiểu lầm:** Team giả định T=0 = deterministic cho automation. Thực tế **tối ưu inference** (kernel, batching, provider) gây variance — demo trên **Bedrock** hai model T=0 cho output khác nhau cùng prompt.

**Giảm thiểu:** voting nhiều lần chạy; self-host khi cần kiểm soát; JSON mode; thiết kế downstream chịu biến thể format; thử T≈0.1 thay vì 0; đọc **tài liệu chính thức model** (Claude 3.x) trước khi tune hyperparameter.

**Kết luận:** LLM là engine xác suất — thiết kế chịu variance, test kỹ, không assume chuỗi cố định trong production.

### Vy Lâm — Multi-agent đánh giá tín dụng startup (VPBank)

Vy Lâm mở bằng tư duy kinh doanh: **Ai dùng? Vấn đề gì? Vì sao giải pháp của bạn? Khi nào phù hợp?** (How đã được các phiên trước cover.)

**Use case:** Thẩm định tín dụng **startup** trong bối cảnh kinh tế startup VN (2024–2026). Mô hình truyền thống cần báo cáo tài chính nhiều năm, lịch sử tín dụng, tài sản thế chấp — startup thường chỉ có traction, team, IP, pitch deck.

**Vì sao multi-agent:** Nhiều loại tài liệu và góc chuyên gia; giới hạn context; một agent không thể đóng vai analyst, market research, đánh giá team và risk officer cùng lúc.

**Vai agent:** Orchestrator (“chủ tọa hội đồng tín dụng”), financial analyst, market researcher, đánh giá team/founder, **risk & compliance** (then chốt ngân hàng).

**Thực tế enterprise (2 năm VPBank):** MCP mở attack surface — tool phải duyệt; Ollama local có thể bị chặn. Guardrails: chống prompt injection, lọc I/O, rotate key, **audit trail** cho quyết định con người. Knowledge transfer từ credit officer senior quan trọng như RAG. Sự cố chatbot: paste ChatGPT vào production không qua review. Tuyển dụng: **nền backend/software engineering** + AI an toàn.

**Lộ trình:** POC → SIT → UAT → pilot → scale; trình bày **ROI**. Triển khai: containerize → **AgentCore** trên AWS; Cognito/JWT/OIDC.

---

## Bài học rút ra

- Context engineering và tư duy production phân biệt dùng AI sở thích vs. kỹ năng tuyển dụng.
- CloudFront flat-rate kiểm soát chi phí workload public-facing.
- Hackathon dạy scope, teamwork, pitch demo-first.
- AI enterprise bị ràng buộc compliance, audit, ROI.
- LLM workflow phải assume non-determinism kể cả T=0.

## Cảm nhận cá nhân

Sự kiện kết nối tinh thần FCAJ với phiên thực dụng: từ CloudFront billing đến góc nhìn thẳng thắn VPBank về multi-agent dưới quy định ngân hàng. Thông điệp lặp lại: build sản phẩm thật, hiểu những gì mình ship, nói giá trị kinh doanh — không chỉ tên dịch vụ.
