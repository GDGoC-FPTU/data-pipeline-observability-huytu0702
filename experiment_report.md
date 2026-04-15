# Experiment Report: Data Quality Impact on AI Agent

**Student ID / GitHub Username:** huytu0702
**Name:** Nguyen Huy Tu
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | `Agent: Based on my data, the best choice is Laptop at $1200.0.` | 9 | Tra loi hop ly vi du lieu da duoc loc record loi, category duoc chuan hoa, va tap electronics chi con Laptop va Monitor. |
| Garbage Data (`garbage_data.csv`) | `Agent: Based on my data, the best choice is Nuclear Reactor at $999999.` | 2 | Agent bi outlier gia cuc lon danh lua. Bo du lieu nay con co duplicate ID, sai kieu du lieu, gia bang 0, va null category. |

---

## 2. Phan tich va nhan xet

### Tai sao agent tra loi sai khi dung garbage data?

Agent trong bai nay rat don gian: no tim san pham electronics co gia cao nhat trong bo du lieu. Khi du lieu sach da duoc ETL xu ly, record am gia va category rong bi loai bo, nen ket qua hop ly la Laptop. Nguoc lai, garbage data chua mot outlier la Nuclear Reactor co gia 999999, vi vay agent uu tien record nay ngay lap tuc. Ngoai ra, duplicate ID lam giam do tin cay cua khoa chinh, wrong data type nhu `ten dollars` co the gay loi khi mo rong logic, con null values va gia bang 0 lam tap du lieu nhieu noise hon. Van de cot loi la agent khong co lop validation rieng, nen no tin rang du lieu dau vao da dung. Chat luong du lieu kem vi the dan den suy luan sai du prompt khong doi. Neu mot he thong AI dua vao pipeline khong co observability, nhom van hanh se rat kho xac dinh output sai do prompt, do model hay do input bi ban. Bai test nay cho thay chi can mot vai record doc hai la quyet dinh cuoi cung cua agent da lech hoan toan khoi muc tieu.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Toi dong y. Prompt tot chi giup agent su dung du lieu hieu qua hon, nhung neu du lieu nen da sai, thieu, hoac bi doc, ket qua van se lech. Trong thi nghiem nay, prompt giu nguyen hoan toan, chi thay doi chat luong du lieu ma output da chuyen tu hop ly sang sai ro rang. Dieu nay cho thay quan sat chat luong du lieu va chan record bat thuong quan trong khong kem viec viet prompt.
