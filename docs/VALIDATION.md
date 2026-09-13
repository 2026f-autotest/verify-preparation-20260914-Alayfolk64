# 2026f 课程 2074 验证记录

来源：[LearningOS/2026s-oscamp-base-2026s-oscamp-base-exercise-oscamp-base-experiment](https://github.com/LearningOS/2026s-oscamp-base-2026s-oscamp-base-exercise-oscamp-base-experiment)，提交 `1196ac363c2cba1dcd7f33cf584b5d746f396ffd`。

## 已完成的实际验证（2026-09-14）

已创建公开模板 [2026f-oscamp-base](https://github.com/2026f-autotest/2026f-oscamp-base)，并真实执行 `python3 enroll.py Alayfolk64`，创建 [首个学员仓库](https://github.com/2026f-autotest/2026f-oscamp-base-Alayfolk64)。

组织 Secret `OSCAMP_2026F_BASE_TOKEN` 的访问范围为 Public repositories。学员仓库变量 `STUDENT_GITHUB` 已设为 `Alayfolk64`；[建仓后的配置检查](https://github.com/2026f-autotest/2026f-oscamp-base-Alayfolk64/actions/runs/34775639102) 和 [最终 push 的配置检查](https://github.com/2026f-autotest/2026f-oscamp-base-Alayfolk64/actions/runs/34775995328) 均通过。学员仓库未单独复制课程 Secret。

| 验证 | 实际结果 |
| --- | --- |
| 源码与权重 | 全量比较 2026s 的 24 项权重与运行目标，一致；实验、测试源码和上游 Cargo.lock 未修改 |
| 定向回归 | 16 项通过，覆盖建仓重试、身份、课程隔离、不完整结果、错误分数、原始退出状态及接口业务错误 |
| 模板真实 CI | [34775608460](https://github.com/2026f-autotest/2026f-oscamp-base/actions/runs/34775608460)，实际 0/100；模板不上传成绩 |
| 学员首次主动 push | [34775686458](https://github.com/2026f-autotest/2026f-oscamp-base-Alayfolk64/actions/runs/34775686458)，实际 0/100，OpenCamp 接受 |
| 固定工具链后的完整重测 | [34775995308](https://github.com/2026f-autotest/2026f-oscamp-base-Alayfolk64/actions/runs/34775995308)，实际 0/100，OpenCamp 再次接受 |

最后一次评测代码提交为 `c186632`，使用 Ubuntu 24.04、Rust **1.98.1**、RISC-V GCC 和 QEMU user mode。编译产物放在仓库 `tmp/target`，24 项评测均有完整日志和结果，没有以缺少测试或缺少环境代替真实评测。

上传日志原文：

```text
Course 2074: 0/100 points; 0/24 exercises passed.
Submitting measured score: course=2074, student=Alayfolk64, score=0/100
OpenCamp accepted the score (result=1).
```

## 如何理解红色评测状态

上游模板保留未完成的实验，实际 Cargo 测试返回 101，各项未通过。因此 **Test exercises and calculate score** 作业会在记录结果后标红，**Save measured score and upload to OpenCamp** 作业成功。这符合往期“上传真实部分得分”的规则；0 分来自真实测试，没有上传伪造的通过结果。

本轮验证了课程 2074 的接口接受 0/100，不代表已验证学员完成全部实验后的 100/100，也未声称核对了 OpenCamp 网页显示。未访问或修改 OpenCamp 管理后台。

首个账号同时是组织所有者，已具备仓库权限；普通外部学员接受邀请的页面操作尚未用第二个账号实测。自助 Issue 领取入口尚未接入，维护者当前仍运行 `enroll.py` 分配仓库。

## 复核入口

```sh
python3 -m unittest discover -s .github/tests
```

在仓库根目录运行 16 项定向回归；`-s` 指定测试目录，测试不创建真实远程仓库或上传课程分数。Python 语法、两份工作流的 YAML 解析及 `git diff --check` 均通过。

维护者本地原始证据位于 `tmp/enroll-Alayfolk64.log`、`tmp/template-run-34775608460.log`、`tmp/student-push-34775686458.log`、`tmp/student-push-34775995308.log`。每次 GitHub 运行也上传完整结果 JSON、逐项原始日志和 Cargo.lock；当前成绩明细在学员仓库 `gh-pages:course-2074.json`。

## 秋冬季页面与排行榜核对

2026-09-14 只读核对 [OpenCamp 基础阶段](https://opencamp.cn/os2edu/camp/2026fall/stage/4) 的公开页面数据，课程编号为 2074。按该页面使用的排行榜查询接口核对，`Alayfolk64` 的记录为 0 分，与真实 CI 测得及上传的分数一致。浏览器完整表格受自动化连接限制，未声称完成视觉验收。未修改 OpenCamp 后台。

## 自助领取

统一入口 [2026f-autotest/enroll](https://github.com/2026f-autotest/enroll) 已启用；本课程已用维护者账号验证新 Issue 自动触发、识别申请人、配置仓库、回复链接及配置检查成功。该次沿用已有课程仓库；外部学员接受邀请尚未用第二个账号实测。见[入口验证记录](https://github.com/2026f-autotest/enroll/blob/main/docs/VALIDATION.md)。
