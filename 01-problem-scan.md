## Phase 1 - SCAN

### Danh sach bai toan cua toi

| # | Subsidiary | Lens | Mo ta ngan bai toan |
|---|---|---|---|
| 1 | Vinmec | Ton thoi gian | Bac si soan `discharge summary` thu cong tu EMR, ket qua xet nghiem va ghi chu dieu tri. BMJ Quality Improvement report ghi nhan 1 electronic discharge summary ton trung binh `18.25 phut`; voi pilot `40 ca xuat vien/ngay` tai 1 benh vien lon se ton khoang `12.2 gio bac si/ngay`. |
| 2 | Vinmec | Stakeholder Pain | Dieu phoi dat lich doc mo ta trieu chung tu do roi route chuyen khoa bang tay. Neu co `250 yeu cau/ngay` va moi yeu cau mat `6 phut`, team mat khoang `25 gio/ngay`; route sai lam tang lead time kham va gay bo lo lich trong. |
| 3 | VinFast | AI-upgrade | Co van dich vu/warranty admin doc mo ta loi cua khach, ghi chu ky thuat, doi chieu dieu kien bao hanh roi nhap claim bang tay. WarrCloud cho biet thoi gian xu ly mot warranty claim da tang `47%` so voi nam 2020; voi uoc tinh `20-30 phut/claim` va `60 claim/ngay`, back-office ton `20-30 gio/ngay`. |
| 4 | VinFast | Lap lai | Doi ngu van hanh doi soat giao dich sac, ticket sai lech va hoa don doi tac. Chi can `1,000 truong hop lech/thang` va `8 phut/truong hop`, team da ton hon `130 gio/thang` cho viec check tay va doi file Excel. |
| 5 | Vinpearl | Stakeholder Pain | Guest relations/e-commerce doc review tu Google, Booking, Agoda, TripAdvisor, tu phan loai muc do nghiem trong va soan phan hoi cong khai bang tay. Neu `120 review/tuan` cho 1 cum resort va moi review mat `18 phut`, team mat `36 gio/tuan`; Cornell cho thay cai thien `1%` diem uy tin online co the nang `RevPAR` toi da `1.42%`. |

### Top 3 bai toan toi chon cho Quick Cards

1. `Vinmec`: draft discharge summary
2. `VinFast`: triage warranty/service claim
3. `Vinpearl`: triage review va draft response

---

## Phase 2 - QUICK-ASSESS

### Quick Problem Card #1 - Vinmec

- Bai toan: Tu dong soan `ban nhap discharge summary` tu ho so benh an dien tu de bac si duyet truoc khi xuat vien.
- Cong ty thanh vien: `Vinmec`
- Ai dang dau: `Bac si dieu tri`, `dieu duong ho so`, va gian tiep la `benh nhan` cho thong tin sau xuat vien.
- Workflow thu cong hien tai:
  1. Bac si mo EMR, doc ghi chu tien trien, chi dinh, thuoc, xet nghiem.
  2. Tong hop lai dien bien benh, thu thuat, thuoc xuat vien.
  3. Tu go ban tom tat y khoa va huong dan theo doi tai nha.
  4. Dieu duong kiem tra thuoc/lich hen.
  5. Bac si sua lan cuoi va ky.
- Buoc ton thoi gian/loi nhat: `Buoc 2-3`, khoang `20 phut/ca`, vi phai tong hop nhieu nguon va viet lai bang ngon ngu de ca dong nghiep va benh nhan deu hieu.
- AI co the nhay vao o dau: Trich xuat su kien lam sang, thuoc, can lam sang, sau do draft `discharge summary` va huong dan sau xuat vien bang ngon ngu de hieu.
- Do thanh cong bang gi:
  - Giam thoi gian soan ban nhap tu `20 phut` xuong `duoi 5 phut`.
  - `95%` ban nhap duoc tao trong `duoi 60 giay`.
  - `0%` truong hop AI duoc phep ky/ban hanh khong co bac si duyet.
- Quick Architecture: `LLM Feature` + trich xuat du lieu co cau truc + `HITL` bat buoc.
### Quick Problem Card #2 - VinFast

- Bai toan: Chuan hoa mo ta loi cua khach hang va goi y ma claim/ho so thieu cho quy trinh warranty/service.
- Cong ty thanh vien: `VinFast`
- Ai dang dau: `Service advisor`, `warranty admin`, `to truong ky thuat`.
- Workflow thu cong hien tai:
  1. Nhan mo ta loi tu khach hang qua app/cuoc goi/quay dich vu.
  2. Co van viet lai trieu chung theo ngon ngu ky thuat.
  3. Ky thuat vien bo sung ket qua chan doan va hinh anh.
  4. Warranty admin doi chieu dieu kien bao hanh, ma loi, chung tu.
  5. Gui claim va xu ly claim bi tra ve neu thieu ho so.
- Buoc ton thoi gian/loi nhat: `Buoc 2-4`, khoang `25 phut/claim`, de bi loi vi mo ta cua khach bang tieng noi thuong ngay khong khop ngon ngu ky thuat va quy tac OEM.
- AI co the nhay vao o dau: Chuan hoa symptom, goi y nhom loi, check-list tai lieu thieu, draft narrative `3C` (Concern-Cause-Correction) de con nguoi duyet.
- Do thanh cong bang gi:
  - Giam thoi gian chuan bi claim tu `25 phut` xuong `duoi 8 phut`.
  - Giam ty le claim bi tra ve tu `15%` uoc tinh xuong `duoi 5%`.
  - `90%` claim duoc AI goi y day du check-list chung tu ngay lan dau.
- Quick Architecture: `Rule + LLM Feature`.

### Quick Problem Card #3 - Vinpearl

- Bai toan: Tu dong phan loai review cong khai va soan `public reply draft` cho team guest relations, dong thoi canh bao review nguy co cao.
- Cong ty thanh vien: `Vinpearl`
- Ai dang dau: `Guest relations`, `e-commerce`, `resort operations manager`.
- Workflow thu cong hien tai:
  1. Nhan review tu Google/Booking/Agoda/TripAdvisor.
  2. Nhan vien copy vao sheet/CRM.
  3. Doc tung review, gan muc do nghiem trong va phong ban lien quan.
  4. Kiem tra booking/lich su khieu nai neu can.
  5. Soan phan hoi cong khai va note noi bo.
  6. Quan ly duyet roi dang/escalate.
- Buoc ton thoi gian/loi nhat: `Buoc 3-5`, khoang `12 phut draft + 6 phut kiem tra va route`, tong `18 phut/review`.
- AI co the nhay vao o dau: Tu dong tom tat y chinh, phan loai urgency, draft phan hoi dung giong dieu thuong hieu, goi y escalation neu co tu khoa nhu `ban`, `an toan`, `gian lan`, `injury`, `refund`.
- Do thanh cong bang gi:
  - Giam thoi gian xu ly moi review tu `18 phut` xuong `duoi 4 phut`.
  - `95%` review 1-2 sao duoc triage trong `duoi 5 phut` sau khi ingest.
  - `100%` review lien quan den an toan/ve sinh/phap ly duoc dua vao `manual review`.
- Quick Architecture: `LLM Feature` trong workflow co quy tac + `HITL`.

---

## Quyet dinh chon bai toan cho Deep-Dive

 toi chon bai toan `Vinpearl - AI copilot for review triage and draft response`.

### Ly do chon

- Du lieu vao da co san va de lay: review cong khai tu OTA/Google, khong can truy cap du lieu y te nhay cam.
- Gia tri van hanh ro: ton nhieu gio thu cong, co the do bang `response time`, `draft time`, `escalation accuracy`.
- Ranh gioi an toan de quan ly: AI khong duoc dang bai cong khai, khong duoc hua refund/compensation, moi truong hop nhay cam deu co `human approval`.

### Ly do chua chon hai card con lai

- `Vinmec discharge summary`: gia tri cao nhung can xu ly PHI, quy trinh phe duyet y khoa, log truy cap, va bo du lieu noi bo chat luong cao truoc khi pilot.
- `VinFast warranty triage`: huong di tot nhung phu thuoc vao quy tac bao hanh/OEM, ma loi, DMS va label lich su claim bi tra ve; scope dau tien de bi keo dai do tich hop.
