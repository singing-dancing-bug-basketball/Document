# Directory
## /teacher/ API for browser
* [/teacher/login/](#/teacher/login/)
  * [post:提交登录信息](#login-post)
* [/teacher/question/](#/teacher/question/)
  * [get:获取某个问题](#question-get)
  * [post:添加新的问题](#question-post)
  * [delete:删除问题](#question-delete)
  * [put:修改问题](#question-put)
* [/teacher/question/list/](#/teacher/question/list/)
  * [get:获取问题列表](#question-list-get)
* [/teacher/test_paper/](#/teacher/test_paper/)
  * [get:获取某张试卷](#test_paper-get)
  * [post:添加新的试卷](#test_paper-post)
  * [delete:删除试卷](#test_paper-delete)
  * [put:修改试卷](#test_paper-put)
* [/teacher/test_paper/list/](#/teacher/test_paper/list/)
  * [get:获取试卷列表](#test_paper-list-get)
* [/teacher/test/](#/teacher/test/)
  * [get:获取某个测试题](#test-get)
  * [post:添加新的测试](#test-post)
  * [delete:删除某个测试](#test-delete)
  * [put:修改某次测试](#test-put)
* [/teacher/test/list/](#/teacher/test/list/)
  * [get:获取测试列表](#test-list-get)
* [/teacher/record/](#/teacher/record/)
  * [get:获取某次测试结果](#record-get)
* [/teacher/student/](#/teacher/student/)
  * [get:获取某个学生的信息](#student-get)
  * [post:添加学生](#student-post)
  * [put:修改学生信息](#student-put)
  * [delete:删除学生](#student-delete)
* [/teacher/student/list/](#/teacher/student/list/)
  * [get:获取学生的列表](#student-list-get)
## /student/ API for Android
* [/student/login/](#/student/login/)
  * [post:提交登录信息](#student-login)
* [/student/test/](#/student/test/)
  * [get:获取某一次测试](#student-test-get)
* [/student/test/list/](#/student/test/list/)
  * [get:获取学生的测试列表](#student-test-list-get)
* [/student/record/](#/student/record/)
  * [get:获取某次测试结果](#student-record-get)
  * [post:学生提交测试结果](#student-record-post)
* [/student/record/list/](#/student/record/list/)
  * [get:获取测试结果列表](#student-record-list-get)

# /teacher/ 
<h2 id="/teacher/login/">/teacher/login/</h2>
<h3 id="login-post">post:提交登录信息</h3>

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
<h2 id="/teacher/question/">/teacher/question/</h2>
<h3 id="question-get">get:获取某个问题</h3>

* 传入数据格式
```
<question_id(题目ID)>
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
<h3 id="question-post">post:添加新的问题</h3>

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
<h3 id="question-delete">delete:删除问题</h3>

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
<h3 id="question-put">put:修改问题</h3>

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
<h2 id="/teacher/question/list/">/teacher/question/list/</h2>
<h3 id="question-list-get">get:获取问题列表</h3>

PS: 
如果"page"缺失,默认返回第一页的内容(20个)
如果指定的"page">最大页数,则返回最后一页的内容
* 传入数据格式
```
<page, an integer range from 1 to infinite>
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
<h2 id="/teacher/test_paper/">/teacher/test_paper/</h2>
<h3 id="test_paper-get">get:获取某张试卷</h3>

* 传入数据格式
```
<test_paper(试卷ID)>
```
* 返回数据格式
```
{   
    "title": <试卷名称>,
    "duration": <integer 持续时间 range from 0 to infinite, unit: minute>,
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
<h3 id="test_paper-post">post:添加新的试卷</h3>

* 传入数据格式
```
{
    "title": <试卷名称>,
    "duration": <integer 持续时间 range from 0 to infinite, unit: minute>,
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
<h3 id="test_paper-delete">delete:删除试卷</h3>

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
<h3 id="test_paper-put">put:修改试卷</h3>

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
    "duration": <integer 持续时间 range from 0 to infinite, unit: minute>,
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
<h2 id="/teacher/test_paper/list/">/teacher/test_paper/list/</h2>
<h3 id="test_paper-list-get">get:获取试卷列表</h3>

PS: 
如果"page"缺失,默认返回第一页的内容(20个)
如果指定的"page">最大页数,则返回最后一页的内容
* 传入数据格式
```
<page, an integer range from 1 to infinite>
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
            "duration": <integer 持续时间 range from 0 to infinite, unit: minute>
        }
    ]
    "status": 200
}
```
<h2 id="/teacher/test/">/teacher/test/</h2>
<h3 id="test-get">get:获取某个测试题</h3>

* 传入数据格式
```
<test_id(测试ID)>
```
* 返回数据格式
```
{
    "test_title": <string 测试名称>,
    "test_paper_time": <string 试卷名称>,
    "duration": <integer 持续时间 range from 0 to infinite, unit: minute>,
    "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
    "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>,
    "test_paper_id": <试卷ID>
}
```
<h3 id="test-post">post:添加新的测试</h3>

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
<h3 id="test-delete">delete:删除某个测试</h3>

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
<h3 id="test-put">put:修改某次测试</h3>

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
<h2 id="/teacher/test/list/">/teacher/test/list/</h2>
<h3 id="test-list-get">get:获取测试列表</h3>

PS: 
如果"page"缺失,默认返回第一页的内容(20个)
如果指定的"page">最大页数,则返回最后一页的内容
* 传入数据格式
```
<page, an integer range from 1 to infinite>
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
<h2 id="/teacher/record/">/teacher/record/</h2>
<h3 id="record-get">get:获取某次测试结果</h3>

* 传入数据格式
```
<test_id(测试ID)>
```
* 返回数据格式
```
{
    "title": <测试名称>,
    "students_num": <integer 参加考试的学生人数>,
    "student_average": <float 平均分>,
    "students": [
        {
            "student_id": <student的ID>,
            "student_name": <学生姓名>,
            "score": <学生的最终成绩>
        }
    ]
}
```
<h2 id="/teacher/student/">/teacher/student/</h2>
<h3 id="student-get">get:获取某个学生的信息</h3>

* 传入数据格式
```
<student_id(学生ID)>
```
* 返回数据格式
```
{
    "student_id": <学生ID>,
    "name": <学生姓名>
}
```
<h3 id="student-post">post:添加学生</h3>

* 传入数据格式
```
{
    "student_id": <老师指定的学生学号>
    "name": <学生姓名>,
    "password": <密码>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
<h3 id="student-put">put:修改学生信息</h3>

PS: 存在的项覆盖,不存在的项不变,id不可缺
* 传入数据格式
```
{
    "student_id": <学生ID>,
    "name": <学生姓名>,
    "password": <密码>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
<h3 id="student-delete">delete:删除学生</h3>

* 传入数据格式
```
{
    "student_id": <学生ID>
}
```
* 返回数据格式
```
{
    "status": 200
}
```
<h2 id="/teacher/student/list/">/teacher/student/list/</h2>
<h3 id="student-list-get">get:获取学生的列表</h3>

PS: 
如果"page"缺失,默认返回第一页的内容(20个)
如果指定的"page">最大页数,则返回最后一页的内容
* 传入数据格式
```
<page, an integer range from 1 to infinite>
```
* 返回数据格式
```
{
    page: <integer range from 1 to infinite 当前页数>,
    "total_page": <integer range from 1 to infinite>,
    "students": [
        {
            "student_id": <学生ID>,
            "name": <学生名字>
        }
    ]
}
```
# /student/
<h2 id="/student/login/">/student/login/</h2>
<h3 id="student-login">post:提交登录信息</h3>

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
<h2 id="/student/test/">/student/test/</h2>
<h3 id="student-test-get">get:获取某一次测试</h3>

* 传入数据格式
```
<test_id(测试ID)>
```
* 返回数据格式
```
{
    "title": <string 测试名称>,
    "duration": <integer 持续时间 range from 0 to infinite, unit: minute>,
    "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
    "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>,
    "questions":[
        {
            "question_id": <question_ID>,
            "stem": <题干>,
            "selections": [<string 选项内容>],
            "score": <score is an integer range from 0 to 100>
        }
    ]
}
```
<h2 id="/student/test/list/">/student/test/list/</h2>
<h3 id="student-test-list-get">get:获取学生的测试列表</h3>

PS: 此API表示获取学生可以参加但还未参加的测试列表
* 传入数据格式
```
<student ID>
```
* 返回数据格式
```
{
    "tests": [
        {
            "test_id": <测试ID>,
            "title": <测试名称>,
            "total_score": <测试总分>,
            "num_questions": <总题数>,
            "duration": <integer 持续时间 range from 0 to infinite, unit: minute>,
            "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
            "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>
        }
    ]
}
```
<h2 id="/student/record/">/student/record/</h2>
<h3 id="student-record-get">get:获取某次测试结果</h3>

* 传入数据格式
```
/<student_id>/<test_id(测试ID)>/
```
* 返回数据格式
```
{
    "title": <string 测试名称>,
    "duration": <integer 持续时间 range from 0 to infinite, unit: minute>,
    "start_time": <测试开始时间(YYYY-MM-DD HH:MM:SS)>,
    "end_time": <测试截止时间(YYYY-MM-DD HH:MM:SS)>,
    "questions":[
        {
            "question_id": <question_ID>,
            "stem": <题干>,
            "selections": [<string 选项内容>],
            "selection": <integer range from 1 to 4 or more 学生提交的答案>
            "answer": <integer range from 1 to 4 or more>,
            "score": <score is an integer range from 0 to 100>
        }
    ]
}
```
<h3 id="student-record-post">post:学生提交测试结果</h3>

* 传入数据格式
```
{
    "student_id": <student id>,
    "test_id": <测试ID>,
    "selections": [
        {
            "question_id": <问题ID>,
            "selection": <integer range from 1 to 4 or more 学生提交的答案>
        }
    ]
}
```
* 返回数据格式
```
{
    "status": 200
}
```
<h2 id="/student/record/list/">/student/record/list/</h2>
<h3 id="student-record-list-get">get:获取测试结果列表</h3>

PS: 此API表示获取学生已经参加的测试列表
* 传入数据格式
```
<student id>
```
* 返回数据格式
```
{
    "tests": [
        {
            "test_id": <测试ID>,
            "title": <测试名称>,
            "start_time": <测试开始日期>,
            "end_time": <测试结束日期>,
            "duration": <测试持续时间>
        }
    ]
}
```