# Session Understanding Checklist

Muc tieu: phien nay chi ket thuc khi nguoi hoc da chung minh rang minh hieu van de, giai phap, quyet dinh thiet ke, edge cases va tac dong rong hon cua bai/lab.

## Cach hoc trong phien

- [ ] Nguoi hoc tu dien giai hieu biet ban dau truoc khi duoc giai thich.
- [ ] Moi chang chi chuyen tiep khi nguoi hoc da the hien nam duoc y chinh.
- [ ] Ket hop dong luc cap cao voi logic/chi tiet cap thap.
- [ ] Dung cau hoi mo, cau hoi trac nghiem, va doc code/notebook khi can.
- [ ] Cap nhat checklist khi xac minh duoc tung phan.
- [ ] Dieu chinh nhip hoc: uu tien hieu de lam lab/report, khong kiem tra qua ti mi khi nguoi hoc da nam y chinh.

## 1. Van de can hieu

- [x] Bai/lab dang co gang giai quyet van de gi?
- [x] Tai sao van de nay ton tai trong fine-tuning LLM?
- [x] Vi sao full fine-tuning thuong ton kem va kho chay tren GPU gioi han?
- [x] LoRA/QLoRA xuat hien de giai quyet nhanh, re, nhe hon o diem nao?
- [x] Cac nhanh/huong tiep can phan biet: full fine-tuning, LoRA, QLoRA, inference-only, prompt engineering.
- [x] Cac trade-off giua chi phi, chat luong, toc do, bo nho, va do phuc tap.

## 2. Giai phap can hieu

- [x] LoRA them low-rank adapters vao dau trong mo hinh va vi sao cach nay tiet kiem tham so.
- [ ] Cac tham so quan trong: rank `r`, `alpha`, `dropout`, target modules, learning rate, batch size, gradient accumulation.
- [x] QLoRA khac LoRA o dau: quantization 4-bit, base model dong bang, adapter duoc train.
- [ ] Vi sao giai phap trong repo/notebook duoc thiet ke theo cach hien tai.
- [ ] Cac buoc pipeline: load model/tokenizer, chuan bi dataset, cau hinh PEFT/LoRA, train, evaluate, save/merge adapter.
- [ ] Edge cases: dataset format sai, sequence qua dai, OOM GPU, target module sai, tokenizer/pad token, chat template, overfitting, checkpoint/resume.

## 3. Tac dong rong hon

- [x] Thay doi nay tac dong den chi phi train/inference nhu the nao.
- [x] Tac dong den kha nang deploy, chia se adapter, va tai su dung base model.
- [x] Khi nao nen dung LoRA/QLoRA, khi nao khong nen.
- [ ] Rui ro ve chat luong, bias, data leakage, evaluation ao, va monitoring sau deploy.
- [x] Cac thay doi se anh huong den nguoi dung cuoi/nhom ML/ha tang ra sao.

## Bang chung da hieu

- [x] Nguoi hoc tu tom tat lai van de bang loi cua minh.
- [x] Nguoi hoc giai thich duoc vi sao giai phap chon LoRA/QLoRA thay vi full fine-tuning.
- [ ] Nguoi hoc doc duoc cac o/cau hinh quan trong trong notebook va noi chung lam gi.
- [ ] Nguoi hoc tra loi dung cac cau hoi ve trade-off va edge cases.
- [ ] Nguoi hoc dua ra duoc mot kich ban ap dung that te va cac rui ro can canh chung.

## Trang thai hien tai

- [x] Nguoi hoc da restate hieu biet ban dau.
- [x] Hoan thanh Stage 1: van de, vi sao van de ton tai, va cac nhanh giai phap.
- [ ] Dang hoc Stage 2: giai phap trong notebook, design decisions, cau hinh va edge cases.

## Restate ban dau cua nguoi hoc

- Van de chinh: fine-tuning LoRA LLMs.
- Full fine-tuning kho vi can dataset tot/chuan hoa va yeu cau phan cung lon.
- LoRA/QLoRA giup fine-tune phan nho cua model, giam chi phi tinh toan va yeu cau phan cung.
- Chua ro muc dich so sanh `r=8`, `r=16`, `r=64`.
- Chua ro edge cases khi fine-tune LLM tren GPU gioi han.

## Khoang trong can day tiep

- Phan biet chinh xac bai lab: khong chi "fine-tuning LoRA", ma la hoc trade-off cua parameter-efficient fine-tuning thong qua rank experiment.
- [x] Lam ro: LoRA khong fine-tune "mot vai layer goc" theo nghia sua truc tiep weight goc; no dong bang base model va them adapter low-rank co the train.
- [x] Lam ro muc dich rank: rank cang cao thi adapter co nang luc bieu dien lon hon, nhung ton VRAM/time hon va co the diminishing returns/overfit.
- Lam ro edge cases: OOM, format dataset sai, target module sai, max sequence length qua dai, eval OOM, overfitting, tokenizer/pad/chat template/version mismatch.

## Kiem tra Stage 1 lan 1

- Cau 1: Nguoi hoc sua dung y chinh: LoRA khong sua truc tiep weight goc ma them "ghi chu"/adapter vao model.
- Cau 2: Nguoi hoc hieu `r=64` ton tai nguyen hon va co the khong cai thien tuong xung.
- Cau 3: Nguoi hoc neu dung cac nghi ngo OOM quan trong: model qua nang/phan cung yeu, sequence qua dai, batch qua lon.
- Can bo sung: eval OOM, target module/tokenizer/version mismatch, va phan biet khi nao dung prompt/RAG/fine-tuning.

## Kiem tra Stage 1 lan 2

- Cau hoi: Chatbot sai vi khong biet chinh sach hoan tien moi nhat cua cong ty thi nen dung gi?
- Tra loi nguoi hoc: dung RAG vi day la van de knowledge cap nhat, co the cap nhat retrieval corpus/index thay vi sua prompt hay fine-tune.
- Danh gia: dat Stage 1.

## Kiem tra Stage 2 lan 1

- Cau 1 ve `r`: dat y chinh. Nguoi hoc hieu `r` la rank/capacity cua adapter, rank cao hon thi nhieu tham so train hon.
- Cau 2 ve `alpha = 2r`: chua ro. Can day tiep ve viec giu scaling ratio on dinh de so sanh rank cong bang hon.
- Cau 3 ve save adapter truoc eval: chua ro. Can day tiep ve eval OOM va checkpoint safety.
- Cau 4 ve chon deploy khi r64 chi tot hon it: dat. Nguoi hoc chon r16 vi ROI tot hon, chi can nhac r64 khi du tai nguyen/thoi gian va loi ich dang gia.

## Kiem tra Stage 2 lan 2

- Cau 1 ve `alpha/r`: dat. Nguoi hoc tinh dung bang 2 va hieu giu ty le on dinh giup so sanh cong bang.
- Cau 2 ve save adapter truoc eval: dat. Nguoi hoc hieu eval co the fail/OOM va lam mat cong train neu chua save.
- Cau 3 ve report khi eval OOM: mot phan. Nguoi hoc biet can ghi nhan OOM, can bo sung cach ghi metric thieu/fallback/anh huong den ket luan.

## Kiem tra Stage 2 lan 3

- Cau 1 ve QLoRA vs LoRA: mot phan. Nguoi hoc biet QLoRA dung quantized 4-bit; can bo sung base model dong bang va adapter van la phan duoc train.
- Cau 2 ve vi sao 4-bit giup T4 chay duoc: chua ro. Can day tiep memory math truc giac.
- Cau 3 ve dataset `_vi` va hard-code `instruction`: chua chinh xac. Loi thuong la code khong tim thay cot va nem `KeyError`, khong phai model "hieu sai" ngay tu dau.
- Cau 4 ve split train/eval: dat y chinh. Nguoi hoc hieu eval la bai kiem tra chua hoc de phat hien hoc vet/overfitting.

## Kiem tra Stage 2 lan 4

- Cau 1 QLoRA dien khuyet: dat. Nguoi hoc tra loi `4-bit`, `frozen`, `trainable`.
- Cau 2 vi sao van co the OOM: dat y chinh. Nguoi hoc hieu 4-bit chi giam tai nguyen, khong lam bien mat moi chi phi bo nho.
- Cau 3 `KeyError: instruction`: mot phan. Nguoi hoc biet kiem tra hard-code; can bo sung kiem tra actual column names cua dataset.

## Kiem tra Stage 2 edge cases lan 1

- Cau 1 ve `max_seq_length = p95`: chua ro. Can day tiep ve trade-off giua cover du context va tranh bi outlier lam OOM.
- Cau 2 ve gradient accumulation: chua ro. Can day tiep ve effective batch size.
- Cau 3 ve train loss giam nhung eval loss tang: mot phan. Nguoi hoc mo ta dung viec model khong tong quat hoa, nhung can dung thuat ngu `overfitting`.
- Cau 4 ve khong giau qualitative failures: dat. Nguoi hoc hieu report phai trung thuc de tim loi va tranh trai nghiem xau khi deploy.

## Kiem tra Stage 2 edge cases lan 2

- Cau 1 ve outlier sequence dai: dat. Nguoi hoc hieu outlier lam tang memory/training cost cho ca pipeline.
- Cau 2 ve effective batch size: dat. Cong thuc dung: `per_device_train_batch_size x gradient_accumulation_steps`.
- Cau 3 ve `r=64` train loss dep nhung eval/output kem: dat y chinh. Nguoi hoc goi dung `overfitting`; can bo sung cach xu ly: giam rank, giam epochs, tang/clean data, tang dropout/regularization, giam learning rate.

## Kiem tra Stage 2 tong hop lan 1

- Nguoi hoc neu dung cac quyet dinh: 4-bit, frozen base, batch size nho, save adapter truoc eval, va giu scaling cong bang.
- Can sua nhe: khong phai "set alpha = nhau"; dung hon la giu `alpha/r` bang nhau, trong lab la `2`.
- Con thieu trong tong hop: `max_seq_length = p95`, gradient accumulation, train/eval split, va muc dich train `r=8/16/64`.

## Dieu chinh nhip hoc

- Nguoi hoc yeu cau tang toc de vao lam lab.
- Cach tiep tuc: gom cac y con thieu thanh ban do thuc hanh, chi quiz mini defense cuoi moi stage thay vi hoi tung chi tiet nho.

## Mini defense truoc khi vao lab

- Cau hoi: Neu `r=64` perplexity chi tot hon `r=16` rat it nhung ton VRAM/time hon nhieu, ket luan report the nao?
- Tra loi nguoi hoc: `r=64` tot hon `r=16`, tuy nhien trade-off qua lon nen khong toi uu; uu tien chon `r=16`.
- Danh gia: dat muc san sang vao lab. Can nho viet ro bang chung metrics va khong noi `r=64` "tot hon" chung chung neu loi ich qua nho/khong on dinh.

## Ghi chu repo cu the

- Notebook chinh: `notebooks/Lab21_LoRA_Finetuning_T4.ipynb`.
- Muc tieu notebook: fine-tune Qwen2.5-3B bang LoRA/QLoRA tren T4/Free Colab.
- Thiet ke lab: train 3 adapter voi rank `r=8`, `r=16`, `r=64`.
- Baseline: `r=16`, `alpha=32`; rank experiments: `r=8, alpha=16` va `r=64, alpha=128`.
- Dataset mac dinh: Vietnamese Alpaca tu HuggingFace, co auto-detect cot vi dataset dung suffix `_vi`.
- Constraint quan trong: T4 16GB nen dung model 3B, batch size 1, gradient accumulation, tat eval-during-training, safe eval fallback.
- Metrics can hieu: trainable params, training time, peak VRAM, eval loss, perplexity, qualitative before/after.
- Pitfalls repo da neu: sai cot dataset, version mismatch TRL/Transformers, `eval_strategy` rename, `packing=True` bug, NotebookProgressCallback bug, OOM khi eval.
