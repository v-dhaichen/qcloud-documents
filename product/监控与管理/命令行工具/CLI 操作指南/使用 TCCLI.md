

## 操作场景

命令行工具集成了腾讯云所有支持云 API 的产品，可以在命令行下完成对腾讯云产品的配置和管理。包括使用 TCCLI 创建云服务器、操作云服务器、通过 TCCLI 创建 CBS 盘、查看 CBS 盘使用情况、通过 TCCLI 创建 VPC 网络、往 VPC 网络中添加资源等，所有在控制台页面能完成的操作，均能在命令行工具上执行命令实现。

* 通过`tccli cvm DescribeInstances`命令查看当前账号有哪些云服务器。
* 通过`tccli cbs DescribeDisks`命令查看有 CBS 盘列表。

## 操作示例

>! demo 中非简单类型的参数必须为标准 JSON 格式。

1. 以创建一台 CVM 为例，执行以下命令。
```bash
tccli cvm RunInstances
--InstanceChargeType POSTPAID_BY_HOUR
--InstanceChargePrepaid '{"Period":1,"RenewFlag":"DISABLE_NOTIFY_AND_MANUAL_RENEW"}'
--Placement '{"Zone":"ap-guangzhou-2"}'
--InstanceType S1.SMALL1
--ImageId img-8toqc6s3
--SystemDisk '{"DiskType":"CLOUD_BASIC", "DiskSize":50}'
--InternetAccessible '{"InternetChargeType":"TRAFFIC_POSTPAID_BY_HOUR","InternetMaxBandwidthOut":10,"PublicIpAssigned":true}' 
--InstanceCount 1
--InstanceName TCCLI-TEST
--LoginSettings '{"Password":"TCCLI"}'
--SecurityGroupIds '["sg-0rszg2vb"]'
--HostName TCCLI-HOST-NAME1
```
2. 如果调用接口参数是复杂类型时，需加 `--cli-unfold-argument`（可补全）参数，进行参数补全，使用复杂类型点(.)展开的方式调用，降低输入难度。（`3.0.273.1` 版本开始支持）
```bash
$ tccli cvm RunInstances 
--cli-unfold-argument
--Placement.Zone ap-guangzhou-3
--ImageId img-8toqc6s3
--DryRun True
```
3. 如果您不清楚接口入参，加`--generate-cli-skeleton`（可补全）参数可输出一份 JSON 格式入参骨架。（`3.0.273.1` 版本开始支持）
```bash
# 可将 json 格式入参骨架直接输入到 json 文件中
# $ tccli cvm DescribeInstances --generate-cli-skeleton > /home/test.json
$ tccli cvm DescribeInstances --generate-cli-skeleton
{
    "Limit": "Integer", 
    "Filters": [
        {
            "Values": [
                "String"
            ], 
            "Name": "String"
        }
    ], 
    "InstanceIds": [
        "String"
    ], 
    "Offset": "Integer"
}
```
4. 如果接口入参比较多，加`--cli-input-json`（可补全）参数支持 JSON 文件输入（后面需要加上`file://+文件路径`）。（`3.0.250.2`版本开始支持）。
```bash
 $ tccli cvm DescribeInstances --cli-input-json file:///home/test.json
```


## 说明
更多功能，您可以通过`tccli help`查看支持的产品，通过`tccli cvm help`（以 CVM 举例）查看产品支持的接口。通过`tccli cbs DescribeDisks help`（以 CBS 产品的 DescribeDisks 接口为例） 查看接口支持的参数。
