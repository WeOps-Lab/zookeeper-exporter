## 嘉为蓝鲸Zookeeper插件使用说明

## 使用说明
插件连接Zookeeper并执行命令：`mntr` 和 `ruok`。通过执行这些命令，插件会收集相关输出结果，并将其转化为监控指标以供分析。

### 插件功能

### 版本支持

操作系统支持: linux, windows

是否支持arm: 支持

**组件支持版本：**

部署模式支持: 单机(Standalone), 集群(Cluster)

**是否支持远程采集:**

是

### 参数说明

| **参数名**    | **含义**                                                                    | **是否必填** | **使用举例**       |
|------------|---------------------------------------------------------------------------|----------|----------------|
| --zk-hosts | Zookeeper服务的地址，可使用逗号分隔多个服务地址。例如 10.0.0.1:2181,10.0.0.2:2181,10.0.0.3:2181 | 是        | 127.0.0.1:2181 |
| --timeout  | 连接超时时间(s)                                                                 | 否        | 30             |

### 使用指引
需要确保zookeeper能够响应监控探针输入的命令。
注意从版本v3.4.10开始可能需要 `mntr` 命令白名单，详情参考: [4lw.commands.whitelist](https://zookeeper.apache.org/doc/current/zookeeperAdmin.html)  

测试mntr结果  
```shell
echo mntr | nc 127.0.0.1 2181
zk_version      3.4.13-2d71af4dbe22557fda74f9a9b4309b15a7487f03, built on 06/29/2018 04:05 GMT
zk_avg_latency  0
zk_max_latency  0
zk_min_latency  0
zk_packets_received     1
zk_packets_sent 0
zk_num_alive_connections        1
zk_outstanding_requests 0
zk_server_state standalone
zk_znode_count  51
zk_watch_count  0
zk_ephemerals_count     0
zk_approximate_data_size        621501
zk_open_file_descriptor_count   38
zk_max_file_descriptor_count    1048576
zk_fsync_threshold_exceed_count 0
```

测试ruok结果  
```shell
echo ruok | nc 127.0.0.1 2181
imok%  
```  

**注意**  
能采集到的监控指标与zookeeper版本有关，如果发现监控指标有缺失，请检查mntr和ruok是否能显示对应的字段，否则监控探针无法转换为对应的指标。  

### 指标简介  

| **指标ID**                           | **指标中文名**             | **维度ID** | **维度含义**      | **单位** |
|------------------------------------|-----------------------|----------|---------------|--------|
| zk_up                              | ZooKeeper监控探针运行状态     | zk_host  | zookeeper服务地址 | -      |
| zk_uptime                          | ZooKeeper服务已运行时长      | zk_host  | zookeeper服务地址 | ms     |
| zk_version                         | ZooKeeper版本           | zk_host  | zookeeper服务地址 | -      |
| zk_server_leader                   | ZooKeeper主节点          | zk_host  | zookeeper服务地址 | -      |
| zk_ruok                            | ZooKeeper健康状态         | zk_host  | zookeeper服务地址 | -      |
| zk_avg_latency                     | ZooKeeper平均延迟         | zk_host  | zookeeper服务地址 | ms     |
| zk_max_latency                     | ZooKeeper最大延迟         | zk_host  | zookeeper服务地址 | ms     |
| zk_min_latency                     | ZooKeeper最小延迟         | zk_host  | zookeeper服务地址 | ms     |
| zk_num_alive_connections           | ZooKeeper活跃连接数        | zk_host  | zookeeper服务地址 | -      |
| zk_connection_rejected             | ZooKeeper拒绝连接数        | zk_host  | zookeeper服务地址 | -      |
| zk_sessionless_connections_expired | ZooKeeper失效会话连接数      | zk_host  | zookeeper服务地址 | -      |
| zk_connection_drop_count           | ZooKeeper连接断开数        | zk_host  | zookeeper服务地址 | -      |
| zk_global_sessions                 | ZooKeeper全局会话数        | zk_host  | zookeeper服务地址 | -      |
| zk_watch_count                     | ZooKeeper当前Watch数量    | zk_host  | zookeeper服务地址 | -      |
| zk_ephemerals_count                | ZooKeeper临时节点数量       | zk_host  | zookeeper服务地址 | -      |
| zk_znode_count                     | ZooKeeper节点数量         | zk_host  | zookeeper服务地址 | -      |
| zk_open_file_descriptor_count      | ZooKeeper打开文件描述符数量    | zk_host  | zookeeper服务地址 | -      |
| zk_max_file_descriptor_count       | ZooKeeper最大文件描述符数量    | zk_host  | zookeeper服务地址 | -      |
| zk_fsync_threshold_exceed_count    | ZooKeeper超过fsync阈值的次数 | zk_host  | zookeeper服务地址 | -      |
| zk_packets_received                | ZooKeeper接收的数据包数量     | zk_host  | zookeeper服务地址 | -      |
| zk_packets_sent                    | ZooKeeper发送的数据包数量     | zk_host  | zookeeper服务地址 | -      |
| zk_outstanding_requests            | ZooKeeper待处理的请求数量     | zk_host  | zookeeper服务地址 | -      |
| zk_approximate_data_size           | ZooKeeper数据大小         | zk_host  | zookeeper服务地址 | bytes  |


### 版本日志

#### weops_zookeeper_exporter 2.1.13

- weops调整

添加“小嘉”微信即可获取Zookeeper监控指标最佳实践礼包，其他更多问题欢迎咨询

<img src="https://wedoc.canway.net/imgs/img/小嘉.jpg" width="50%" height="50%">
