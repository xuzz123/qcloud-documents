## 操作场景
云数据库 Redis [4.0标准版](https://cloud.tencent.com/document/product/239/36151) 和 [4.0集群版](https://cloud.tencent.com/document/product/239/18336) 提供更灵活的规格配置、更高的性能以及更完善的功能。如果您使用的 Redis 版本较低，为保证更好的云数据库服务体验，建议您升级至 Redis 4.0 版本。

云数据库 Redis 实例版本升级通过 [数据传输服务 DTS](https://cloud.tencent.com/document/product/571) 以热迁移的方式进行，保证升级过程中 Redis 实例业务不停服，能实时增量更新数据。

| 术语 | 说明 | 
|---------|---------|
| 源实例 | 版本升级的源实例 | 
| 目标实例 | 版本升级的目标实例 | 

#### 支持版本
<table>
    <tr>
    <td colspan=2 align=center>源实例版本</td>
    <td rowspan=2 align=cente>目标实例版本</td>
    </tr>
    <tr>
    <td>2.8标准版</td>
    <td>4.0标准版</td>
    </tr>
    <tr>
    <td>✓</td>
    <td>✓</td>
    <td>4.0标准版</td>
    </tr>
    <tr>
    <td>✓</td>
    <td>✓</td>
    <td>4.0集群版</td>
    </tr>
</table>

## 前提条件
- 需是正常运行状态下的 Redis 源实例。
- 购买的Redis 4.0标准版或Redis 4.0集群版实例。
>? 如果数据量小于12GB，且后续数据增长不超过60GB，QPS 不超过4W，建议选择 Redis 4.0 标准版，否则建议选择  Redis 4.0 集群版，Redis 4.0 集群版不支持事务命令（如果需要事务支持，请选择 Redis 4.0 标准版），您可根据业务实际情况进行选择。

## 操作步骤
1. 使用 DTS 从云数据库 Redis 源实例，迁移数据至 Redis 4.0 标准版或 Redis 4.0 集群版实例，请参见 [使用 DTS 进行迁移](https://cloud.tencent.com/document/product/239/31958#1.-.E6.96.B0.E5.BB.BA.E8.BF.81.E7.A7.BB.E4.BB.BB.E5.8A.A1)。
2. 数据同步完成，业务侧验证数据无误后，可根据业务 QPS 等指标选择时间断开 Redis 源实例连接，将连接切换到 Redis 目标实例，切换方法有两种可供选择：
 - 记录 Redis 源实例的旧 IP 地址并修改 IP 地址；修改 Redis 目标实例的网络信息和 Redis 源实例处于同一个 VPC 子网，并指定 Redis 目标实例的新 IP 地址为 Redis 源实例的旧 IP 地址，即可完成业务切换。
修改网络信息和 IP 地址的具体操作请参见 [配置网络](https://cloud.tencent.com/document/product/239/30910)。
 - 将代码中 Redis 源实例的 IP 更新为 Redis 目标实例的 IP 即可。
