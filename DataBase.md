### Tables

#### student 学生

+ student_id (primary key)
+ name 学生姓名
+ password 密码

#### question 题目

+ question_id (primary key)
+ stem 题干内容
+ answer 题目答案

#### option 选项

+ question_id (foreign key)
+ content 选项内容

#### test_paper 试卷

+ test_paper_id (primary key)
+ title 试卷名称(仅供老师查看)
+ duration 考试持续时间

#### test 测试

+ test_id (primary key)
+ test_paper_id (foreign key)
+ title 测试名称(仅供学生查看)
+ start_time 测试开始时间
+ end_time 测试截止时间

#### question_ownership 题目试卷所属关系

+ test_paper_id (foreign key)
+ question_id (foreign key)
+ score 每道题的分值

#### record 测试记录

+ student_id (foreign key)
+ test_id (foreign key)
+ question_id (foreign key)
+ selection 学生选择的答案