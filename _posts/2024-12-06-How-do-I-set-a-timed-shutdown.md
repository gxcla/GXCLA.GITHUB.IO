---
title: 使用 `schtasks` 命令设置每天定时关机
layout: post
category: article
description: 定时关机能节省电能，保护设备，避免系统长时间运行造成损耗，也有助于养成良好作息与工作习惯，是高效生活与设备管理的实用助手。
---
通过 `schtasks` 命令，可以方便地设置 Windows 每天在指定时间自动关机。以下是步骤：

## 步骤：

1、 **打开命令提示符**  
   以管理员身份运行命令提示符（CMD）。

2、 **运行 `schtasks` 命令**  
   输入以下命令来创建一个每天定时关机的任务。以下命令设置任务每天晚上 22:00 执行关机操作：

   ```cmd
   schtasks /create /tn "ShutdownTask" /tr "shutdown -s -f" /sc daily /st 22:00
   ```

**参数说明**：

- `/tn "ShutdownTask"`：指定任务的名称为 `ShutdownTask`。你可以根据需要修改任务名称。

- `/tr "shutdown -s -f"`：指定要执行的命令，这里是`shutdown -s -f`，表示关机并强制关闭所有应用程序。

  - `-s` 表示关机。
  - `-f` 表示强制关闭正在运行的应用程序（如果有的话）。

- `/sc daily`：设置任务为 **每天** 触发。你也可以设置为其他频率，比如 `weekly`（每周）、`monthly`（每月）等。

- `/st 22:00`：指定任务开始执行的时间为 **22:00**。你可以修改为其他时间（例如 `08:30`）来指定每天执行关机的时间。

3、 **确认任务已创建**
   执行命令后，任务将会被添加到任务调度器中。你可以通过以下方式验证：

   - 打开任务调度器：按 `Win + R`，输入 `taskschd.msc`，然后按回车。
   - 在任务调度器的左侧栏找到 **任务调度器库**，检查是否有名为 `ShutdownTask` 的任务。

4、 **取消定时关机任务**
   如果你不再需要该定时关机任务，可以通过以下命令删除该任务：

   ```cmd
   schtasks /delete /tn "ShutdownTask"
   ```

## 示例：

每晚 22:00 自动关机的完整命令：

```cmd
schtasks /create /tn "ShutdownTask" /tr "shutdown -s -f" /sc daily /st 22:00
```

这条命令将创建一个名为 `ShutdownTask` 的任务，确保每天 22:00 自动关机。

## 其他设置

如果你想设置任务在特定的日期或条件下执行，可以根据需要修改命令中的参数。例如：

- **设置任务为每周触发**：

  ```cmd
  schtasks /create /tn "ShutdownTask" /tr "shutdown -s -f" /sc weekly /d MON /st 22:00
  ```

  - `/sc weekly`：任务每周触发。
  - `/d MON`：设置为每周的周一执行。

- **设置任务为特定日期触发**：

  ```cmd
  schtasks /create /tn "ShutdownTask" /tr "shutdown -s -f" /sc once /st 22:00 /sd 2024/12/05
  ```

  - `/sc once`：任务仅在某个特定的日期执行。
  - `/sd 2024/12/05`：指定任务开始执行的日期。

- **设置任务为每月执行**：

  ```cmd
  schtasks /create /tn "ShutdownTask" /tr "shutdown -s -f" /sc monthly /d 1 /st 22:00
  ```

  - `/sc monthly`：任务每月执行。
  - `/d 1`：设置为每月的第一天执行任务。

## 任务修改与管理

- **查看现有任务**： 使用以下命令查看任务调度器中所有的任务：

  ```cmd
  schtasks /query
  ```

- **修改任务**： 如果你需要修改现有任务的时间或频率，可以使用以下命令：

  ```cmd
  schtasks /change /tn "ShutdownTask" /st 23:00
  ```

  这将更改 `ShutdownTask` 任务的执行时间为 23:00。

- **删除任务**： 如果不再需要任务，可以删除它：

  ```cmd
  schtasks /delete /tn "ShutdownTask"
  ```

## 总结

通过 `schtasks` 命令，你可以非常方便地设置每天、每周、每月或某个特定日期执行的自动关机任务。调整任务的时间、频率或执行条件，只需要修改命令中的相应参数。

```
这个文档详细描述了如何使用 `schtasks` 命令设置每天、每周、每月或特定日期自动关机任务，同时包括了常用参数的说明和命令的管理方式。
```
