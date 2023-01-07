> Java 基础知识：连接数据库操作，及返回结果处理方式

## JDBC 概述
JDBC，Java Database Connectivity，Java数据库连接技术。
JDBC是JDK原生的独立于特定数据库管理系统、通用的SQL数据库存取和操作的公共接口
相关API包： **java.sql.* 和 javax.sql.***
![](_assets/Java%20数据库编程JDBC/1636981457202-e421534d-6d21-403b-852f-070fbca34882.jpeg)

## JDBC 连接
**使用步骤**

1. 添加数据库驱动依赖  // 例如：MySQL的 mysql-connector-java.jar 或者使用maven的pom找到坐标
2. 加载并注册驱动程序
3. 创建 Connection 对象
4. 创建 Statement 对象
5. 执行 SQL 语句
6. 若为查询操作，处理 ResultSet 结果集
7. 关闭 Statement 对象
8. 关闭 Connection 对象



**四个核心接口**

- DriverManager：用于注册驱动并创建符合该驱动的数据库的连接
- Connection:：表示与数据库创建的连接对象，即一个connection对应着一个会话，即一个连接
- Statement：	操作数据库sql语句的对象，有个两个实现类：Statement和PreparedStatement（常用）
- ResultSet:： 	从数据库中查询的结果集
## JDBC 增删改查
操作对象News
```java
@Data
public class News {
    private Integer id;
    private String title;
    private String author;
    private Date date;
}
```
封装资源操作工具类（有够简陋的~）
```java
public class DBUtils {
    public static Connection getConnection() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.cj.jdbc.Driver");
        String url = "jdbc:mysql://localhost:3306/mytest";
        String username = "root";
        String password = "root";
        Connection connection = DriverManager.getConnection(url,username,password);
        return connection;
    }
    public static void closeConnection(PreparedStatement preparedStatement, Connection connection) throws SQLException {
        preparedStatement.close();
        connection.close();
    }
}
```
相关操作
```java
public class NewsDao {
    // add news
    public int addNews(News news) throws SQLException, ClassNotFoundException {
        String sql = "insert into news(id, author,title,date) values (?,?,?,?)";
        Connection connection = DBUtils.getConnection();
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        preparedStatement.setInt(1,news.getId());
        preparedStatement.setString(2,news.getAuthor());
        preparedStatement.setString(3,news.getTitle());
        preparedStatement.setDate(4, (java.sql.Date)news.getDate());
        int addCount = preparedStatement.executeUpdate();
        DBUtils.closeConnection(preparedStatement,connection);
        return addCount;
    }

    // update news
    public int updateNews(News news) throws SQLException, ClassNotFoundException {
        String sql = "update news set title = ? where author = ?";
        Connection connection = DBUtils.getConnection();
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        preparedStatement.setString(1,news.getTitle());
        preparedStatement.setString(2,news.getAuthor());
        int updateCount = preparedStatement.executeUpdate();
        DBUtils.closeConnection(preparedStatement,connection);
        return updateCount;
    }

    // update news

    public int deleteNews(News news) throws SQLException, ClassNotFoundException {
        String sql = "delete from news where id = ?";
        Connection connection = DBUtils.getConnection();
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        preparedStatement.setInt(1,news.getId());
        int deleteCount = preparedStatement.executeUpdate();
        DBUtils.closeConnection(preparedStatement,connection);
        return deleteCount;
    }
    // get news list
    public List<News> getNewsList() throws SQLException, ClassNotFoundException {
        ArrayList newsList = new ArrayList();

        String sql  = "select * from news";
        Connection connection = DBUtils.getConnection();
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        ResultSet resultSet = preparedStatement.executeQuery();
        while (resultSet.next()) {
            News news = new News();
            news.setId(resultSet.getInt("id"));
            news.setAuthor(resultSet.getString("author"));
            news.setTitle(resultSet.getString("title"));
            news.setDate(resultSet.getDate("date"));
            newsList.add(news);
        }
        DBUtils.closeConnection(preparedStatement,connection);
        return  newsList;
    }

    public News getNewsByAuthor(String author) throws SQLException, ClassNotFoundException {
        News news = new News();
        String sql ="select * from news where author like ?";

        Connection connection = DBUtils.getConnection();

        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        preparedStatement.setString(1,"%"+author+"%");

        ResultSet resultSet = preparedStatement.executeQuery();
        while (resultSet.next()) {
            news.setId(resultSet.getInt("id"));
            news.setAuthor(resultSet.getString("author"));
            news.setTitle(resultSet.getString("title"));
            news.setDate(resultSet.getDate("date"));
        }
        DBUtils.closeConnection(preparedStatement,connection);
        return news;
    }
}

```
测试JDBCTest
```java
public class JDBCTest {
    public static void main(String[] args) throws Exception{
        NewsDao newsDao = new NewsDao();

        System.out.println("===========add news===========");
        News news1 = new News();
        news1.setId(100);
        news1.setTitle("add-news-title");
        news1.setAuthor("Sean - add test");
        news1.setDate(new Date(System.currentTimeMillis()));
        int addNews = newsDao.addNews(news1);
        System.out.println("add news : " + addNews);

        System.out.println("===========delete news===========");
        News news2 = new News();
        news2.setId(2);
        int deleteNews = newsDao.deleteNews(news2);
        System.out.println("delete news : " + deleteNews);

        System.out.println("===========update news===========");
        News news3 = new News();
        news3.setAuthor("update-author");
        int updateNews = newsDao.updateNews(news3);
        System.out.println("update news : " + updateNews);

        System.out.println("===========select news===========");
        List<News> newsList = newsDao.getNewsList();
        for (News news : newsList) {
            System.out.println("select news :"+news);
        }


        System.out.println("===========select news by author===========");
        News news = newsDao.getNewsByAuthor("Sean");
        System.out.println("select news by author:"+news.getAuthor());
        System.out.println("select news by author:"+news);
    }
}
```
## JDBC 进阶玩法
数据库连接池

- c3p0
- dbcp

JDBC工具类库

- DBUtils （Apache）

ORM框架

- MyBatis
- Hibernate
- JPA
