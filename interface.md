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
    "status": 200
}
```
## /teacher/question/
### get:获取某个问题
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
    "selections": [
        <选项内容 string>
    ],
    "answer": <integer range from 1 to 4 or more>
}
```
### post:添加新的问题
* 传入数据格式
```
{
    "stem": <题干>,
    "selections": [<string 选项内容>],
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
PS:
存在的项覆盖,不存在的项不变,id不可缺
* 传入数据格式
```
{
    "question_id": <题目ID>
    "stem": <题干>,
    "selections": {
        "id": <string 选项内容> // id range from 1 to 4 or more, means A,B,C,D and etc.
    },
    "answer": <integer range from 1 to 4>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
### /teacher/question/list/
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
    page: <integer range from 1 to infinite 当前页数>,
    "total_page": <integer range from 1 to infinite>,
    "questions": [
        {
            "question_id": <题目ID>,
            "stem": <题干>,
            "selections": [<string 选项内容>],
            "answer": <integer range from 1 to 4>
        }
    ]
}
```
## /teacher/test_paper/
### get:获取某张试卷
* 传入数据格式
```
{
    "test_paper": <试卷ID>
}
```
* 返回数据格式
```
{   
    "title": <试卷名称>,
    "duration": <integer 持续时间 range from 0 to infinite>,
    "questions":[
        {
            "question_id": <question_ID>,
            "stem": <题干>,
            "selections": [<string 选项内容>],
            "answer": <integer range from 1 to 4>,
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
    "duration": <integer 持续时间 range from 0 to infinite>,
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
+ 放在"questions"中的题目: 
如果传入的题目是原本试卷已经存在的,则覆盖已有题目的分数
如果传入的题目是原本试卷不存在的,则向试卷添加此题目
+ 放在"delete_questions"中的题目:
从试卷中删除对应的题目
+ 存在的项覆盖,不存在的项不变,id不可缺


* 传入数据格式
```
{
    "test_paper_id": <试卷的ID>,
    "title": <string 试卷名称>,
    "duration": <integer 持续时间 range from 0 to infinite>,
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
### /teacher/test_paper/list/
#### get:获取试卷列表
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
    page: <integer range from 1 to infinite 当前页数>,
    "total_page": <integer range from 1 to infinite>,
    "test_papers": [
        {
            "test_paper_id": <试卷ID>,
            "title": <试卷名称>,
            "duration": <integer 持续时间 range from 0 to infinite>
        }
    ]
    "status": 200
}
```
## /teacher/test/
### get:获取某个测试题
* 传入数据格式
```
{
    "test_id": <测试ID>
}
```
* 返回数据格式
```
{
    "test_title": <string 测试名称>,
    "test_paper_time": <string 试卷名称>,
    "duration": <integer 持续时间 range from 0 to infinite>,
    "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
    "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>,
    "test_paper_id": <试卷ID>
}
```
### post:添加新的测试
* 传入数据格式
```
{
    "test_paper_id": <需要用到的试卷ID>,
    "title": <string 测试名称>,
    "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
    "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>
}
``` 
* 返回数据格式
```
{
    "test_id": <测试的ID>,
    "status": 200
}
```
### delete:删除某个测试
* 传入数据格式
```
{
    "test_id": <测试ID>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
### put:修改某次测试
PS: 存在的项覆盖,不存在的项不变,id不可缺
* 传入数据格式
```
{
    "test_id": <需要更改的测试ID>,
    "test_paper_id": <需要用到的试卷ID>,
    "title": <string 测试名称>,
    "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
    "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
### /teacher/test/list/
#### get:获取测试列表
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
    page: <integer range from 1 to infinite 当前页数>,
    "total_page": <integer range from 1 to infinite>,
    "tests": [
        {
            "test_id": <测试ID>,
            "title": <测试名称>
        }
    ]
}
```

## /teacher/record/
### get:获取某次测试结果

## /teacher/record/list/
### get:获取测试结果列表

## /teacher/student/
### get:获取某个学生的信息
### post:添加学生
### put:修改学生信息
### delete:删除学生

# /student/

## /student/login/
### post:提交登录信息
* 传入数据格式
```
{
    "id": <student ID>,
    "password": <password>,
}
```
* 返回数据格式
```
{
    "status": 200
}
```
## /student/test/
### get:获取某一次测试
* 传入数据格式
```
{
    "id": <student ID>,
    "test_id": <测试ID>
}
```
* 返回数据格式
```
{
    "test_title": <string 测试名称>,
    "duration": <integer 持续时间 range from 0 to infinite>,
    "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
    "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>,
    "questions":[
        {
            "question_id": <question_ID>,
            "stem": <题干>,
            "selections": [<string 选项内容>],
            "answer": <integer range from 1 to 4>,
            "score": <score is an integer range from 0 to 100>
        }
    ]
}
```
## /student/test/list/
### get:获取学生的测试列表
* 传入数据格式
```
{
    "id": <student ID>
}
```
* 返回数据格式
```
{
    "tests": [
        {
            "test_id": <测试ID>,
            "title": <测试名称>,
            "duration": <integer 持续时间 range from 0 to infinite>,
            "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
            "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>,
        }
    ]
}
```
## /student/record/
### get:获取某次测试结果
* 传入数据格式
```
{
    
}
```
* 返回数据格式
### post:学生提交测试结果

## /student/record/list/
### get:获取测试结果列表