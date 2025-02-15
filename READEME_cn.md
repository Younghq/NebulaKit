### NebulaKit 星云Kit
构建这个项目的初衷是将自己的技术汇总，学习到好的库，借鉴其设计模式与数据结构，重新优化成好用好懂的库。

#### 一、分支规范
##### 1.主要分支
+ main分支：稳定版本分支，由develop合并至此。
+ develop分支：日常开发主分支，所有新功能合并至此。
##### 2.辅助分支
+ feature/模块描述:用于开发新模块，从develop创建分支，合并到develop后删除分支。
+ hotfix/问题描述:用于修复提交的BUG，从main创建分支，修复后合并到develop和main后删除分支。
+ docs/修改内容:从develop创建分支，合并到develop后删除。
#### 二、提交信息规范
##### 1.结构化格式
类型：
+ feat:新功能
+ fix：修复bug
+ docs:文档变更
+ refactor：代码重构

示范：
``` plaintext
<类型>(<范围>): <主题>          # 标题行（必填）
<空行>
<详细描述>                     # 说明改动背景、方案和影响（可选）
<空行>
<关联标记>                     # 例如 Closes #123, Refs #45（可选）
```

#### 整套流程演示
场景：开发网络请求工具
``` bash
# 1. 创建分支
git checkout develop
git checkout -b feature/http-client

# 2. 开发代码...
git add .
git commit -m "feat: 实现基础GET请求"

# 3. 合并到 develop
git checkout develop
git merge --no-ff feature/http-client
git branch -d feature/http-client

# 4. 测试稳定后，通过PR将 develop 合并到 main（在GitHub页面操作）
```

#### 三、项目规范

##### 1.命名规范
+ 类型名（类/结构体/枚举）：大驼峰
+ 函数名/方法名：使用下划线命名，强调动作
+ 变量名：使用下划线命名，易区分
+ 宏/常量：使用大写下划线命名

##### 2.代码偏好
+ 智能指针替代常规指针
+ 使用#pragma once替代#ifndef
+ 使用constexpr替代#define
+ 禁止引用全局命名空间
##### 3.文件规范
+ 文件结构
```plaintext
NebulaKit/  
├── assets                 # 存放静态文件
├── src/  
│   └── net_kit/           # 模块目录  
│       ├── tcp_server.hpp # 头文件
│       └── tcp_server.cpp # 实现文件  
└── tests/  
    └── test_math.cpp      # 测试与源码同名+test_前缀  
```
##### 4.注释规范
1. 函数注释（Doxygen精简版）

 ```cpp
/// 计算数组平均值（无Doxygen冗余标签）  
/// - 空数组返回0.0  
/// - 时间复杂度：O(n)  
double average(const std::vector<double>& data);  
```
2. 代码行注释（三不原则）

+   不写：描述代码本身（代码应自解释）
+   要写：解释 Why（如算法选择原因）

``` cpp
// 用快速排序替代归并排序：实测数据量<1w时快15%  
std::sort(data.begin(), data.end());  
```