# Bookstore
Project for Internet&amp;Application NTUA

## Bookstore Installation Instructions

To run the Bookstore project locally, please follow the steps below:
### Prerequisites 
1. **Install Tomcat Server 8.5:**  
- Visit the [Tomcat download page](https://tomcat.apache.org/download-80.cgi) .
- Download the appropriate distribution package for your operating system.
- Follow the installation instructions provided for your platform. 
2. **Install MariaDB Server 11:**  
- Visit the [MariaDB download page](https://mariadb.org/download/?t=mariadb&p=mariadb&r=11.2.0&os=windows&cpu=x86_64&pkg=msi&m=crete) .
- Download the MSI package for Windows.
- Run the downloaded MSI package and follow the installation instructions.
- Create the user "root" with the password "hallo21" if you dont want to have to change the credentials in the project.
### Setup Database 
1. Launch the MariaDB Command Line Client or any other MySQL client of your choice.
2. Connect to the MariaDB server using your credentials. 
```console 
mysql -u root -p 
``` 
3. Create the Database with ```console 
CREATE DATABASE Bookstore;
```
4. Import the necessary tables and example data for the Bookstore project using the mysqldump tool in the bin folder of mariadb.
The datadump.sql can be found next to the bookstore archive  
 ```console
mysqldump -u username -p new_database < data-dump.sql
```
4.2 Alternatively you can also create the neccessary tables manually

```sql

USE bookstore;

CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  username VARCHAR(50) NOT NULL,
  password VARCHAR(50) NOT NULL,
  email VARCHAR(100) NOT NULL
);

CREATE TABLE books (
  id INT PRIMARY KEY AUTO_INCREMENT,
  title VARCHAR(100) NOT NULL,
  author VARCHAR(100) NOT NULL,
  cover_image VARCHAR(255),
  price DECIMAL(10, 2) NOT NULL,
  description TEXT,
  quantity INT NOT NULL
);

CREATE TABLE shopping_cart (
  user_id INT,
  book_id INT,
  quantity INT,
  PRIMARY KEY (user_id, book_id),
  FOREIGN KEY (user_id) REFERENCES users (id),
  FOREIGN KEY (book_id) REFERENCES books (id)
);
CREATE TABLE placed_orders (
  user_id INT(11) NOT NULL,
  book_id INT(11) NOT NULL,
  quantity INT(11) NOT NULL,
  id INT(11) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (id),
  KEY idx_book_id (book_id),
  CONSTRAINT fk_user_id FOREIGN KEY (user_id) REFERENCES users (user_id),
  CONSTRAINT fk_book_id FOREIGN KEY (book_id) REFERENCES books (book_id)
);
```


### Deploying the Bookstore Web Application 
1. Download the Bookstore project from the [GitHub repository](https://github.com/misterrioes/Bookstore) . 
2. Extract the downloaded project folder to a location on your computer. 
3. Open Eclipse IDE. 
4. Import the project into Eclipse: 
- Select **File**  -> **Import**  -> **Existing Projects into Workspace** .
- Browse to the location where you extracted the project folder. 
- Select the project and click **Run on server** .
- Wait for the server to start and deploy the Bookstore web application.
- Eclipse will open a web browser with the Bookstore application running on http://localhost:8080/Bookstore.

## External Libraries/Code Snippets Used: 
1. MariaDB Connector/J:
- Library: mariadb-java-client.jar
- Usage:
```java
public abstract class JDBCConnection {

	static String url = "jdbc:mariadb://localhost:3306/bookstore";
	static String userdb = "root";
	static String passworddb = "hallo21";
	Connection con = null;

	public static Connection getMariaDbConnection() throws SQLException {
		try {
			Class.forName("org.mariadb.jdbc.Driver");
		} catch (ClassNotFoundException e1) {
			// TODO Auto-generated catch block
			e1.printStackTrace();
		}
		return DriverManager.getConnection(url, userdb, passworddb);
	}
}
```
- Description: The MariaDB Connector/J is a Java database driver for connecting Java applications to the MariaDB database. It provides the necessary functionality to handle the database queries.
2. Servlet API (from Tomcat 8.5):
- Library: servlet-api.jar
- Description: The Servlet API provides the necessary classes and interfaces for creating servlets and handling servlet requests and responses. It is required for developing Java web applications using servlet containers such as Apache Tomcat. 
- Download: You can find the servlet file in the bin folder of your tomcat Installation
3. GSON:
  - Description: GSON is a Java library developed by Google for serializing and deserializing Java objects to JSON and vice versa. It provides a simple API for working with JSON data, making it easier to parse and generate JSON content in Java applications. 
- Library: gson.jar
- Usage:
  ```java
  import com.google.gson.Gson;
  booksJson = new Gson().toJson(books);
  ```

4. Bootstrap:
- Usage:
```html
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
 <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
```   
5. Font Awesome 4:
- Description: Font Awesome is a font and icon toolkit that allows you to easily add scalable vector icons to your web projects.
- Website: [Font Awesome](https://fontawesome.com/v4.7.0/)
