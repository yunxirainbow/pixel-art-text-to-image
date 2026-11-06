# Stable Diffusion 1.5 + LoRA: Parameter Evaluation Results

## 1. Checkpoint (Training Steps)

**Conclusion: No clear optimal checkpoint.**

Early checkpoints (especially images 1–2) generally performed worse. Later checkpoints produced recognizable objects, but their overall visual quality remained moderate. Increasing training steps did not consistently improve image quality.

## 2. LoRA Strength

**Best Range: 0.70–0.80 | Recommended: 0.75**

LoRA strength showed a noticeable impact on image quality. Frogs and pine trees performed better around 0.70–0.80, while jellyfish showed relatively good results at both 0.40 and 0.80.

Lower strengths around 0.40 produced an interesting hybrid style between pixel art and realistic illustrations. This style is worth preserving as an alternative rather than treating it as inferior.

Higher LoRA strengths did not consistently improve visual quality and sometimes introduced excessive noise or overly simplified shapes.

## 3. Classifier-Free Guidance (CFG Scale)

**Conclusion: Limited impact on overall quality | Recommended: 7.5**

Across the tested range of 3.0–9.0, CFG adjustments produced relatively minor differences in overall image quality.

Lower CFG values (approximately 3.0–5.0) introduced noticeable stylistic variations, but these changes were not consistently better or worse.

The LoRA × CFG interaction experiments did not identify a universally optimal CFG value.

## 4. Sampling Steps

**Conclusion: No consistent relationship with image quality | Recommended: 30–40 steps**

Increasing sampling steps did not consistently improve image quality.

Different prompts responded differently:
- Jellyfish: Relatively good results at 25 and 50 steps.
- Pine tree: Better results around 50–60 steps.
- Red pepper: Relatively good results around 25–40 steps.

Higher sampling steps increase inference time without guaranteeing better results.

## 5. Sampling Scheduler

**Best Scheduler: Euler Ancestral (EulerA)**

EulerA demonstrated the clearest improvement among all tested inference parameters.

Compared with DDIM, Euler, and DPM, EulerA generally produced more recognizable object shapes, better structural details, and more visually appealing results.

This was the most consistent and significant finding across the experiments.

## 6. Random Seed

**Conclusion: Major impact on image appearance, but no universally optimal seed.**

Random seeds strongly affect object shapes, composition, visual details, and overall style.

Different seeds can produce dramatically different images even when all other parameters remain unchanged.

However, no specific seed consistently improved quality across all prompts. Multiple seeds should be tested when selecting final images.

## 7. Negative Prompt

**Conclusion: No demonstrated consistent improvement.**

The initial negative prompt experiments did not produce reliable improvements in image quality.

Negative prompting was not independently retested in V2.2, so its effectiveness under the improved EulerA configuration remains uncertain.

For now, an empty negative prompt is recommended.

## 8. Postprocessing (24×24 Pixel Art)

**Preferred Methods: Nearest Neighbor or Box | No Color Quantization**

The first three postprocessing variants generally preserved more useful visual information.

For actual 24×24 outputs, Nearest Neighbor and Box are the preferred downsampling methods.

Restricting images to 16, 8, or 5 colors frequently caused darker outputs, color loss, and reduced visual detail.

Therefore, aggressive palette reduction is not recommended at this stage.

## 9. Recommended Configuration

| Parameter | Recommended Setting |
|---|---|
| Base Model | Stable Diffusion 1.5 |
| Fine-Tuning Method | LoRA |
| Checkpoint | Best validation checkpoint (provisional) |
| LoRA Strength | 0.75 |
| CFG Scale | 7.5 |
| Sampling Steps | 30 |
| Scheduler | Euler Ancestral (EulerA) |
| Negative Prompt | None |
| Random Seed | Multiple seeds for visual selection |
| Generation Resolution | 512×512 |
| Final Resolution | 24×24 |
| Downsampling | Nearest Neighbor / Box |
| Color Quantization | Disabled |

## 10. Overall Findings

The V2.1 and V2.2 experiments revealed several important patterns.

**Parameters with noticeable quality improvements:**
- **Scheduler:** EulerA consistently outperformed the alternatives.
- **LoRA Strength:** Values around 0.70–0.80 generally produced better results.

**Parameters with limited or inconsistent quality improvements:**
- **Checkpoint:** No clearly superior training stage was identified.
- **CFG Scale:** Mainly introduced minor visual and stylistic variations.
- **Sampling Steps:** Increasing steps did not guarantee better results.
- **Negative Prompt:** No reliable improvement was demonstrated.

**Parameters primarily affecting visual appearance:**
- **Random Seed:** Major influence on composition, shape, and style.
- **Low LoRA Strength (~0.40):** Produced a distinctive hybrid pixel-art/realistic style.
- **Postprocessing:** Changed pixel appearance and color preservation without correcting underlying generation errors.

### Final Conclusion

The most effective inference configuration identified so far is **EulerA with LoRA strength around 0.75, CFG 7.5, and 30 sampling steps**.

Two visual directions are worth preserving: a stronger pixel-art style at LoRA strengths of 0.70–0.80, and a hybrid pixel-art/realistic style around 0.40.

However, overall image quality remains below the desired standard. Further improvements may require changes to the LoRA training process, dataset quality, or text–image conditioning rather than additional inference parameter tuning alone.

These conclusions are based on subjective human visual evaluations across five prompts and should be treated as preliminary experimental findings rather than universal optimal settings.
