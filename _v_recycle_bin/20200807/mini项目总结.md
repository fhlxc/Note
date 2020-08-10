# mini项目总结
### 1. 性能测试
- 框架层次结构
    - function：功能层，抽取相关页面可复用操作
    - object：页面元素定义层
    - case：测试用例层，组织function，实现相关操作，需要继承TestSuite
    - tools：定位元素的方法
    - run.sh：shell脚本运行整个项目
- 相关API
    - Config：用于配置TestCase的需要收集的数据项，可在suite或者case中的getConfig()配置，TestCase会覆盖TestSuite
    - TestSuite：测试集父类，记录App的基本信息，与App唯一对应
    - Explorer：工具控制类
    - Operator：常用UI操作
### 2. ui自动化测试
- 框架层次结构
    - bean：页面中的元素
    - case：编写的测试用例，断言
    - page：封装页面的操作
    - main.py：执行测试方法
### 3. 接口自动化测试
- 框架层次结构
    - cases：测试用例的集合
    - data：接口传递的参数，json文件
    - dataprovider：数据读取操作
    - model：定义调用的原型
    - util：基本的操作工具
    - main.py：调用测试case，执行测试用例