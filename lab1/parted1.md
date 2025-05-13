
fdisk 适用于dos 分区 
parted 适用于gpt 分区



在 `parted` 分区时确保 分区对齐（alignment） 对磁盘性能（尤其是 SSD/NVMe）非常重要。以下是具体操作步骤和验证方法，确保分区按 `optimal`（最佳）对齐：

---

**1. 检查当前磁盘的对齐状态**
```bash
sudo parted /dev/vdb align-check optimal 1  # 检查第1个分区的对齐（如果存在）
```
• 返回 `1 aligned` 表示已对齐，`0 not aligned` 表示未对齐。


---

**2. 创建对齐分区的完整流程**
**方法1：交互式分区（推荐）**
```bash
sudo parted /dev/vdb
```
在交互模式中执行：
```plaintext
(parted) mklabel gpt                      # 创建GPT分区表（对齐更友好）
(parted) unit s                           # 切换到扇区单位（sectors）
(parted) print                            # 查看磁盘的扇区大小（如512B或4K）
(parted) mkpart primary 2048s 33%        # 从2048扇区（1MB）开始，确保对齐
(parted) mkpart primary 33% 66%          # 后续分区自动对齐
(parted) mkpart primary 66% 100%         # 剩余空间
(parted) align-check optimal 1           # 验证第1分区对齐
(parted) quit
```

**关键点**：
• 起始扇区：现代磁盘建议从 `2048s`（即1MB）开始，避开保留区域。

• 百分比分配：使用百分比（如 `33%`）时，`parted` 会自动计算对齐的位置。


---

**方法2：非交互式命令（脚本中使用）**
```bash
sudo parted -s /dev/vdb -- \
  mklabel gpt \
  mkpart primary 2048s 33% \
  mkpart primary 33% 66% \
  mkpart primary 66% 100%
```

---

**3. 验证所有分区对齐**
```bash
# 检查所有分区是否对齐
sudo parted /dev/vdb align-check optimal 1
sudo parted /dev/vdb align-check optimal 2
sudo parted /dev/vdb align-check optimal 3
```
• 每个命令应返回 `X aligned`（X为分区号）。


---

**4. 高级对齐设置（手动计算）**
如果需精确控制扇区对齐（例如 4K 高级格式磁盘）：
```bash
# 计算起始扇区（示例：4K对齐）
SECTOR_SIZE=4096   # 假设磁盘物理扇区为4K
START_SECTOR=$(( 4096 / 512 ))  # 转换为512B逻辑扇区（通常为8s）

sudo parted -s /dev/vdb -- \
  mklabel gpt \
  mkpart primary ${START_SECTOR}s 33% \
  mkpart primary 33% 66% \
  mkpart primary 66% 100%
```

---

**5. 分区后格式化（保持对齐）**
```bash
# 格式化时启用块对齐（ext4示例）
sudo mkfs.ext4 -E stride=128,stripe-width=128 /dev/vdb1
```
• `stride` 和 `stripe-width` 参数适用于RAID/SSD优化（根据实际配置调整）。


---

**为什么对齐重要？**
| 场景 | 未对齐的影响 |
|------|--------------|
| SSD/NVMe | 写入放大，寿命缩短 |
| 4K高级格式磁盘 | 性能下降10-50% |
| RAID | 条带化失效，速度降低 |

---

**总结命令**
```bash
# 完整流程：创建GPT表 + 3个对齐分区
sudo parted -s /dev/vdb -- \
  mklabel gpt \
  mkpart primary 2048s 33% \
  mkpart primary 33% 66% \
  mkpart primary 66% 100% \
  align-check optimal 1 \
  align-check optimal 2 \
  align-check optimal 3
```

通过上述操作，可确保分区在物理扇区、文件系统块和RAID条带上均保持最佳对齐。