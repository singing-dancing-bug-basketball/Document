# /teacher/


## /teacher/login/
### post:提交登录信息
* 传入数据格式
```
{
    "id": <teacher ID>,
    "password": <password>,
}
```
* 返回数据格式
```
{
    test_id:test_name
}
```
## /teacher/question/
### get:获取问题
### post:添加新的问题
* 传入数据格式
```
{
    "stem": <题干>,
    "options": [<选项内容>],
    "answer": <选项内容>
}
```
* 返回数据格式
```
{
    "question_id": <题目ID>
}
```
### delete:删除问题
* 传入数据格式
```
{
    "question_id": <题目ID>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
### put:修改问题
* 传入数据格式
```
{
    "question_id": <题目ID>
    "stem": <题干>,
    "options": [<选项内容>],
    "answer": <选项内容>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
## /teacher/test_paper/
```
老师
    teacher
            /question
                get method
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


            