---
title: "OpenCV 5 Is Here - The Biggest Update Since 2018 (We Tested It)"
video_id: piHpZWcgQyc
channel: "[[channels/Better Stack]]"
uploaded: 2026-07-05
processed: 2026-07-13
duration: "9:42"
url: https://www.youtube.com/watch?v=piHpZWcgQyc
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [computer-vision, local-model-inference]
tools: [OpenCV, PyTorch, ONNX Runtime, YOLO]
llms: [PaliGemma, Gemma]
protocols: [ONNX]
transcript: true
tags: [youtube, ai-automation]
---

# OpenCV 5 Is Here - The Biggest Update Since 2018 (We Tested It)

![thumbnail](https://i.ytimg.com/vi_webp/piHpZWcgQyc/maxresdefault.webp)
▶️ [Watch](https://www.youtube.com/watch?v=piHpZWcgQyc) | 📅 Uploaded [[uploaded/2026-07-05]] | 🗓️ Processed [[created/2026-07-13]]

## TL;DR
> OpenCV 5 is the library's first major release since 2018, headlined by a complete rewrite of the DNN module: ONNX operator coverage jumps from ~22% to ~80%, and the new typed-operation-graph engine (shape inference, constant folding, operator fusion) runs modern transformer models natively — no PyTorch, no ONNX Runtime. OpenCV's own CPU benchmarks show it matching or beating Microsoft's ONNX Runtime (+11.5% on YOLOv8, +37% on OWLv2, +30% on XFeat). The video demos colorization, real-time object detection, latent-diffusion inpainting, and PaliGemma VLM captioning — all on CPU with zero extra dependencies. Big catch: the new engine is CPU-only for now; GPU lands later in the v5 cycle.

**Watch this if:** you build anything with computer vision and want to know whether OpenCV 5's new inference engine can replace your separate model runtime.

## Key Takeaways
- First major version bump in 8 years for a library with 86k+ GitHub stars and a million installs a day — the whole v4 line is what robotics, AR, medical, and industrial-inspection stacks are built on.
- The DNN rewrite is the headline: ONNX operator support goes from ~22% (constant "operator not supported" walls) to ~80%, so most modern models load out of the box.
- New engine architecture: instead of layer-by-layer execution, it builds a typed operation graph and does shape inference, constant folding, and operator fusion before running — enabling dynamic shapes and transformer architectures.
- Self-reported CPU benchmarks vs Microsoft's ONNX Runtime: 11.5% faster on YOLOv8, ~37% faster on OWLv2, 30% faster on XFeat — verify with your own workload.
- Other changes: native FP16/BF16 types, true N-dimensional arrays in cv::Mat, Python-first core, legacy C API removed, C++17 baseline.
- CPU-only for now — GPU support comes later in the v5 cycle; for GPU inference today, fall back to the classic engine (CUDA/OpenVINO).
- Demos: colorization was instant but muted (old model, new engine); real-time object detection on CPU worked impressively; LDM inpainting worked but slowly (iterative diffusion on CPU); PaliGemma captioning was painfully slow — a signal of direction (tokenizer, attention layers, KV cache all built in), not a recommendation.
- Positioning: still train in PyTorch; OpenCV 5 is for *running* models inside a vision pipeline with no extra runtime.

## 🛠 Tools & Software
- [[topics/OpenCV]] — the subject: v5 release with the rewritten DNN engine, tested across four demos
- [[topics/PyTorch]] — explicitly not needed for inference anymore; still the tool for training
- [[topics/ONNX Runtime]] — Microsoft's engine used as the benchmark baseline OpenCV 5 matches or beats on CPU
- [[topics/YOLO]] — run natively by the new engine; YOLOv8 is one of the benchmark models

## 🤖 LLMs Mentioned
- [[topics/PaliGemma]] — vision-language model used in the native VLM captioning demo (works, but painfully slow on CPU)
- [[topics/Gemma]] — 12B Gemma 4 on MLX cited as a ~100× faster alternative for image captioning

## 📡 Protocols & Standards
- [[topics/ONNX]] — the interchange format at the heart of the story; operator coverage jump from 22% to 80% is the release's key number

## ✅ Action Items
- Upgrade a CV project to OpenCV 5 and try loading a model that previously failed on unsupported ONNX operators.
- Benchmark the new DNN engine against your current ONNX Runtime workload on CPU before trusting the self-reported numbers.
- Keep the classic engine (CUDA/OpenVINO) for GPU inference until GPU support ships in the v5 cycle.
- Try the bundled samples: colorization, object detection, LDM inpainting — skip VLM captioning for production use.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — OpenCV's first major update since 2018: YOLO, diffusion inpainting, and VLMs with no PyTorch or ONNX Runtime
- `0:53` — Why it matters: 86k stars, 1M installs/day, foundation of robotics/AR/medical/industrial CV
- `1:36` — The DNN rewrite: ONNX operator coverage 22% → 80%; typed operation graph, shape inference, constant folding, operator fusion
- `2:47` — CPU benchmarks vs ONNX Runtime: +11.5% YOLOv8, +37% OWLv2, +30% XFeat (self-reported)
- `3:27` — Also new: FP16/BF16, N-dimensional cv::Mat, Python-first core, C++17 baseline, legacy C API removed
- `3:44` — The catch: new engine is CPU-only; classic engine keeps CUDA/OpenVINO for GPU
- `4:16` — Demo 1: colorizing a Spider-Noir frame — instant, muted tones (old model, new engine)
- `5:15` — Demo 2: real-time object detection on CPU through the new engine
- `6:03` — Demo 3: latent-diffusion inpainting — works, slow on CPU (iterative denoising)
- `7:11` — Demo 4: PaliGemma VLM captioning — painfully slow, but tokenizer/attention/KV cache all native now
- `8:27` — Verdict: train in PyTorch, run in OpenCV 5; massive leap, GPU update will complete it

## Transcript
<details>
<summary>Full transcript</summary>

So we all know OpenCV, right? It is the ultimate computer vision library everyone's been using for resizing images, detecting objects, and performing all sorts of computer vision tasks. And it just got the first major release update since 2018. And this is a big one. OpenCV 5 has a brand new deep learning engine that can run YOLO. It can also do stable diffusion-style inpainting and even run a full vision language model all natively with no PyTorch, no ONNX runtime, and nothing else bolted on it. So in today's video, we'll break down what's actually new in OpenCV 5, and then we'll test out the new features ourselves with some cool demos running locally on my own machine. It's going to be a lot of fun, so let's dive into it.

So first off, here's why this update is a big deal. OpenCV is everywhere. It has more than 86,000 GitHub stars, over a million installs a day, and for two decades it's been the foundation for robotics and AR and medical engineering, industrial inspection, basically any software that has some computer vision aspect attached to it. And for the last 8 years, everyone's been building on the same version 4 line. So a major version bump here is genuinely a huge deal. And the headline feature of this new version is a complete rewrite of the DNN module, and that's the part of OpenCV that runs neural networks. So here's the most important number to pay attention to. In OpenCV 4, the DNN engine supported only about 22% of ONNX operators. ONNX is the standard format you export a model to when you want to run it somewhere other than the framework you trained it on. And 22% coverage meant that more often than not, you'd grab a modern model, try to load it, and immediately hit a wall. Some operator wasn't supported, so you were stuck. But, OpenCV 5 brings that coverage up to 80%. So, now this library runs most of these models out of the box. And the reason it jumped so much is because of how they rebuilt it. The old engine processed networks layer by layer. The new one is built around a typed operation graph. So, it looks at the whole network as a graph first, and then does proper shape inference, constant folding, and operator fusion before it actually runs anything. So, in plain terms, it understands the entire model before executing it, so it can handle dynamic shapes and modern transformer architectures that the old engine just couldn't handle.

And here's the impressive part. With these new changes, not only is it more compatible, but it's also very fast. OpenCV benchmarked their new engine against Microsoft's ONNX engine, and on a CPU, OpenCV 5 matched or even beat it on real models. So, it was 11.5% faster than YOLO version 8, almost 37% faster than OWL version 2, and 30% faster than XFeat. Now, those are OpenCV's own self-reported numbers, so take them with the usual grain of salt and benchmark your own workload. But, if they are true, that is pretty impressive. And there are more cool stuff in this new release, like native FP16 and BF16 data types, real N-dimensional array support in CV Mat, a Python-first core, and the legacy C API is gone and replaced with the C++17 now being the baseline. And one important catch you need to know about up front, the new engine is CPU only at the moment. GPU support is coming later in the version 5 cycle. So, if you need GPU inference today, you will fall back to the classic engine, which still has CUDA and OpenVINO support. So, everything I'm about to show you on this new version 5 runs on a CPU.

So, the biggest feature of this new version is the new DNN engine. So, we'll test out some of the examples and see how it performs. All right, let's start with a fun example. So, OpenCV ships a colorization example where you can take a black and white image and it predicts the color. And on a side note, I've been watching Spider-Noir lately and it's a pretty cool show. And it's also in black and white, so I thought it might be fun to colorize a shot from this show and see how it looks. So, I'm going to take this image and run the colorization example, which is using the new DNN engine, and boom, here it is. Look how fast that was. As far as the output goes, it's not perfect. We still see that it got the sky somewhat correct, but it failed to colorize some other parts of the image. And keep in mind that this is using an older colorization model, which plays it safe with the muted tones. But the point here isn't the model, it is the engine. So, what I wanted to show you here is that this image was produced using the native OpenCV neural network with zero extra dependencies, which is quite cool.

Now, let's try their object detection sample. And again, since we're on the Spider-Noir theme, I'm going to be using a clip from the show and run it through the pipeline and see how it performs. And when I launch the script, look at that. It's doing object detection in real time running on the CPU through the new DNN engine. And remember that benchmark from earlier? This is the kind of model where OpenCV is actually faster than the ONNX runtime. So, not trading performance for convenience, you're getting both in this particular scenario. And you don't need to install PyTorch for this or a separate runtime, and there's no GPU required. This is all running in plain OpenCV.

All right, now let's try their LDM in-painting example. So, LDM stands for latent diffusion, and OpenCV 5 ships a latent diffusion in-painting example here. So, let's see how that works. So, let's load up the same Spider-Man image we used earlier, and now I can paint over something I want to be removed from the image. It can be a person, an object, whatever. And the diffusion model fills in the blank space. And this is a bit slower to run because OpenCV's classic in-painting uses a single forward pass, which is instant, but the LDM uses diffusion, which is iterative. So, it starts from noise, and then it denoises it step by step. So, it's running this model multiple steps in a row. And because we're doing this on a CPU, it's even slower because diffusion is a task more suited for a GPU. But, nonetheless, here is the result I got when running it on just a few steps. And I'd say it's done a pretty decent job. It's not perfect. We can still clearly see some diffusion artifacts, but this can be solved by increasing the step count or using a different diffusion model.

And lastly, I want to show you the VLM inference example, which shows you how you can use vision-language models or LLMs natively inside OpenCV to do things like image captioning or other sorts of things. Now, in this particular demo, we're using the PaLI Gemma model to caption this Spider-Man image. And as you can see, it's painfully slow, and the end result is also nothing spectacular. So, I would most definitely not use OpenCV for this. There are far better options for image captioning. For example, you can run a 12 billion Gemma 4 model locally on MLX and get a 100 times faster output than this. I showed that particular example in one of my previous videos about the 12 billion Gemma 4 model, so check that out if you're interested. But the point of this demo is to showcase that OpenCV now has all the pieces you need to run LLMs. The tokenizer, the attention layers, and the KV cache, all built in. And the fact that it works at all on a separate runtime is genuinely signaling where this library is heading. It's going to have vision and language bundled all in one place. And once they ship the GPU update, it's going to be even better and even faster.

So there you have it, folks. That is the new OpenCV version 5 in a nutshell. One library running on the CPU with no extra dependencies, and we used it for colorization, real-time object detection, diffusion in-painting, and image captioning. Now you're still going to have to train your models on something like a PyTorch. That's not something OpenCV is designed to do, but when it comes to actually running those models inside the vision pipeline, OpenCV 5 is a great choice and a massive leap from where it was just a month ago with their new DNN engine. So what do you think about the new OpenCV 5? Are you going to use it in your projects? Let us know in the comment section down below. And folks, if you like these types of technical breakdowns, please let me know by smashing that like button underneath the video. And also, don't forget to subscribe to our channel. This has been Andress from Better Stack, and I will see you in the next videos.

</details>
