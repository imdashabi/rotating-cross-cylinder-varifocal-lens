# 旋转交叉柱镜变焦镜片项目 — 实验源代码

本项目实验全部为数值仿真（numpy 组）与光学设计软件复现（Zemax 组）双口径交叉验证。
本压缩包按两组归档，包含全部实验脚本、最终版 Zemax 复现脚本、复现日志与 Zemax 模型文件。

## 目录结构

```
旋转交叉柱镜变焦镜片实验源代码/
├── README.md
├── numpy组/   # 25 个 numpy 数值仿真脚本
└── Zemax组/   # 最终版复现脚本 zmx_mvp31e/32 + 日志 + jcc_*.zmx 模型
```

## numpy 组脚本用途

| 脚本 | 用途 |
|---|---|
| exp1_static_psf.py | 实验1：JCC+固定裂隙静态 PSF（焦线形成与形状） |
| exp2_slit_width_scan.py | 实验2：裂隙宽度扫描（13 档 5.00→0.05 mm） |
| exp2b_huygens.py | 实验2 对照：Huygens 近似口径模拟 |
| exp2c_slit_width_v3.py | 实验2 第三版：宽度扫描复验（exp2_slit_width_scan_v3） |
| exp3_multiwavelength_z.py | 实验3：多波长（380–780 nm）轴向扫描（白光增亮 2.44×） |
| exp3_probe_z.py | 实验3：近场 z 探针（z<0.15 m） |
| exp4_width_x_lambda.py | 实验4：宽度×波长 78 组合扫描 |
| exp5_jcc_rotation.py | 实验5：JCC 旋转 α 与 90−α 对称性 |
| exp678.py | 实验6/7/8：转速≥30rps、最优 Cadd=1.5D、进光量面积占比 |
| exp_compare.py | 全实验对比图（exp_all_compare_grid） |
| fft_analytic.py / fft_analytic2.py | FFT 衍射解析校验 |
| fft_compare.py | FFT vs 解析对比 |
| fft_paper_scan.py / fft_paper_scan2.py | 论文用 FFT 扫描 |
| fft_peak_report.py | FFT 峰值报告（fft_peak_compare） |
| slit_shape.py | 六种裂隙形状仿真 |
| slit_shape_fair.py | 六形状公平对比（slit_shape_fair.json 数据源） |
| sphere_prefocus.py | 固定正球镜前置扫描（sphere_prefocus_scan.json 数据源） |
| fp_redesign_1d.py | 一维架构重构（fp_redesign_1d.json 数据源） |
| fp_redesign_2d.py | 二维架构重构（fp_redesign_2d_cadd4/9/19.json 数据源） |
| locate_focus.py | z_peak≈1/(1+Cadd) 焦点定位 |
| plot_slit_fair.py | 六形状效率图（slit_shape_fair.png） |
| make_hd_gif.py | 高清动画 GIF（varifocal_JCC_animation_hd） |
| make_figs.py | 论文配图批量生成 |

## Zemax 组脚本用途

| 脚本 | 用途 |
|---|---|
| zmx_mvp31e.py | 球镜前置 S9 全开锚点复现（最终版；对应 log：zmx_mvp31e.log） |
| zmx_mvp32.py | 1D/2D 全开锚点复现（最终版；对应 log：zmx_mvp32.log） |

模型文件 jcc_*.zmx：JCC+裂隙变焦镜片的 Zemax 序列模式模型（含 1D/2D、全开/裂隙、
半径 R2.5、不同裂隙宽度、球镜前置 S9 等变体）。

## 依赖

- numpy 组：Python 3.x + numpy + scipy + matplotlib（gif 需要 imageio/Pillow）
- Zemax 组：Ansys Zemax OpticStudio 2023 R1（ZOS-API）+ pythonnet（.NET 互操作）

## 口径约定（重要）

- numpy 组：FFT/ASM 强度口径（N=2048/4096，λ=550 nm，孔径 5 mm，中心 ±1 mm 窗）
- Zemax 组：Huygens PSF 振幅口径（128×128，ImageDelta=40 µm），与 numpy 绝对数值不直接比较，
  仅对比趋势与增益量级（Zemax 增益约低 15–25%）
- 关键增益口径：S9_Cadd0 峰值 4605.49 为相对无裂隙全孔径峰值强度比（约 100×，非功率增益）；
  Zemax 裂隙/全开 ≈5.4× 为同系统内增益，二者基准不同不直接比较
