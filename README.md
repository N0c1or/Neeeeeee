## Neeeeeee - 自动化 Web 漏洞挖掘工具

**N7e** 是一款基于 Rust 编写的自动化 Web 漏洞挖掘工具，专为高效、轻量化的漏洞扫描任务设计。它集成了资产搜集、存活扫描和 Nuclei 模板扫描，帮助安全人员快速发现和验证 Web 应用中的漏洞。

---

### 主要特点

- **★ 基于 Rust 开发，高效轻量**  
  N7e 使用 Rust 语言编写，无需额外依赖，运行速度快，资源占用极低，适合在各种环境中部署和使用。

- **★ 全流程自动化：资产搜集 → 存活扫描 → Nuclei 扫描**  
  从资产搜集到漏洞扫描，N7e 提供完整的自动化流程，显著提升漏洞挖掘效率，减少人工干预。

- **★ 支持 FOFA API，灵活自定义查询语句**  
  支持使用 FOFA API Key 进行资产搜集，允许用户自定义批量查询语句，灵活适应不同场景需求。

- **★ 开箱即用，自动生成配置模板**  
  工具首次运行时会自动生成 `config.ini` 配置文件模板，用户只需根据需求修改配置即可快速上手，无需复杂启动参数。

- **★ 高效处理大规模数据，内存占用极低**  
  支持单次处理几十万条数据，内存占用不超过 10MB，确保在资源有限的环境中也能稳定运行。

- **★ 数据冗余处理，避免重复测试**  
  自动去重 IP 和域名，确保不会对同一目标进行重复测试，所有测试链接均会记录，提升扫描效率。

- **★ 任务中断恢复，数据可续性**  
  关闭或重启工具不会丢失已测试存活的链接，未完成的任务会自动队列到下次任务结尾，确保扫描任务的连续性。

- **★ 多线程支持，高效并发扫描**  
  支持多线程并发存活扫描，用户可自定义线程数，显著提升存活扫描速度。

- **★ 自定义存活扫描超时时间**  
  用户可根据需求设置存活扫描的超时时间，灵活适应不同网络环境。

- **★ 支持 Nuclei 自定义 POC 路径**  
  用户可指定 Nuclei 的自定义 POC 路径，灵活适应不同的扫描场景。

---

### 快速开始

1. **下载并运行**  
   下载 N7e 可执行文件，直接运行即可。

2. **配置模板生成**  
   首次运行时会自动生成 `config.ini` 配置文件模板。

3. **修改配置**  
   根据需求修改配置文件中的 FOFA Key、Nuclei 配置等参数。

4. **启动扫描**  
   运行 N7e，工具会自动执行资产搜集、存活扫描和 Nuclei 扫描任务。

---

### 配置文件示例

```ini
[DEFAULT]

# FOFA 查询语句，支持多行，逗号分隔
query = [
    org="China Education and Research Network Center" && title="系统",
    org="China Education and Research Network Center" && title="管理",
    org="China Education and Research Network Center" && title="平台",
    org="China Education and Research Network Center" && title="教务",
    org="China Education and Research Network Center" && title="服务"
]

# FOFA的Key
fofa_key = FOFAKEY

# FOFA的查询URL
fofa_query_url_domain = https://fofa.info/

# FOFA的查询的api地址
fofa_query_url_path = api/v1/search/all

# FOFA的验证URL
fofa_query_info = api/v1/info/my

# FOFA单词最大查询数量
query_max = 10000

# 存活扫描的响应超时时间(s)
timeout = 10

# 存活扫描的线程数
max_threads = 16

# Nuclei 的严重性级别
nuclei_severity = critical,high

# Nuclei 并发数量
nuclei_concurrency = 3

# Nuclei 连接数
nuclei_connect = 20

# Nuclei 使用自定义POC路径
nuclei_poc_path = ""
'''
