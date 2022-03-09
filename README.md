# Sec Group FE
安全组 HTTP API 服务

## 1. API 概览

共 12 个 API。
安全组 API 4 个，安全组规则 API 3 个，安全组与资源绑定关系 API 5 个。

```
# 安全组 API
CreateSecGroup
DeleteSecGroup
UpdateSecGroup
DescribeSecGroup

# 安全组规则 API
CreateSecGroupRule
UpdateSecGroupRule
DeleteSecGroupRule

# 安全组与资源绑定关系 API
AssociateSecGroup
DisassociateSecGroup
DescribeSecGroupAssociation
DescribeSecGroupResource
DescribeResourceSecGroup
```

## 2. API 定义

- 服务地址：API 网关地址
- API 路径：/

- **公共请求参数**

| 名称   | 类型   | 是否必填 | 描述          |
| - | - | - | - |
| Action | string | 是 | 接口名称。示例：“DescribeSecGroup”
| Backend | string | 是 | 服务名称，“SecGroup”
| az_group | int | 是 | 地域 ID，示例：1000001，表示北京 2
| organization_id | int | 是 | 用户 ID
| top_organization_id | int | 是 | 公司 ID
| request_uuid | string | 否 | 请求 ID

如果请求来自公共服务网关，则 az_group, organization_id, top_organization_id 参数信息由网关根据用户认证信息解析填写，无需用户填写；如果请求来自内部网关，则需要填写。

- **公共返回值**

| 名称 | 类型 | 描述 |
| - | - | - |
| RetCode | int | 返回错误码。0 表示成功，其他表示错误 |
| Message | string | 错误信息。RetCode 非 0 时，返回错误信息 |

### 2.1 安全组 API

#### CreateSecGroup

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| VPCId  | string | 是 | VPC ID |
| SecGroupRecommendation | string | 否 | 安全组推荐模版，可选填：“web”, "noweb" |
| Name | string | 否 | 安全组名称，Name/Tag/Remark 不能都为空
| Tag | string | 否 | 安全组标记
| Remark | string | 否 | 安全组备注

- 应答参数

| 名称 | 类型 | 描述
| - | - | -
| SecGroupID | string | 创建的安全组资源 ID

---
#### DeleteSecGroup

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| VPCId  | string | 是 | VPC ID |
| SecGroupId | string 数组 | 是 | 安全组资源 ID 数组

- 应答参数

参考公共返回值

---
#### UpdateSecGroup

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| SecGroupId | string 数组 | 是 | 安全组资源 ID 数组
| Name | string | 否 | 安全组名称，Name/Tag/Remark 不能都为空
| Tag | string | 否 | 安全组标记
| Remark | string | 否 | 安全组备注

- 应答参数

参考公共返回值

---
#### DescribeSecGroup

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| VPCId | string | 否 | VPC ID
| SecGroupId | string 数组 | 否 | 安全组资源 ID 数组，传入则 Offset/Limit/BusinessId 失效
| BusinessId | string | 否 | 业务 ID，用于从资源系统过滤
| Offset | int | 否 | 偏移量，分页查询使用
| Limit | int | 否 | 返回数量限制，分页查询使用

- 应答参数

| 名称 | 类型 | 描述
| - | - | -
| TotalCount | int | 安全组总数量
| DataSet | SecGroupInfo 数组 | 安全组信息

SecGroupInfo 信息字段如下：
| 名称 | 类型 | 描述
| - | - | -
| SecGroupId | string | 安全组资源 ID
| VPCId | string | VPC ID
| Account | int | 用户 ID
| Type | string | 安全组类型
| CreateTime | int | 安全组创建的时间戳
| Name | string | 安全组名称
| Tag | string | 安全组标记
| Remark | string | 安全组备注
| Rule | SecGroupRuleInfo 数组 | 安全组规则信息

SecGroupRuleInfo 信息字段如下：
| 名称 | 类型 | 描述
| - | - | -
| RuleId | string | 安全组规则 ID
| IPVersion | string | IP 版本
| Direction | string | 出入向，"Ingress", "Egress"
| ProtocolType | string | 传输层协议，如 "TCP"
| IPRange | string | IP 地址或网段，逗号分割
| DstPort | string | 端口，如 "80,443"
| Priority | int | 规则优先级
| RuleAction | string | 规则匹配行为，"Drop", "Accept"
| Remark | string | 备注

示例
```json
# 请求
{
    "Action": "DescribeSecGroup",
    "Backend": "SecGroup",
    "az_group": 1000001,
    "organization_id": 63782908,
    "top_organization_id": 50120017,
    "Offset": 0,
    "Limit": 10,
    "SecGroupId": [
        "secgroup-q5r3csmv"
    ],
    "request_uuid": "testlzy-secgroup-efg"
}

# 应答
{
    "Action": "DescribeSecGroupResponse",
    "RetCode": 0,
    "Message": "",
    "TotalCount": 1,
    "DataSet": [
        {
            "SecGroupId": "secgroup-q5r3csmv",
            "VPCId": "uvnet-snqyoyjp",
            "Account": 63782908,
            "Type": "user defined",
            "CreateTime": 1625636319,
            "Rule": [
                {
                    "RuleId": "5fad22b3-880d-4f49-94ad-3ec237926ff4",
                    "IPVersion": "IPv4",
                    "Direction": "Ingress",
                    "ProtocolType": "TCP",
                    "IPRange": "127.0.0.1,10.8.0.0/16",
                    "DstPort": "80,443",
                    "Priority": 0,
                    "RuleAction": "Drop",
                    "Remark": "http,https"
                },
                {
                    "RuleId": "b47ec87c-275b-44c7-a464-b6e5379faa4e",
                    "IPVersion": "IPv4",
                    "Direction": "Ingress",
                    "ProtocolType": "TCP",
                    "IPRange": "10.8.0.0/16",
                    "DstPort": "80",
                    "Priority": 0,
                    "RuleAction": "Drop",
                    "Remark": "http"
                },
                {
                    "RuleId": "4fe4c881-6509-4e53-ba67-8d90ca952931",
                    "IPVersion": "IPv4",
                    "Direction": "Ingress",
                    "ProtocolType": "TCP",
                    "IPRange": "secgroup-q5r3csmv",
                    "DstPort": "99",
                    "Priority": 66,
                    "RuleAction": "Drop",
                    "Remark": ""
                },
                {
                    "RuleId": "4551e64d-971d-4ff4-82ff-7f048c624dbb",
                    "IPVersion": "IPv4",
                    "Direction": "Ingress",
                    "ProtocolType": "ALL",
                    "IPRange": "secgroup-q5r3csmv",
                    "DstPort": "ALL",
                    "Priority": 1,
                    "RuleAction": "Accept",
                    "Remark": ""
                }
            ],
            "Name": "test-lzy-name",
            "Tag": "test-lzy-tag",
            "Remark": "test-lzy-remark"
        }
    ]
}
```

### 2.2 安全组规则 API

#### CreateSecGroupRule

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| VPCId | string | 是 | VPC ID
| SecGroupId | string | 是 | 安全组资源 ID
| Rule | SecGroupRuleInfo 数组 | 是 | 安全组规则，其中 RuleId 不需要填写

- 应答参数

| 名称 | 类型 | 描述
| - | - | -
| RuleId | string 数组 | 创建的安全组规则 ID

---

#### UpdateSecGroupRule

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| VPCId | string | 是 | VPC ID
| SecGroupId | string | 是 | 安全组资源 ID
| Rule | SecGroupRuleInfo 数组 | 是 | 安全组规则，其中 RuleId 需要填写

- 应答参数

参考公共返回值

---

#### DeleteSecGroupRule

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| VPCId | string | 是 | VPC ID
| SecGroupId | string | 是 | 安全组资源 ID
| RuleId | string 数组 | 是 | 安全组规则 ID

- 应答参数

参考公共返回值

### 2.3 安全组绑定关系 API

#### AssociateSecGroup

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| VPCId | string | 是 | VPC ID
| ResourceId | string 数组 | 是 | （主机/虚拟网卡等）资源 ID
| PrioritySecGroup | PrioritySecGroup 数组 | 是 | 安全组 ID 和绑定优先级

PrioritySecGroup 信息字段如下：
| 名称 | 类型 | 描述
| - | - | -
| SecGroupId | string | 安全组资源 ID
| Priority | int | 绑定优先级

备注：资源和安全组不支持同时传入多个。更新绑定优先级也使用该接口。

- 应答参数

参考公共返回值

---

#### DisassociateSecGroup

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| VPCId | string | 是 | VPC ID
| ResourceId | string 数组 | 是 | （主机/虚拟网卡等）资源 ID
| SecGroupId | string 数组 | 是 | 安全组 ID

备注：资源和安全组不支持同时传入多个。

- 应答参数

参考公共返回值

---

#### DescribeSecGroupAssociation

查询安全组绑定的资源（只返回资源 ID 和类型信息）

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| SecGroupId | string 数组 | 是 | 安全组 ID

- 应答参数

| 名称 | 类型 | 描述
| - | - | -
| DataSet | SecGroupAssociation 数组  | 安全组绑定的资源信息

SecGroupAssociation 信息字段如下：
| 名称 | 类型 | 描述
| - | - | -
| SecGroupId | string  | 安全组资源 ID
| ObjectList | ObjectInfo 数组 | 资源信息

ObjectInfo 信息字段如下：
| 名称 | 类型 | 描述
| - | - | -
| ObjectId | string | 资源 ID
| ObjectType | int | 资源类型

示例
```json
# 请求
{
    "Action": "DescribeSecGroupAssociation",
    "Backend": "SecGroup",
    "SecGroupId": [
        "secgroup-svpv1n5j"
    ],
    "az_group": 1000001,
    "organization_id": 63782908,
    "top_organization_id": 50120017,
    "request_uuid": "testlzy-secgroup"
}

# 应答
{
    "Action": "DescribeSecGroupAssociationResponse",
    "RetCode": 0,
    "Message": "",
    "DataSet": [
        {
            "SecGroupId": "secgroup-svpv1n5j",
            "ObjectList": [
     {
         "ObjectId": "uhost-vweq4cs5",
         "ObjectType": 1
     }
            ]
        }
    ]
}
```

---

#### DescribeSecGroupResource

查询单个安全组绑定的资源（返回资源详细信息），支持分页查询（对绑定的资源分页获取）。

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| SecGroupId | string | 是 | 安全组 ID
| Offset | int | 否 | 偏移量，分页查询使用
| Limit | int | 否 | 返回数量限制，分页查询使用

- 应答参数

| 名称 | 类型 | 描述
| - | - | -
| TotalCount | int | 安全组绑定资源的总数量
| DataSet | SecGroupResourceInfo 数组 | 安全组绑定的资源详细信息

SecGroupResourceInfo 信息字段如下：
| 名称 | 类型 | 描述
| - | - | -
| Zone | int | 资源可用区
| Name | string | 资源名称
| Tag | string | 资源标签
| ResourceId | string | 资源 ID
| ResourceType | string | 资源类型
| PrivateIp | string | 资源内网 IP
| SubResourceName | string | 子资源名称，子资源可以是主机的主网卡
| SubResourceId | string | 子资源 ID
| SubResourceType | string | 子资源类型

示例
```json
# 请求
{
    "Action": "DescribeSecGroupResource",
    "Backend": "SecGroup",
    "az_group": 1000001,
    "organization_id": 63782908,
    "top_organization_id": 50120017,
    "SecGroupId": "secgroup-svpv1n5j",
    "Offset": 0,
    "Limit": 2,
    "request_uuid": "testfts-secgroup"
}

# 应答
{
    "Action": "DescribeSecGroupResourceResponse",
    "RetCode": 0,
    "Message": "",
    "DataSet": [
        {
            "Zone": 4001,
            "Name": "UHost",
            "Tag": "",
            "ResourceId": "uhost-vweq4cs5",
            "ResourceType": "uhost",
            "PrivateIp": "10.9.132.184",
            "SubResourceName": "",
            "SubResourceId": "",
            "SubResourceType": ""
        }
    ],
    "TotalCount": 1
}
```

---
#### DescribeResourceSecGroup

查询资源绑定的安全组。

- 请求参数

| 名称 | 类型 | 是否必填 | 描述 |
| - | - | - | - |
| ResourceType | string | 是 | 资源类型
| ResourceId | string 数组 | 否 | 资源 ID 数组，如果指定则不分页；否则分页获取该账号下的指定类型的资源
| Offset | int | 否 | 偏移量，分页查询使用
| Limit | int | 否 | 返回数量限制，分页查询使用

- 应答参数

| 名称 | 类型 | 描述
| - | - | -
| TotalCount | int | 资源的总数量
| DataSet | ResourceSecgroupInfo 数组 | 资源绑定的安全组信息

ResourceSecgroupInfo 信息字段如下：
| 名称 | 类型 | 描述
| - | - | -
| ResourceId | string | 资源 ID
| Count | int | 该资源绑定的安全组数量
| SecGroupInfo | BindingSecGroupInfo 数组

BindingSecGroupInfo 信息字段如下：
| 名称 | 类型 | 描述
| - | - | -
| SecGroupId | string | 安全组 ID
| Name | string | 安全组名称
| Priority | int | 该资源与该安全组绑定的优先级

示例
```json
# 请求
{
    "Action": "QueryResourceSecgroup",
    "Backend": "SecGroup",
    "az_group": 1000001,
    "organization_id": 63782908,
    "top_organization_id": 50120017,
    "ResourceType": "uhost",
    "ResourceId": [
        "uhost-vweq4cs5"
    ],
    "Offset": 0,
    "Limit": 10,
    "request_uuid": "testfts-secgroup"
}

# 应答
{
    "Action": "QueryResourceSecgroupResponse",
    "RetCode": 0,
    "Message": "",
    "DataSet": [
        {
            "ResourceId": "uhost-vweq4cs5",
            "Count": 5,
            "SecGroupInfo": [
     {
         "SecGroupId": "secgroup-3rnhotcv",
         "Name": "test-lzy-web",
         "Priority": 1
     },
     {
         "SecGroupId": "secgroup-jvngrgk3",
         "Name": "test-lzy-name",
         "Priority": 4
     },
     {
         "SecGroupId": "secgroup-q5r3csmv",
         "Name": "test-lzy-name",
         "Priority": 2
     },
     {
         "SecGroupId": "secgroup-svpv1n5j",
         "Name": "test-lzy-name-3",
         "Priority": 3
     },
     {
         "SecGroupId": "secgroup-yf2ow0ml",
         "Name": "test-lzy-web",
         "Priority": 5
     }
            ]
        }
    ],
    "TotalCount": 1
}
```
