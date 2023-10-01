# KoT-platypus
![KO-platypus](./kot-platypus.png)
**CoT 방식을 활용하여 KO-platypus2를 fine-tuning한 model**  
  
**KoT-platypus2-7B🥮:** [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/kyujinpy/KoT-platypus2-7B)   
**KoCoT_2000🥮:** [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/datasets/kyujinpy/KoCoT_2000)   
- 본 연구는 (주)마커와 (주)미디어그룹사람과숲의 오픈소스 LLM 연구 컨소시엄에서 진행되었습니다.

# KO-platypus2
[KO-platypus2](https://github.com/Marker-Inc-Korea/KO-Platypus)  

# Training Hyperparameters  
| Hyperparameters | Value |  
| --- | --- |  
| batch_size | `64` |   
| micro_batch_size | `1` |  
| Epochs | `15` |  
| learning_rate | `1e-5` |  
| cutoff_len | `4096` |  
| lr_scheduler | `linear` |  
| base_model | `kyujinpy/KO-Platypus2-7B-ex` |  
  
# Performance
When I evaluated Ko-Platy, I used this [repo](https://github.com/Beomi/ko-lm-evaluation-harness).  
And, implement below code.
```
# In colab,
!python main.py \
    --model gpt2 \ 
    --model_args pretrained=..your_model_name.. \
    --tasks kobest_hellaswag,kobest_copa,kobest_boolq,kobest_sentineg \
    --device cuda:0 \
    --num_fewshot 0 # 5, 10, 25, ...
```
  
### COPA (F1)
| Model | 0-shot | 5-shot | 10-shot | 50-shot |
| --- | --- | --- | --- | --- |
| [Polyglot-ko-1.3b](https://huggingface.co/EleutherAI/polyglot-ko-1.3b) | 0.7196 | 0.7193 | 0.7204 | 0.7206 |
| [Polyglot-ko-3.8b](https://huggingface.co/EleutherAI/polyglot-ko-3.8b) | 0.7595 | 0.7608 | 0.7638 | 0.7788 |
| [Polyglot-ko-5.8b](https://huggingface.co/EleutherAI/polyglot-ko-5.8b) | 0.7745 | 0.7676 | 0.7775 | 0.7887 |
| [Polyglot-ko-12.8b](https://huggingface.co/EleutherAI/polyglot-ko-12.8b) | 0.7937 | 0.8108 | 0.8037 | 0.8369 |
| [Llama-2-Ko-7b 20B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.7388 | 0.7626 | 0.7808 | 0.7979 |
| [Llama-2-Ko-7b 40B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.7436 | 0.7927 | 0.8037 | 0.8259 | 
| [KO-platypus2-7B-EX](https://huggingface.co/kyujinpy/KO-Platypus2-7B-ex) | 0.7509 | 0.7899 | 0.8029 | 0.8290 |  
| **KoT-platypus2-7B(ours)** | 0.7517 | 0.7868 | 0.8009 | 0.8239 |   
  
### HellaSwag (F1)
| Model | 0-shot | 5-shot | 10-shot | 50-shot |
| --- | --- | --- | --- | --- |
| [Polyglot-ko-1.3b](https://huggingface.co/EleutherAI/polyglot-ko-1.3b) | 0.5247 | 0.5260 | 0.5278 | 0.5427 |
| [Polyglot-ko-3.8b](https://huggingface.co/EleutherAI/polyglot-ko-3.8b) | 0.5707 | 0.5830 | 0.5670 | 0.5787 |
| [Polyglot-ko-5.8b](https://huggingface.co/EleutherAI/polyglot-ko-5.8b) | 0.5976 | 0.5998 | 0.5979 | 0.6208 |
| [Polyglot-ko-12.8b](https://huggingface.co/EleutherAI/polyglot-ko-12.8b) | 0.5954 | 0.6306 | 0.6098 | 0.6118 |
| [Llama-2-Ko-7b 20B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.4518 | 0.4668 | 0.4726 | 0.4828 |
| [Llama-2-Ko-7b 40B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.4562 | 0.4657 | 0.4698 | 0.4774 |
| [KO-platypus2-7B-EX](https://huggingface.co/kyujinpy/KO-Platypus2-7B-ex) | 0.4571 | 0.4461 | 0.4371 | 0.4525 |  
| **KoT-platypus2-7B(ours)** | 0.4432 | 0.4382 | 0.4550 | 0.4534 | 
  
### BoolQ (F1)
| Model | 0-shot | 5-shot | 10-shot | 50-shot |
| --- | --- | --- | --- | --- |
| [Polyglot-ko-1.3b](https://huggingface.co/EleutherAI/polyglot-ko-1.3b) | 0.3552 | 0.4751 | 0.4109 | 0.4038 |
| [Polyglot-ko-3.8b](https://huggingface.co/EleutherAI/polyglot-ko-3.8b) | 0.4320 | 0.5263 | 0.4930 | 0.4038 |
| [Polyglot-ko-5.8b](https://huggingface.co/EleutherAI/polyglot-ko-5.8b) | 0.4356 | 0.5698 | 0.5187 | 0.5236 |
| [Polyglot-ko-12.8b](https://huggingface.co/EleutherAI/polyglot-ko-12.8b) | 0.4818 | 0.6041 | 0.6289 | 0.6448 |
| [Llama-2-Ko-7b 20B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.3607 | 0.6797 | 0.6801 | 0.6622 |
| [Llama-2-Ko-7b 40B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.5786 | 0.6977 | 0.7084 | 0.7144 |
| [KO-platypus2-7B-EX](https://huggingface.co/kyujinpy/KO-Platypus2-7B-ex) | 0.6028 | 0.6979 | 0.7016 | 0.6988 |  
| **KoT-platypus2-7B(ours)** | 0.6142 | 0.6757 | 0.6839 | 0.6878 | 
  
### SentiNeg (F1)
| Model | 0-shot | 5-shot | 10-shot | 50-shot |
| --- | --- | --- | --- | --- |
| [Polyglot-ko-1.3b](https://huggingface.co/EleutherAI/polyglot-ko-1.3b) | 0.6790 | 0.6257 | 0.5514 | 0.7851 |
| [Polyglot-ko-3.8b](https://huggingface.co/EleutherAI/polyglot-ko-3.8b) | 0.4858 | 0.7950 | 0.7320 | 0.7851 |
| [Polyglot-ko-5.8b](https://huggingface.co/EleutherAI/polyglot-ko-5.8b) | 0.3394 | 0.8841 | 0.8808 | 0.9521 |
| [Polyglot-ko-12.8b](https://huggingface.co/EleutherAI/polyglot-ko-12.8b) | 0.9117 | 0.9015 | 0.9345 | 0.9723 |
| [Llama-2-Ko-7b 20B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.4855 | 0.8295 | 0.8711 | 0.8513 |
| [Llama-2-Ko-7b 40B](https://huggingface.co/beomi/llama-2-ko-7b) | 0.4594 | 0.7611 | 0.7276 | 0.9370 |
| [KO-platypus2-7B-EX](https://huggingface.co/kyujinpy/KO-Platypus2-7B-ex) | 0.5821 | 0.7653 | 0.7991 | 0.8643 |  
| **KoT-platypus2-7B(ours)** | 0.6127 | 0.7199 | 0.7531 | 0.8381 | 
   
# References
[Kopen-Platypus🥮](https://huggingface.co/datasets/kyujinpy/KOpen-platypus)   
[KO-platypus](https://github.com/Marker-Inc-Korea/KO-Platypus)  
[Platypus](https://github.com/arielnlee/Platypus)  
[ko-lm-evaluation-harness](https://github.com/Beomi/ko-lm-evaluation-harness)   
