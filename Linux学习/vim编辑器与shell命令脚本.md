# vim编辑器与shell命令脚本
### 1. vim编辑器
- vim中常用的命令
> 命令 | 作用
> --- | ---
> dd | 删除光标所在整行
> 5dd | 删除从光标处开始的5行
> yy | 复制光标所在的行
> 5yy | 复制从光标处开始的5行
> n | 显示搜索命令定位到的下一个字符串
> N | 显示搜索命令定位到的上一个字符串
> u | 撤销上一步操作
> p | 将之前删除dd或复制yy过的数据粘贴到光标后面
- 末行模式中可用的命令
> 命令 | 作用
> -- | --
> :w | 退出
> :q | 推出
> :q! | 强制退出
> :wq! | 强制保存退出
> :set nu | 显示行号
> :set nonu | 不显示行号
> :命令 | 执行该命令
> :整数 | 跳转到该行
> :s/one/two | 将当前光标所在行的第一个one替换成two
> :s/one/two/g | 将当前光标所在行的所有one替换成two
> :%s/one/two/g | 将全文中所有的one替换成two
> ?字符串 | 在文中从下至上搜索该字符串
> /字符串 | 在文中从上至下搜索该字符串
### 2. Shell脚本
- 文件测试参数
>运算符 | 作用
>-- | --
>-d | 测试文件是否为目录
>-e | 测试文件是否存在
>-f | 测试是否为一般文件
>-r | 测试当前用户是否有权限读取
>-w | 测试当前用户是否有权限写入
>-x | 测试当前用户是否有权限执行
- 整数比较运算符
> 运算符 | 作用
> -- | --
> -eq | 是否等于
> -ne | 是否不等于
> -gt | 是否大于
> -lt | 是否小于
> -le | 是否小于等于
> -ge | 是否大于等于
- 字符串比较运算符
> 运算符 | 作用
> -- | --
> = | 比较字符串内容是否相同
> != | 比较字符串内容是否不同
> -z | 判断字符串内容是否为空
- 流程控制语句
    - if条件测试语句
        ```shell
        if # 条件测试操作
        the
        # 满足条件后的语句
        fi
        ```
        ```shell
        if # 条件测试操作
        then
        # 满足条件之后的语句
        else
        # 不满足条件要做的语句
        fi
        ```
        ```shell
        if # 条件测试操作
        then
        # 满足条件之后的语句
        elif # 条件测试操作
        then
        # 满足条件之后的语句
        else
        # 不满足上述条件的语句
        fi
        ```
    - for条件循环语句
        ```shell
        for 变量名 in 取值列表
        do
        # 循环要做的语句
        done
        ```
        ```shell
        # 以下是for循环的例子,用于从文件中创建用户
        for uname in `cat user.txt`
        do
        read -p "enter ${uname}'s password: " pwd
        id $uname &> /dev/null
        if [ $? -eq 0 ]
        then
        echo "Already exists"
        else
        useradd $uname &> /dev/null
        echo "$pwd" | password --stdin $user &> /dev/null
        if [ $? -eq 0 ]
        then
        echo "$uname, create success"
        else
        echo "$uname, create failure"
        fi
        fi
        done
        ```
    - while条件循环语句
        ```shell
        while # 条件测试语句
        do
        # 满足条件执行的语句
        done
        ```
        ```shell
        # 例子输出10个数
        number=0
        while [ $number -lt 10 ]
        do
        echo $number
        let number++
        done
        ```
    - case条件测试语句
        ```shell
        case 变量值 in
        模式1)
        # 要做的命令
        ;;
        模式2)
        # 要做的命令
        ;;
        ......
        *)
        # 以上都不是要做的命令
        esac
        ```
        ```shell
        # 使用case的例子，判断用户输入的类型
        read -p "请输入字符，按enter确认：" key
        case "$key" in
        [a-zA-Z]*)
        echo "你输入的是字符"
        ;;
        [0-9]*)
        echo "你输入的是数字"
        ;;
        *)
        echo "你输入的是非字母和数字"
        esac
        ```