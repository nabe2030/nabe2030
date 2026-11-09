# 渡辺 誠 | Makoto Watanabe

**GPUインフラ・ローカルLLM・AIエージェントの実機検証**

限られた計算資源で、どのAIモデルが動き、どこまで現場の仕事を任せられるかを検証しています。GPUや推論エンジンの選定から、性能と品質の比較、運用時の権限・通信制御まで扱います。公開リポジトリには、検証条件、再現手順、実測データ、分かったこととその限界を残しています。

I test what AI models can run on available hardware and which real-world tasks they can handle. My work covers GPU infrastructure, local inference, and agent evaluation, with reproducible setups and measurements that help teams choose what to deploy.

## 代表プロジェクト | Selected work

| プロジェクト | 内容 |
| --- | --- |
| [GembaBench](https://github.com/nabe2030/gembabench) | AIエージェントにサーバー調査、侵入分析、更新、脆弱性対応を任せられるかを評価。報告書に加え、作業後のサーバーの状態やサービスの動作も検査します。 · Hands-on benchmark for AI agents doing sysadmin work over SSH. |
| [BEVFormer on Blackwell / Hopper](https://github.com/nabe2030/bevformer-blackwell) | 自動運転向けのBEVFormerをPyTorch 2.8とB200/H200で動かすための互換パッチとDocker環境。GPU更新による性能差も実測しました。 · Compatibility patches, a Docker setup, and training performance measurements on B200 and H200. |
| [Strata on dual RTX 4060 Ti](https://github.com/nabe2030/strata-split-geforce-16gb) | 16 GBのGeForce 2枚で大規模MoEモデルを動かし、入力処理と出力生成の速度差、長文コンテキスト、エージェント業務での性能を比較。 · Multi-GPU inference and workload trade-offs on consumer hardware. |
| [SGLang on a single DGX Spark](https://github.com/nabe2030/flashnext-dgx-spark) | 大規模モデルをDGX Spark 1台で動かす手順と、再起動時に大きなファイルを書き直す問題の調査。 · A single-node inference recipe and investigation of a slow restart path. |
| [Local LLM Agent Egress Guard](https://github.com/nabe2030/local-llm-agent-egress-guard) | ローカルAIエージェントの外向き通信をOSとネットワークで制限する設定例と受入テスト。 · OS and network controls for agent egress, with an acceptance test. |

## OSSへの報告・提案 | Upstream work

- **SGLang** — DGX Sparkで再起動を遅くしていた書き込みを回避する変更を提案。別のユーザーによる実機での比較結果も記録されています。 · Proposed a restart optimization with an independent hardware validation report. [PR #42400](https://github.com/sgl-project/sglang/pull/42400)
- **Strata** — 16 GB GPU 2枚で起動できない条件を切り分け、再現条件と修正案を共有。 · Diagnosed a startup failure on dual 16 GB GPUs and shared a reproducer and proposed fix. [Issue #5187](https://github.com/Niko1221/Strata/issues/5187) · [PR #5258](https://github.com/Niko1221/Strata/pull/5258)

センスウェイ CTO / 生成AI協会（GAIS）理事 / IoTメディアラボ理事  
CTO at SenseWay · Director at the Generative AI Society (GAIS) and IoT Media Lab

[Qiita](https://qiita.com/nabe2030) · [LinkedIn](https://www.linkedin.com/in/nabe2030/)
