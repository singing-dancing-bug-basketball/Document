# /teacher/


## /teacher/login/
### post: 提交登录信息
* 传入数据格式
```
{
    "id": <教师 ID>,
    
}
```
* 返回数据格式
```
老师
    teacher/login
                {
                    user_name
                    password
                }
                {
                    测验
                }
            /question
                post method 
                {
                    题目
                    选项
                    答案
                }
                {
                    题目ID
                }
                delete method
                {
                    题目ID
                }
                200
                get method
                {
                   题目ID
                   题目
                   选项
                   答案 
                }
                put method
                {
                    题目ID
                    题目
                    选项
                    答案
                }
            /试卷
                post method
                {
                    试卷名字
                    {
                        题目ID:题目对应分数
                    }   
                }
                {
                    试卷ID
                    试卷名字
                }
                delete
                {
                    试卷ID
                }
                200
                get
                {
                    {试卷ID:试卷名字}
                }
                get/试卷ID
                {
                    试卷ID
                    试卷名字
                    {
                        题目ID{
                            题目内容:
                            选项:[]
                            正确答案:
                        }
                        
                    }
                }
                put
                {
                    试卷ID
                    试卷名字
                    {
                        题目ID:题目对应分数
                    }   
                }
    测验

```


            