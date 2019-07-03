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
* 传入数据格式
```
{
    "question_id": <题目ID>
}
```
* 返回数据格式
```
{
    "stem": <题干>,
    "options": [
        {
            "selection_id": <选项ID>,
            "content": <选项内容>
        }
    ],
    "answer": <答案选项的ID>
}
```
### post:添加新的问题
* 传入数据格式
```
{
    "stem": <题干>,
    "options": [<string 选项内容>],
    "answer": <integer range from 1 to 4>
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
    "options": [
        {
            "selection_id": <选项ID>,
            "content": <选项内容>
        }
    ],
    "answer": <选项ID>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
### /teacher/question/list
#### get:返回问题列表
PS: 
如果"page"缺失,默认返回第一页的内容(20个)
如果指定的"page">最大页数,则返回最后一页的内容
* 传入数据格式
```
{
    "page": <integer range from 1 to infinite>
}
```
* 返回数据格式
```
{
    "total_page": <integer range from 1 to infinite>,
    "questions": [
        {
            "question_id": <题目ID>,
            "stem": <题干>,
            "options": [
                {
                    "selection_id": <选项ID>,
                    "content": <选项内容>
                }
            ],
            "answer": <选项ID>
        }
    ]
}
```
## /teacher/test_paper/
### get:获取问题
* 传入数据格式
```
{
    "test_paper": <试卷ID>
}
```
* 返回数据格式
```
{
    questions:[
        {
            "question_id": <question_ID>,
            "stem": <题干>,
            "options": [
                {
                    "selection_id": <选项ID>,
                    "content": <选项内容>
                }
            ],
            "answer": <选项ID>,
            "score": <score is an integer range from 0 to 100>
        }
    ]
}
```
### post:添加新的试卷
* 传入数据格式
```
{
    "title": <试卷名称>,
    questions:[
        "question_id": <question_ID>,
        "score": <score is an integer range from 0 to 100>
    ]
}
```
* 返回数据格式
```
{
    "test_paper_id": <试卷ID>
}
```
### delete:删除试卷
* 传入数据格式
```
{
    "test_paper_id": <试卷的ID>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
### put:修改试卷
PS:
放在"questions"中的题目: 
如果传入的题目是原本试卷已经存在的,则覆盖已有题目的分数
如果传入的题目是原本试卷不存在的,则向试卷添加此题目
放在"delete_questions"中的题目:
从试卷中删除对应的题目
* 传入数据格式
```
{
    "test_paper_id": <试卷的ID>,
    "questions" :[
        "question_id": <question_ID>,
        "score": <score is an integer range from 0 to 100>
    ],
    "delete_questions": [
        "question_id": <question_ID>
    ]
}
```
* 返回数据格式
```
{
    "status": 200
}
```
### /teacher/test_paper/list
#### get:获取问题列表
PS: 
如果"page"缺失,默认返回第一页的内容(20个)
如果指定的"page">最大页数,则返回最后一页的内容
* 传入数据格式
```
{
    "page": <integer range from 1 to infinite>
}
```
* 返回数据格式
```
{
    "total_page": <integer range from 1 to infinite>,
    "test_papers": [
        {
            "test_paper_id": <试卷ID>,
            "title": <试卷名称>
        }
    ]
    "status": 200
}
```

            