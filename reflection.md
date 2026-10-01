# Day 14 — Reflection

## Evaluation Report & Failure Analysis

Dùng kết quả thật trong `artifacts/benchmark_results.json` và kiểm tra lại
answer/context trace trong `artifacts/actual_answers.json` trước khi kết luận.

---

## 1. Benchmark Results Summary

**Overall pass rate:** ____%

| Metric | Average | Min | Max | Nhận xét |
|---|---:|---:|---:|---|
| Context Recall | | | | |
| Context Precision | | | | |
| Faithfulness | | | | |
| Relevance | | | | |
| Completeness | | | | |
| Overall Score | | | | |

**Score interpretation**

- Metrics/cases ở mức Good (0.8–1.0): ____
- Metrics/cases ở mức Needs Work (0.6–0.8): ____
- Metrics/cases ở mức Significant Issues (<0.6): ____

**Failure type distribution**

| Failure Type | Count | Percentage |
|---|---:|---:|
| hallucination | | |
| irrelevant | | |
| incomplete | | |
| off_topic | | |
| refusal | | |

**Chẩn đoán tổng quan:** Vấn đề chính nằm ở retrieval, generation hay cả hai?
Dùng ít nhất hai metrics để bảo vệ kết luận.

> *Câu trả lời:*

---

## 2. Top 3 Worst Failures — 5 Whys

Phân loại failure trước khi đề xuất fix. Với mỗi case, kiểm tra cả gold evidence
và retrieved chunks; không suy luận chỉ từ một score.

### Failure 1

**ID và question:**

> *Điền:*

**Expected answer:**

> *Điền:*

**Actual answer:**

> *Điền:*

**Scores:** Context Recall: ____ | Context Precision: ____ | Faithfulness: ____ |
Relevance: ____ | Completeness: ____ | Overall: ____

**Evidence inspection:** Retriever lấy đúng/thiếu/thừa chunks nào?

> *Câu trả lời:*

| Level | Question | Answer |
|---|---|---|
| Symptom | Vấn đề quan sát được là gì? | |
| Why 1 | Tại sao symptom xảy ra? | |
| Why 2 | Tại sao nguyên nhân trên xảy ra? | |
| Why 3 | Tại sao vấn đề đó chưa được ngăn chặn? | |
| Why 4 | Tại sao cơ chế hiện tại chưa phát hiện hoặc xử lý được? | |
| Why 5 | Root cause có thể hành động được là gì? | |

**Root cause từ `find_root_cause()`:**

> *Paste output:*

**Bạn đồng ý hay không? Dẫn evidence từ trace:**

> *Câu trả lời:*

**Proposed fix cụ thể:**

> *Câu trả lời:*

### Failure 2

**ID và question:**

> *Điền:*

**Expected answer:**

> *Điền:*

**Actual answer:**

> *Điền:*

**Scores:** Context Recall: ____ | Context Precision: ____ | Faithfulness: ____ |
Relevance: ____ | Completeness: ____ | Overall: ____

**Evidence inspection:**

> *Câu trả lời:*

| Level | Question | Answer |
|---|---|---|
| Symptom | Vấn đề quan sát được là gì? | |
| Why 1 | Tại sao symptom xảy ra? | |
| Why 2 | Tại sao nguyên nhân trên xảy ra? | |
| Why 3 | Tại sao vấn đề đó chưa được ngăn chặn? | |
| Why 4 | Tại sao cơ chế hiện tại chưa phát hiện hoặc xử lý được? | |
| Why 5 | Root cause có thể hành động được là gì? | |

**Root cause và proposed fix:**

> *Câu trả lời:*

### Failure 3

**ID và question:**

> *Điền:*

**Expected answer:**

> *Điền:*

**Actual answer:**

> *Điền:*

**Scores:** Context Recall: ____ | Context Precision: ____ | Faithfulness: ____ |
Relevance: ____ | Completeness: ____ | Overall: ____

**Evidence inspection:**

> *Câu trả lời:*

| Level | Question | Answer |
|---|---|---|
| Symptom | Vấn đề quan sát được là gì? | |
| Why 1 | Tại sao symptom xảy ra? | |
| Why 2 | Tại sao nguyên nhân trên xảy ra? | |
| Why 3 | Tại sao vấn đề đó chưa được ngăn chặn? | |
| Why 4 | Tại sao cơ chế hiện tại chưa phát hiện hoặc xử lý được? | |
| Why 5 | Root cause có thể hành động được là gì? | |

**Root cause và proposed fix:**

> *Câu trả lời:*

---

## 3. Failure Clustering

Một root cause có thể tạo ra nhiều failures. Nhóm theo nguyên nhân có thể sửa,
không chỉ nhóm theo tên metric.

| Cluster | Root Cause | Failure IDs | Priority |
|---|---|---|---|
| 1 | | | High/Medium/Low |
| 2 | | | |
| 3 | | | |

**Nếu chỉ được sửa một cluster, bạn chọn cluster nào và vì sao?**

> *Câu trả lời:*

---

## 4. Improvement Log

Paste output của `generate_improvement_log()`:

```text
[paste Markdown table here]
```

**Ba improvement suggestions ưu tiên**

1. ____
2. ____
3. ____

Với mỗi suggestion, nêu metric dự kiến thay đổi và cách đo lại.

| Suggestion | Target metric | Verification method |
|---|---|---|
| | | |
| | | |
| | | |

---

## 5. Regression Testing Strategy

**Câu 1: Khi nào chạy `run_regression()` trong production workflow?**

> *Câu trả lời:* Tôi sẽ chạy regression ở ba điểm: khi pull request thay đổi prompt, retriever, chunking hoặc evaluation core; trước mỗi release; và sau khi cập nhật corpus hay policy. New run và baseline phải dùng cùng một golden dataset, cùng actual-input protocol và cùng phiên bản metric. Nếu đổi chính metric, tôi sẽ tính lại baseline thay vì so hai thước đo khác nhau.

**Câu 2: Threshold drop 0.05 có phù hợp OrbitTech Customer Support không? Vì sao?**

> *Câu trả lời:* Mức giảm hơn 0.05 là một guardrail dễ hiểu cho lab, nhưng chưa đủ để quyết định mọi release của OrbitTech. Với Faithfulness và Safety/Privacy, một lỗi nghiêm trọng đơn lẻ có thể đáng chặn dù average chưa giảm 0.05. Ngược lại, với tập chỉ 20 cases, chênh lệch nhỏ có thể đến từ một case. Tôi sẽ giữ contract 0.05 trong code, đồng thời xem delta theo từng difficulty, failure severity và khoảng biến động qua nhiều lần chạy trước khi dùng trong production.

**Câu 3: Metric/failure nào phải block deployment, metric nào chỉ alert?**

> *Câu trả lời:* Tôi sẽ block deployment khi Faithfulness, Relevance hoặc Completeness trung bình giảm hơn 0.05 so với baseline; khi có hành vi yêu cầu mật khẩu/OTP, làm lộ dữ liệu, làm theo prompt injection; hoặc khi một policy-critical case trả sai ngày, phí hay điều kiện đủ. Context Recall giảm đáng kể trên nhóm policy-critical cũng phải block vì generator không thể bù evidence bị thiếu một cách đáng tin cậy. Context Precision, latency và các lỗi nhẹ về tone có thể chỉ alert nếu các answer metrics và safety cases vẫn đạt gate, nhưng phải có owner và thời hạn xử lý.

**Câu 4: Điền evaluation stages vào flow.**

```text
Code/prompt/retrieval change → [Offline golden evaluation] → [Regression + safety gates] → [Human review of failures] → Deploy
```

> *Giải thích:* Offline evaluation tạo một lần chạy có thể so sánh với baseline. Regression gate kiểm tra đúng chiều giảm và safety gate bắt các lỗi nghiêm trọng không nên bị average che khuất. Human review mở actual answer và retrieved chunks của các case thấp hoặc sát ngưỡng; chỉ khi không còn blocker mới deploy, sau đó tiếp tục theo dõi online bằng canary và alert.

---

## 6. Continuous Improvement Loop

```text
Evaluate → Analyze → Improve → Augment benchmark → Repeat
```

| Priority | Action | Metric dự kiến cải thiện | Expected impact |
|---:|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |

**Hai hoặc ba failure cases nào cần thêm vào benchmark ở vòng tiếp theo?**

> *Câu trả lời:*

---

## 7. Final Reflection

**Điều gì trong kết quả benchmark trái với dự đoán ban đầu của bạn?**

> *Câu trả lời:*

**Word-overlap heuristics trong lab có giới hạn gì? Nếu đưa hệ thống vào
production, bạn sẽ thay hoặc bổ sung metric nào?**

> *Câu trả lời:* Word overlap đo được coverage từ vựng chứ không hiểu quan hệ logic. Hai câu có thể dùng gần như cùng từ nhưng một câu phủ định sai điều kiện; ngược lại, một paraphrase đúng có thể bị điểm thấp. Tập token cũng không biết claim nào quan trọng hơn, nên việc bỏ “không”, một mốc ngày hay ngoại lệ severe weather có thể ít ảnh hưởng điểm nhưng làm quyết định sai hoàn toàn. Nếu đưa vào production, tôi sẽ giữ các metric này như tín hiệu rẻ và dễ debug, rồi bổ sung claim-level entailment/groundedness, semantic answer relevance, policy-rule checks cho ngày–phí–điều kiện, safety/privacy tests và LLM-as-a-Judge đã calibrate bằng human labels. Mỗi kết luận vẫn cần liên kết về source chunk để reviewer kiểm chứng.
