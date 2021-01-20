# github

## 本地已存在项目与GitHub发生关联

1. 对本地项目进行git初始化 ,初始化后本地项目会创建一个.git文件夹，是附属于该仓库的工作树

   ```java
   git init
   ```

2. 进行git初始化管理后，进行暂存(add)，提交(commit)

   ```java
   git add .
   git commit -m "init commit"
   ```


3. 将本地项目和GitHub远程仓库发生关联(关联前可以不执行第二步的命令，关联后再执行也可以)

   ```java
   git remote add origin git@github.com:Fighting-Night-One-People/pms.git
   ```

4. 将本地项目push到远程GitHub仓库

   ```java
   git push origin master
   ```
- 本地仓库与远程仓库解除管理，只需要将.git文件夹删除即可

  ```java
  进入到本地仓库目录执行以下命令
  rm -rf .git
  ```

  