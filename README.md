# DABIC Gravity Vinton 题目提交包说明

本压缩包是 `dabic_gravity_vinton` 题目的当前提交材料包，包含题目配置、评分文件、starter/data/docs、30min 与 2h agent 运行及复评证据、QC 自查材料和分数曲线图。


## 1. 评分标准

当前主评分文件为：

- `judge_files/eval_dabic_v2.py`
- SHA256：`71ca4da82c850baf49206e16c79023210c58429c3b1f17154c02dfbec57b2409`

当前任务配置为：

- `task/dabic_gravity_vinton.json`
- SHA256：`daa9f55a3d8faff7b66ca0d9b8048c4339006dcd6f87f6906fefc9b099ecaf77`
- `parser=structured_json`
- `selection=valid_then_score`



## 2. 项目要求与结果

项目要求：

- agent 运行 30min：分数不能超过 15。
- agent 运行 2h：分数不能超过 30。

本包主结果：

| 证据 | run id | 分数 | 要求 | 结论 |
| --- | --- | ---: | ---: | --- |
| 30min final recheck | `dabic-30min-v37-final-recheck` | `14.805673577806198` | `<= 15` | 通过 |
| 2h fresh run | `dabic-2h-v37-agent-rerun-001` | `17.42871919045102` | `<= 30` | 通过 |
| 2h best auto-21 recheck | `dabic-2h-v37-agent-rerun-001-auto21-recheck` | `17.39920179678114` | `<= 30` | 通过 |
| 2h final archive recheck | `dabic-2h-v37-agent-rerun-001-final-recheck` | `16.7391753739695` | `<= 30` | 通过 |

说明：

- 30min 的原始 agent 运行轨迹保存在 `results/agent_runs_original/30min_agent_run/`，用于审查 agent 行为。
- 30min 的最终提交分数以当前评分标准下的复评结果为准，即 `results/fresh_current_scorer/30min_final_recheck/manual-1/report.json`。
- 2h 是在当前评分标准下重新跑出的完整 agent 结果，主结果为 `results/fresh_current_scorer/2h_full_run/final_result.json`。

## 3. 关键目录

- `task/`：当前 SE-Bench task 配置。
- `judge_files/`：当前评分器源码。
- `starter/`：题目给 agent 的 starter 文件。
- `data/`：题目数据。
- `docs/task_refs/`：题目相关参考文献。
- `docs/process_refs/`：项目执行指南、题目优化流程、历史质检反馈等过程文件。
- `environment/`：环境说明。
- `results/fresh_current_scorer/`：本次提交的主结果证据，均对应当前评分标准。
- `results/agent_runs_original/`：原始 agent 行为溯源材料。
- `qc/`：分数汇总、bug 修复自查、哈希校验、曲线图和作图数据。

## 4. 推荐审查入口

建议优先查看以下文件：

- `qc/score_summary.json`：机器可读的主分数汇总。
- `qc/qc_summary.md`：评分 bug 修复和剩余注意事项说明。
- `qc/scorer_hashes.txt`：评分文件、task 配置、关键 report 的哈希清单。
- `qc/dabic_30min_2h_score_curves.png`：30min 与 2h 分数曲线图。
- `qc/dabic_30min_2h_score_curves.csv`：曲线图对应的数据源。
- `results/fresh_current_scorer/30min_final_recheck/manual-1/report.json`：30min 当前评分标准复评 report。
- `results/fresh_current_scorer/2h_full_run/final_result.json`：2h 当前评分标准完整运行结果。
- `results/fresh_current_scorer/2h_best_auto21_recheck/manual-1/report.json`：2h 最优提交离线复评 report。

## 5. 已处理的历史问题

本包当前状态：

- E-monitor 使用隐藏算例真实规模集合 `[80, 252, 500]` 和 cell sizes `[600, 1800, 4480]`，不再用 `1271` 判定数据空间。
- `valid` 与结构惩罚解耦，当前 2h 复评中 `valid=true`、`is_data_space=true`、`n_data_space_matrix_matches=34`。
- 当前 task 使用 `structured_json`，不是 fake `score_sum` case 展开。
- 当前 report 中保留了 `raw_total`、`structural_penalty`、`penalty_reason`、`valid_for_selection`、`is_data_space`、`data_sizes_used`、`cell_sizes_used` 等诊断字段。## 6. 哈希校验


## 6. 曲线图说明

曲线图位于：

- `qc/dabic_30min_2h_score_curves.png`
- `qc/dabic_30min_2h_score_curves.svg`

图中包含：

- 上半部分：每次提交的 score。
- 下半部分：best-so-far 曲线。
- 蓝色：30min 原始 agent 行为轨迹。
- 蓝色虚线：30min 在当前评分标准下的最终复评分数 `14.8057`。
- 橙色：2h 当前评分标准完整运行轨迹，最优点为 `auto-21 / 17.43`。

作图数据源为：

- `qc/dabic_30min_2h_score_curves.csv`

