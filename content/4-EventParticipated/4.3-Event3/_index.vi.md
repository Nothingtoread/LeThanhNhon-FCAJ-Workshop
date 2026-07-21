---
title: "Event 3"
date: 2026-06-27
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Báo cáo tham dự: FCAJ Community Day

**Sự kiện:** FCAJ Community Day  
**Thời gian:** 27/06/2026  
**Địa điểm:** Không gian FCAJ (tầng 26 & 36, livestream YouTube)  
**Vai trò:** Người tham dự

## Tổng quan

Community day hàng tháng của FCAJ với diễn giả từ đối tác AWS và startup. Các phiên gồm nghề nghiệp cloud, agentic AI vận hành, voice AI tiếng Việt, AWS DevOps Agent, Amazon Quick cho HR và tích hợp MCP private bảo mật cho Quick doanh nghiệp.

## Diễn giả

| # | Diễn giả | Chức danh / tổ chức |
|---|----------|---------------------|
| 1 | **Steve Trần** | Founder, **CloudThinker** |
| 2 | **Hiếu Nghị** | **Renova Cloud**; AWS Community Builder |
| 3 | **Kiệt** | **Student Video Group** |
| 4 | **Trung** | Founder & CEO, **R AI** |
| 5 | **Nguyên Nguyễn** | Cloud Engineer, **Cloud Kinetics** |
| 6 | **Bảo** | Cloud Engineer, **Cloud Kinetics** |
| 7 | **Trường Anh (Wayne)** | AI Solutions, **Noventis** |
| 8 | **Minh Anh** | Solutions team, **Noventis** |
| 9 | **Toàn Nguyễn** | **AWS Security Builder** |
| 10 | **Hiếu Nghị** | **Renova Cloud** (phiên cuối, cùng Toàn Nguyễn) |

---

## Nội dung trình bày

### Steve Trần — Hành trình nghề nghiệp & nền tảng agentic CloudThinker

Steve chia sẻ lộ trình từ IT contact center (reboot server on-prem lúc 19 tuổi), thi Azure fail nhiều lần, chuyển sang AWS nhờ tài liệu rõ ràng, lấy chứng chỉ Developer/SA trong ~1 năm thời COVID cloud boom (2020–2021). ~4 năm: IT engineer FPT (dự án sân bay) → Solution Architect AWS Vietnam. Nhấn mạnh dự đoán nhu cầu cloud và học liên tục khi đi làm.

**AI & tuyển dụng:** Nhiều công ty tạm dừng tuyển junior hoặc chỉ tuyển senior làm việc tốt với AI. Khuyên thực tập/thử việc sớm để tích lũy kinh nghiệm trước khi tốt nghiệp.

**Bài toán CloudThinker:** Doanh nghiệp lên cloud → độ phức tạp vận hành tăng (DevOps/SRE/SOC, observability tool) nhưng “nợ công nghệ” legacy vẫn phục vụ hàng triệu user. AI **hỗ trợ** engineer giỏi trên hạ tầng critical — downtime tính bằng phút, mất tiền lớn.

**Nền tảng agentic (4 trụ):**
1. **Incident** — điều tra AI tính bằng phút vs. con người tính giờ (ví dụ lỗi payment ngân hàng).
2. **AI code review** — coding nhanh hơn nhưng QA/automation test chưa theo kịp; leadership đầu tư SDLC lớn nhưng throughput không đổi.
3. **FinOps** — tối ưu chi phí vẫn thủ công nhiều; AI hiểu AWS + tài chính hỗ trợ FinOps (khách hàng chuyển headcount FinOps sang product).
4. **Security** — pentest liên tục vs. quý/năm; đánh giá infra, code, logging. Giúp squad dev không có DevOps embedded provision/debug môi trường trong vài phút.

Thảo luận **single-agent vs. multi-agent** và bài học startup: validate bài toán khách hàng thật, map ý tưởng vào nhu cầu doanh nghiệp.

### Hiếu Nghị, Kiệt & Trung — Voice AI cho doanh nghiệp Việt Nam

**Hiếu Nghị (Renova Cloud):** Dữ liệu và model giọng nói tiếng Việt khan hiếm so với tiếng Anh — cơ hội research, thi đấu và theo đuổi nghề voice.

**Hai kiến trúc:** speech-to-speech (audio in/out) vs. pipeline 3 bước STT → LLM → TTS (Viettel *098#).

**Kiệt (Student Video Group):** Demo voice agent trên **Bedrock AgentCore** + knowledge base, trả lời câu hỏi sản phẩm Apple (demo gặp sự cố mic).

**Trung (CEO R AI):** Voice production cho ngân hàng VN (VPBank, VIP):
- Model speech-to-speech toàn cầu thiên tiếng Anh; tiếng Việt là **low-resource language**.
- Ngân hàng cần **kiểm soát text** trước TTS, **tool calling** (khóa thẻ sau thu thập CCCD) — speech-to-speech hạn chế.
- **Engineering:** stream end-to-end, detect giới tính cho *anh/chị*, **ngắt lời / barge-in** (biết khách dừng giữa số điện thoại), audit log, versioning prompt, knowledge base, **handoff sang người** khi AI không xử lý được.
- **Giọng vùng miền:** train STT/TTS ~10–20% giọng miền; từ vựng địa phương nặng vẫn khó; một số use case nhắc nợ cố ý dùng giọng miền nhẹ.

### Nguyên Nguyễn & Bảo — AWS DevOps Agent (Cloud Kinetics)

**Vấn đề:** Điều tra sự cố thủ công — telemetry phân mảnh (CloudWatch, X-Ray…), silo kiến thức, context switching, **MTTD/MTTR** cao, mất liên kết log.

**AWS DevOps Agent:** Tự động điều tra khi trigger (alert, PagerDuty, chat), đề xuất mitigation, học dần qua incident.

**Sáu trụ:** context learning (agent space, topology ~300 relationship sau ~15 phút), control (IAM/tag), integration (MCP mở rộng), collaboration (web, Slack, ServiceNow), cost theo **thời gian chạy** (~$0.0083/giây), workflow 4 bước (phân loại → điều tra giả thuyết → mitigate chỉ đề xuất → cải thiện phòng ngừa).

**Demo (Bảo):** E-commerce ECS + ALB; mô phỏng DDoS; agent tiếng Việt tìm root cause, đề xuất stop task — app phục hồi. **Case study:** đại học online ~200k học sinh giảm xử lý sự cố từ ~2 giờ xuống ~28 phút (~77% MTTR) với Datadog + DevOps Agent.

**Điều kiện:** observability trưởng thành, hệ thống đa service; agent chỉ recommend — người approve và execute.

### Trường Anh & Minh Anh — AI, HR & Amazon Quick (Noventis)

**Trường Anh (Wayne):** Vào FCAJ 12/2024 từ “nghe như vịt”, phát triển đến gặp khách hàng nhờ cộng đồng — nghề nghiệp không chỉ kỹ thuật mà còn con người (HR).

**Minh Anh — thách thức HR thời AI:** Sàng lọc CV thủ công bỏ lỡ talent; đánh giá chủ quan; time-to-hire 1–2 tháng; tuyển sai làm trễ dự án; rủi ro upload dữ liệu ứng viên lên AI public.

**Amazon Quick:** Agent biến câu trả lời thành hành động; kết nối M365, Google, SharePoint, Jira, GitHub, S3, DB, MCP tùy chỉnh; model Bedrock (Nova, Claude); Local Zone VN.

**Trường Anh:** Custom agent (tuyển dụng, policy, sales, research); research nội bộ + web; Quick BI; flows/automate; spaces phân quyền.

**Demo HR:** Ingest CV từ LinkedIn, TopCV, email, HR system qua MCP → screening AI theo JD → lên lịch phỏng vấn → email → pipeline. Skill **HR Talent Review Assistant** từ markdown; chấm 6 CV theo JD Junior Cloud Engineer (technical 40%, problem-solving 25%, communication 15%…); báo cáo HTML; board tracking vi-code. Khuyên optimize CV cho JD vì screening ngày càng dùng AI.

### Toàn Nguyễn & Hiếu Nghị — MCP private bảo mật cho Amazon Quick

**Nghị (Renova):** Quick trên internet kết nối bên thứ ba cần đường riêng tư cho enterprise.

**Toàn Nguyễn (AWS Security Builder):** MCP public — rủi ro DDoS, MITM, vi phạm zero-trust/residency. **Giải pháp:** MCP server **private subnet**; **VPC connection** + interface endpoint; DNS nội bộ Route 53 Resolver; **ALB** + TLS (ACM); **Cognito** auth. Demo: DNS public không resolve; từ bastion trong VPC, Quick query MCP real-time ECS/latency — traffic trên mạng private AWS.

**Chi phí (Nghị):** ~$250–350/tháng baseline (Resolver ~$180+, ALB ~$32+, EC2, Secrets Manager, data transfer) — cần sizing theo khách hàng.

---

## Bài học rút ra

- Vai trò vận hành cloud vẫn critical; AI hỗ trợ engineer senior, không thay accountability production.
- Voice AI tiếng Việt cần pipeline, streaming và UX locale (giới tính, ngắt lời, accent).
- DevOps Agent phù hợp tổ chức observability trưởng thành, nén MTTR với human-in-the-loop.
- Amazon Quick + MCP private cho enterprise có quy định bảo mật.
- Thực tập và FCAJ đẩy nhanh chuyển từ sinh viên sang practitioner.

## Cảm nhận cá nhân

Community day kết nối chiến lược nghề nghiệp (Steve Trần), agent kỹ thuật sâu (voice, DevOps, Quick security) và automation HR hướng kinh doanh. Thông điệp xuyên suốt: hiểu ràng buộc production — bảo mật, chi phí, phê duyệt con người — và thiết kế AI là bộ tăng tốc trong guardrail đó.
