# Rotating Cross-Cylinder Varifocal Lens / 旋转交叉柱镜变焦镜片

**A low-cost continuous axial varifocal lens based on a rotating Jackson Cross Cylinder (JCC) + fixed slit + add cylinder — open-source research series**

**一种基于旋转交叉柱镜（JCC）+ 固定裂隙 + 附加柱镜的低成本连续轴向变焦镜片 —— 开源研究系列**

---

## English / English 简介

**Rotating Cross-Cylinder Varifocal Lens: Mechanisms, Design, Verification, and Roadmap**

This repository releases the complete research series of a low-cost continuous axial varifocal lens that shifts the focal plane along the optical axis **without changing the physical focal length**. The scheme recombines three mature optical elements:

- **Jackson Cross Cylinder (JCC)** — provides orientation-tunable pure astigmatism as the varifocal phase source (+1.00 DC × 90 / −1.00 DC × 180, M=0, J0=+1.00 D);
- **Fixed slit** (at 180°, not synchronously rotating) — spatial filtering and axial energy concentration;
- **Add cylinder Cadd** (axis 180°, parallel to the slit long axis) — controls the focal plane position.

When the JCC rotates, the time-averaged wavefront coefficient vanishes (⟨c5⟩=⟨c6⟩=0) while the time-averaged focal-line intensity forms a stable on-axis energy concentration. This is a **geometric wavefront-shaping mechanism (intensity time averaging), not an interference effect** — therefore it **remains effective under white light** (brightness gain ≈2.44×, close to the monochromatic 550 nm value of 2.46×).

**Zoom law:**

> **z_peak ≈ 1/(1+Cadd)**  (Cadd in D, z in m) — verified over 0.5–19D: 0D→1000 / 1D→500 / 2D→335 / 4D→200 / 9D→100 / 19D→50 mm.

**Verification (two independent groups, ≤1% deviation):**

- numpy numerical group: N=2048/4096, λ=550 nm, 5 mm aperture, FFT / angular-spectrum (ASM) / 1D Fresnel cross-checks, grid-convergence deviation 0.42%;
- Ansys Zemax OpticStudio 2023 R1 reproduction group: Huygens PSF 128×128, ImageDelta=40 µm, circular aperture R=2.5 mm ∩ rectangular slit half-width 0.5 mm.

**Key conclusions:**

1. **Slit spatial-filtering brightening**: slit-vs-open gains 14.2×/17.5×/13.9× at stations 1/2/3 (Zemax convention); rectangular slit 2 mm×5 mm throughput ≈49.5%; brightness–image-quality trade-off bounded by the Sturm separation = 1/Cadd.
2. **Slit shape design**: width dominates efficiency (rectangular efficiency 36.4 highest at Cadd=9D); at Cadd=19D soft-edge shapes outperform the rectangle by ≈2.2× (Gaussian soft-edge 8.0 vs. rectangular 3.7), suppressing hard-edge diffraction sidelobes.
3. **Distance matching to human working distances**: near reading (0.3–0.4 m) covered by 2–4D (gain 2.6–3.6×), mid-range (0.75–1 m) by 0.5–1D (gain ≈1+), near field (z=0.01 m) reaches ≈130× at Cadd≈99D (microscopy / near-eye boundary); all stations >1D attenuate at z≥1.5 m (0.4–0.6×).
4. **Non-liquid-crystal architecture reconstruction**: removing the physical slit yields 22.9/24.5/21.8× at 4/9/19D; removing the JCC adds 5–20%; final architecture = fixed positive-sphere coarse stages (S=4/9/19D) + tunable cylindrical phase for fine zoom (0–1D) — **no physical slit, no mechanical rotation, no liquid-crystal actuating element**; zoom travel compressed by ≈47% (Cadd 0→9D: 1000→100 mm reduces to 100→53 mm with S9).

> **Gain-convention note**: the S9_Cadd0 peak 4605.49@100 mm is a peak-intensity ratio of ≈100× relative to the slitless full aperture (S0_Cadd0) — a **peak-intensity convention, NOT a power gain**. Baselines differ; do not compare directly with other gains.

**Repository contents / 仓库内容:**

- Review paper (this series overview, EN/中文) & four topical papers P1–P4 (pending submission);
- Patent concepts C1–C4 (utility model + inventions);
- Simulation source code and datasets (json/png, all conclusions traceable);
- Desktop optical verification plan (4 experiments, pass criteria ≤10% deviation) & procurement tiers;
- Open-source declaration and author statement (below).

**Limitations:** all conclusions are from pure simulation (numpy + Zemax reproduction); no physical prototype verified yet. MTF/PSF/color (white-light multi-wavelength aberration) and electro-optic device parameters (phase error ±0.05λ, throughput, response time 5–20 ms design) await process-level measurement. Desktop verification can start at ≈0.5–1 万 CNY (four criteria, ~1500 CNY tier fully quantitative).

---

## 中文 / Chinese 简介

**《旋转交叉柱镜变焦镜片研究总述：机制、设计、验证与路线图》**

本仓库发布一套低成本连续轴向变焦镜片的完整研究系列：旋转交叉柱镜（JCC）+ 固定裂隙片 + 附加柱镜组合，可在**不改变物理焦距**的前提下实现焦面轴向位置的可控移动。

方案由三件成熟光学元件组合而成：

- **交叉柱镜（JCC）**：提供方位角可调的纯像散，作为变焦相位源（+1.00 DC × 90 / −1.00 DC × 180，M=0、J0=+1.00 D）；
- **固定裂隙片**（固定 180° 方位，不与 JCC 同步旋转）：实现空间滤波与轴向能量集中；
- **附加柱镜 Cadd**（轴 180°，平行裂隙长轴）：控制焦面位置。

JCC 旋转时，波前系数时均归零（⟨c5⟩=⟨c6⟩=0），而焦线强度时均形成稳定的轴上能量集中。该机制属于**几何波前整形（强度时均），而非干涉型变焦**，因此**白光下不失效**（宽谱白光焦面窗口能量增亮约 2.44×，近似单色 550 nm 的 2.46×）。

**变焦规律：**

> **z_peak ≈ 1/(1+Cadd)**（Cadd 单位 D，z 单位 m）——0.5~19D 范围内与仿真吻合：0D→1000 / 1D→500 / 2D→335 / 4D→200 / 9D→100 / 19D→50 mm。

**验证（双口径独立交叉验证，偏差 ≤1%）：**

- numpy 数值仿真组：N=2048/4096、λ=550 nm、孔径 5 mm、FFT / 角谱传播（ASM）/ 1D Fresnel 复核，网格收敛偏差 0.42%；
- Ansys Zemax OpticStudio 2023 R1 独立复现组：Huygens PSF 128×128、ImageDelta=40 µm、圆孔 R=2.5 mm ∩ 矩形裂隙半宽 0.5 mm。

**核心结论：**

1. **裂隙空间滤波增亮**：裂隙 vs 全开增益 1D 14.2× / 2D 17.5× / 3D 13.9×（Zemax 口径）；矩形裂隙 2 mm×5 mm 进光量约 49.5%；增亮—像质权衡按 Sturm 间距 = 1/Cadd 界定。
2. **裂隙形状设计**：宽度主导效率（Cadd=9D 矩形效率 36.4 全表最高）；Cadd=19D 档软边形状效率反超矩形约 2.2 倍（高斯软边 8.0 vs 矩形 3.7），并抑制硬边衍射旁瓣。
3. **变焦距离匹配**：近读距（0.3~0.4 m）由 2~4D 档覆盖（增益 2.6~3.6×），中距（0.75~1 m）由 0.5~1D 档覆盖（增益≈1 略增），近场（z=0.01 m）高 Cadd 档增益约 130×（99D，显微/近眼边界）；所有 >1D 档在 z≥1.5 m 衰减（0.4~0.6×）。
4. **非液晶架构重构**：删物理裂隙增益 4D 22.9× / 9D 24.5× / 19D 21.8×；删 JCC 额外 5~20%；最终架构为"固定正球镜粗分档（S=4/9/19D）+ 可调柱面相位精细变焦（0~1D）"——**无物理裂隙、无机械旋转、无液晶执行元件**；变焦行程压缩约 47%（Cadd 0→9D：1000→100 mm 缩为 100→53 mm）。

> **增益口径声明**：S9_Cadd0 峰值 4605.49@100 mm 为相对无裂隙全孔径（S0_Cadd0）的峰值强度比约 100×，属**峰值强度口径而非功率增益**；不同基准的增益（如 Zemax 同系统裂隙/全开 ≈5.4×）不可直接比较。

**仓库内容：**

- 研究总述论文（本综述，中英文版）与四篇分主题论文 P1~P4（待投稿）；
- 专利构思 C1~C4（实用新型 + 发明）；
- 全部仿真源代码与数据集（json/png，所有结论可追溯）；
- 桌面光学验证方案（四组实验，判据偏差 ≤10%）与采购套餐；
- 开源声明与作者声明（见下）。

**局限说明**：全部结论来自纯仿真（numpy 数值组 + Zemax 复现组），尚未完成实物样机验证；MTF/PSF/色差（白光多波长像差）及电控器件参数（相位误差 ±0.05λ、透过率、响应速度设计值 5~20 ms）待工艺实测。桌面验证约 0.5~1 万元器材即可启动（约 1500 元套餐即可覆盖四组判据的全量定量）。

---

## Open Source Declaration / 开源声明

**English:**

The "Rotating Cross-Cylinder Varifocal Lens Project" (including the integrated review paper, four topical papers, patent concepts, and all experimental source code) is hereby released to the public as an **open-source project**.

All ideas, principles, methods, design parameters, simulation data, and source code of this project are freely available to everyone for research, study, secondary development, and **non-commercial application**. **No organization or individual may use them for commercial monopoly**, including but not limited to: monopolizing this technology or its derivatives through exclusive licensing, patent blocking, exclusive commercial operation, or erection of technical barriers.

Openness and sharing are the cornerstone of technological progress. As a low-cost, continuously axial-zoom optical solution, the true value of the rotating cross-cylinder varifocal lens lies in being seen, verified, improved, and applied by more people in the field of vision health. Any form of commercial monopoly runs counter to the original purpose of this project's release.

**中文：**

「旋转交叉柱镜变焦镜片项目」（含研究总述论文、四篇分主题论文、专利构思与全部实验源代码）自发布之日起，作为**开源项目**向全社会公开发布。

本项目所有思想、原理、方法、设计参数、仿真数据与源代码，均允许任何人自由研究、学习、二次开发与**非商业应用**。任何组织或个人**不得**将其用于**商业垄断**，包括但不限于：以独占授权、专利封锁、排他性商业运营、设置技术壁垒等方式垄断该技术或其衍生技术。

开放与共享才是技术进步的基石。旋转交叉柱镜变焦镜片作为一种低成本、连续轴向变焦的光学方案，其真正价值在于被更多人看到、验证、改进并应用于视力健康领域。任何形式的商业垄断行为，都与本项目发布的初衷相违背。

## About the Author / 作者情况

**English:** The author is currently affiliated with **no institution** and has independently completed the theoretical research, numerical simulation, and document organization of this project. The author sincerely hopes to find a platform — a research institution, university laboratory, open-source community, incubator, or any other supporting platform — to help continue the related research, including but not limited to: desktop optical verification experiments, engineering prototype development, patent portfolio building, and paper submission. If your platform is interested, you are welcome to contact the author to jointly promote this technology from simulation to real-world application.

**中文：** 作者目前**没有依托单位**，独立完成了本项目的理论研究、数值仿真与文档整理工作。作者诚挚地希望找到一个平台——科研机构、高校实验室、开源社区、孵化器或其他任何形式的支持性平台——帮助其继续开展相关研究，包括但不限于：桌面光学验证实验、工程样机开发、专利布局与论文投稿。如您所在的平台对该项目感兴趣，欢迎通过下方联系方式联系作者，共同推动这项技术从仿真走向真实应用。

## Contact / 联系方式

- Email 1 / 邮箱1：18075129206@163.com
- Email 2 / 邮箱2：lllkopi@proton.me
- Phone / 电话：18075129206
- QQ：1825178962
- WeChat / 微信：he65841

---

*Declaration date / 声明日期：October 21, 2026 / 2026年10月21日*

*This declaration is released together with the project documents and source code and constitutes an integral part of the project's open-source licensing. / 本声明与项目文档、源代码一同发布，构成项目开源许可的整体组成部分。*
