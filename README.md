# 渡辺 誠 | Makoto Watanabe

**GPUインフラ・ローカルLLM・AIエージェントの実機検証**

限られた計算資源で、どのAIモデルが動き、どこまで現場の仕事を任せられるかを検証しています。GPUや推論エンジンの選定から、性能と品質の比較、運用時の権限・通信制御まで扱います。公開リポジトリには、検証条件、再現手順、実測データ、分かったこととその限界を残しています。

I test what AI models can run on available hardware and which real-world tasks they can handle. My work covers GPU infrastructure, local inference, and agent evaluation, with reproducible setups and measurements that help teams choose what to deploy.

**GPU推論・CUDA最適化のご依頼・ご相談 / Consulting inquiries for GPU inference and CUDA optimization** — [nabe@gridtech.jp](mailto:nabe@gridtech.jp)

## 代表プロジェクト | Selected work

| プロジェクト | 内容 |
| --- | --- |
| [Alpamayo 2 Edge on DGX Spark](https://github.com/nabe2030/alpamayo2-edge-dgx-spark) | 自動運転モデルの推論で、推論理由を1トークンずつ生成するための**FP8・FP4のCUDA行列ベクトル積カーネルを実装・チューニング**。DGX Spark（GB10）1台で、生成時間をBF16の16.6 ms/tokenからFP8で11.0、FP4で8.47 ms/tokenに短縮。前処理・画像エンコーダーの最適化も組み合わせ、Argoverse 2の同一入力で推論1回を公式の高速化設定 `tuned` の1.9秒から**FP4で0.64秒（3.0倍速）**に短縮しました。<br>Implemented and tuned custom FP8 and FP4 CUDA matrix–vector kernels for reasoning-token generation on a single DGX Spark. Decode time fell from 16.6 ms/token in BF16 to 11.0 in FP8 and 8.47 in FP4. With preprocessing and vision-encoder optimizations, inference on the same Argoverse 2 input took **0.64 s with FP4, down from 1.9 s with the official `tuned` configuration (3.0× speedup)**. |
| [LlamaMonita](https://github.com/nabe2030/llama-monita) | llama.cpp向けのWindowsデスクトップ監視ツール。ローカルPCのGPU使用率・専用／共有GPUメモリと、llama-serverの生成速度・コンテキスト使用量を可視化し、リクエスト履歴をCSVに保存。Prometheus連携にも対応。 · Windows desktop monitor for llama.cpp, with local GPU telemetry, server activity, CSV request history and Prometheus export. |
| [GembaBench](https://github.com/nabe2030/gembabench) | AIエージェントにサーバー調査、侵入分析、更新、脆弱性対応を任せられるかを評価。報告書に加え、作業後のサーバーの状態やサービスの動作も検査します。 · Hands-on benchmark for AI agents doing sysadmin work over SSH. |
| **BEVFormer on Blackwell / Hopper**<br>[互換パッチ・Docker環境](https://github.com/nabe2030/bevformer-blackwell) · [FP8/FP4 CUDAカーネル](https://github.com/nabe2030/bevformer-blackwell-fp4-fp8) | 自動運転向けBEVFormerをPyTorch 2.8とB200/H200で動かすための互換パッチと再現用Docker環境を公開。さらに、**mmcvのCUDAソースを解析し、変形アテンションと変形畳み込みのFP8/FP4カーネルを実装・チューニング**しました。B200とDGX Sparkで測定し、B200では低精度化によるデータ量の削減が処理の高速化に結びつかないことを確認しました。<br>Ported BEVFormer to PyTorch 2.8 on B200/H200, then profiled and analyzed mmcv’s CUDA source and implemented and tuned custom FP8/FP4 kernels for deformable attention and convolution. Benchmarks on B200 and DGX Spark documented where lower precision helped and where it did not. |
| **DGX Spark multi-node**<br>[2台で228.5GBを動かす](https://github.com/nabe2030/dgx-spark-2node-rpc) · [リング接続とRDMA](https://github.com/nabe2030/dgx-spark-ring-rdma) | DGX Spark 2台をConnectX-7で直結し、228.5GBのGLM-5.2をllama.cppのRPCで分けて動かした実測。RDMAとTCPの差、「200GbE」が100Gbps級×2であることを確認。リング接続の記事では、スイッチなしで4台以上つなぐ仕組みと、台数を増やす意味の限界を整理。 · Measured two-node DGX Spark over ConnectX-7 (RDMA vs. TCP), and analyzed switchless ring clusters and where scaling stops paying off. |
| [Strata on dual RTX 4060 Ti](https://github.com/nabe2030/strata-split-geforce-16gb) | 16 GBのGeForce 2枚で大規模MoEモデルを動かし、入力処理と出力生成の速度差、長文コンテキスト、エージェント業務での性能を比較。 · Multi-GPU inference and workload trade-offs on consumer hardware. |
| [Strata at a 524K context on Ryzen AI Max+ 395](https://github.com/nabe2030/strata-evo-x2-524k) | Strataのコンテクスト長を2倍の52万トークン（524,288）に拡大。日本語の選択問題300問で比べると、標準のYaRNでは18〜29問で答えが変化したのに対し、今回の手法は**全300問で元の設定と応答文まで完全一致**。Ryzen AI Max+ 395（EVO-X2）1台で、OpenCodeの実セッションを47万トークンまで実走しました。 · Doubled Strata’s context to 524,288 tokens with **zero changed answers: all 300 JamC-QA responses matched the original setting character for character**, where standard YaRN changed 18–29. Ran a real OpenCode session to 470K tokens on a single Ryzen AI Max+ 395. |
| [SGLang on a single DGX Spark](https://github.com/nabe2030/flashnext-dgx-spark) | 大規模モデルをDGX Spark 1台で動かす手順と、再起動時に大きなファイルを書き直す問題の調査。 · A single-node inference recipe and investigation of a slow restart path. |
| [Local LLM Agent Egress Guard](https://github.com/nabe2030/local-llm-agent-egress-guard) | ローカルAIエージェントの外向き通信をOSとネットワークで制限する設定例と受入テスト。 · OS and network controls for agent egress, with an acceptance test. |

## OSSへの報告・提案 | Upstream work

- **NVIDIA TensorRT / TensorRT Edge-LLM** — DGX SparkでNVFP4 W4A16推論の最初のトークンから出力が崩れる原因を、Q/K/V投影結果の結合処理まで切り分けました。TensorRT単体の最小再現例を報告し、Edge-LLMには実機で検証した1行の回避策を提案しました。<br>Traced incorrect output from the first token in NVFP4 W4A16 inference to the concatenation of Q/K/V projections. Reported a minimal TensorRT reproducer and proposed a one-line Edge-LLM workaround verified on DGX Spark. [TensorRT #4949](https://github.com/NVIDIA/TensorRT/issues/4949) · [TensorRT Edge-LLM #288](https://github.com/NVIDIA/TensorRT-Edge-LLM/issues/288)
- **SGLang** — DGX Sparkで再起動を遅くしていた書き込みを回避する変更を提案。別のユーザーによる実機での比較結果も記録されています。 · Proposed a restart optimization with an independent hardware validation report. [PR #42400](https://github.com/sgl-project/sglang/pull/42400)
- **Strata** — 16 GB GPU 2枚で起動できない条件を切り分け、再現条件と修正案を共有。 · Diagnosed a startup failure on dual 16 GB GPUs and shared a reproducer and proposed fix. [Issue #5187](https://github.com/Niko1221/Strata/issues/5187) · [PR #5258](https://github.com/Niko1221/Strata/pull/5258)（同等の修正が別PRで入ったためクローズ / Closed after an equivalent fix landed separately）

生成AI協会（GAIS）理事 / IoTメディアラボ理事  
Director at the Generative AI Society (GAIS) and IoT Media Lab

[Qiita](https://qiita.com/nabe2030) · [LinkedIn](https://www.linkedin.com/in/nabe2030/)
