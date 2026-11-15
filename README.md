---
language: [en, de]
license: mit
library_name: pytorch
pipeline_tag: translation
datasets: [bentrevett/multi30k]
metrics: [sacrebleu]
tags: [translation, seq2seq, lstm, attention, from-scratch]
---

<div align="center">

# En2de-A

**A 20M-parameter English→German translator, built from scratch in PyTorch**

![Params](https://img.shields.io/badge/params-20.4M-1f4e79)
![BLEU](https://img.shields.io/badge/BLEU-25.14-1e8449)
![Dataset](https://img.shields.io/badge/data-Multi30k-6b7280)
![Framework](https://img.shields.io/badge/PyTorch-ee4c2c)

</div>

## Results

<p align="center">
  <img src="https://github.com/user-attachments/assets/bf357bf0-bd01-4cfd-890a-39eae8d55096" width="450" height="390">
  <img src="https://github.com/user-attachments/assets/02f9c20b-2942-402a-be6c-8872c4d88b57" width="450" height="390">
</p>

| Model | Params | BLEU ↑ |
|---|---|---|
| En2de without Attention | 19.7M | 16.82 |
| **En2de-A + Attention** | 20.4M | **25.14** |

Attention adds <1M params and gives **+8.3 BLEU**. (sacreBLEU, Multi30k test, greedy decoding)

## Model

- 2-layer LSTM encoder/decoder, 512 hidden, 256 embedding
- Luong-style attention, 16k shared subword vocab, max length 50
- Trained 25 epochs on Multi30k: Adam (1e-3), warmup + cosine, label smoothing 0.1

## Example

> **EN:** A man in an orange hat starring at something.
> **DE:** Ein Mann mit einem orangefarbenen Hut starrt nach etwas .

## Usage

```python
model.load_state_dict(torch.load("En2de-A.pt", map_location="cpu"))
print(translate("A man is riding a bike."))  # Ein Mann fährt auf einem Fahrrad .
```

