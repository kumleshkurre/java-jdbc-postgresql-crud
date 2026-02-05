## 🚀 Java JDBC CRUD Application with PostgreSQL
### 📌 Overview
---
This project demonstrates a Java JDBC-based CRUD application integrated with a PostgreSQL database.
It covers all core database operations  Create, Read, Update, and Delete — using Statement and PreparedStatement in a secure and efficient manner.

The project is designed as a console-based application and follows standard JDBC best practices, making it suitable for learning, interviews, and academic projects.

## 📂 Project Structure
```js
kumleshkurre
├── JRE System Library [JavaSE-21]
├── src
│   ├── Staff
│   │   ├── EmployeeSelect.java
│   │   ├── SelectAllDataById.java
│   │   ├── Employee.java
│   │   ├── Employee2.java
│   │   ├── Employeeupdate.java
│   │   ├── Employeeupdate2.java
│   │   ├── Employeedel.java
│   │   └── Employeedel2.java
│   │
│   └── module-info.java
```
## 🔍 SELECT QUERY – First Program
```js
package Staff;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class Employeeselect {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		    Connection con;
		    Statement stmt;     // select query use
		    ResultSet rs;       // data store
		    try {
	            // Database Connection
		    	String url= "jdbc:postgresql://localhost:5432/your_database_name";
		    	String user= "your_username";
		    	String pwd= "YOUR_PASSWORD";
	            con = DriverManager.getConnection(url,user,pwd);
	            System.out.println("Connection Successful");

	            // Create Statement
	            stmt = con.createStatement();

	            // Execute Query
	            rs = stmt.executeQuery("select * from contact");

	            while (rs.next()) {
	            	System.out.println(rs.getString("name")+" "+rs.getString("mob"));
	            }

	        } catch (Exception e) {
	            System.out.println("Error : " + e);
	        }
	    }
	}
```
## ➕ SELECT QUERY – Second Program (User Input)
```JS
package Staff;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.Scanner;

public class SelectAllDataById {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		    Connection con = null;
	        PreparedStatement ps = null;
	        ResultSet rs = null;
	        Scanner sc = new Scanner(System.in);

		        try {
		        	 // Database Connection
			    	String url= "jdbc:postgresql://localhost:5432/your_database_name";
		    	    String user= "your_username";
		    	    String pwd= "YOUR_PASSWORD";
		            con = DriverManager.getConnection(url,user,pwd);

		            //  User se ID input
		            System.out.print("Enter ID: ");
		            int id = sc.nextInt();

		            //  Create connection
		            con = DriverManager.getConnection(url, user, pwd);
		            System.out.println("Connection Successful");

		            //  SQL Query (ALL data by ID)
		            String sql = "SELECT * FROM contact WHERE id = ?";
		            ps = con.prepareStatement(sql);
		            ps.setInt(1, id);

		            //  Execute query
		            rs = ps.executeQuery();

		            //  Read & print ALL columns
		            if (rs.next()) {
		                System.out.println("----- Employee Details -----");
		                System.out.println("ID     : " + rs.getInt("id"));
		                System.out.println("Name   : " + rs.getString("name"));
		                System.out.println("Mobile : " + rs.getString("mobile"));
		                // agar aur columns hain to yahan add kar sakta hai
		                // System.out.println("City   : " + rs.getString("city"));
		            } else {
		                System.out.println("No record found for ID: " + id);
		            }

		        } catch (Exception e) {
		            System.out.println("Error : " + e.getMessage());
		        } finally {
		            try {
		                if (rs != null) rs.close();
		                if (ps != null) ps.close();
		                if (con != null) con.close();
		                sc.close();
		                System.out.println("Connection Closed");
		            } catch (Exception e) {
		                System.out.println("Close Error : " + e.getMessage());
		            }
		        }
		    }
		}

```
## ➕ INSERT QUERY – First Program (Static Data)
```js
package Staff;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

public class Employee {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Connection con;
	    PreparedStatement psmt;  //insert update delete
	       try {
	    	   String url="jdbc:postgresql://localhost:5432/your_database_name";
	    	   String user="your_username";
	    	   String pwd="YOUR_PASSWORD";
	    	   con=DriverManager.getConnection(url,user,pwd);
	    	  //con=DriverManager.getConnection("jdbc:postgresql://localhost:5432/your_database_name","your_username","YOUR_PASSWORD");
	    	   
	    	  System.out.println("Connection Successfull");   //connection check
	    	  
	    	  //Insert Qury
	    	  psmt=con.prepareStatement("insert into contact(name,email,mob,age,city)values(?,?,?,?,?)");
	    	  psmt.setString(1,"puskar");
	    	  psmt.setString(2,"puskarsahu4@gmail.com");
	    	  psmt.setString(3,"7067132459");
	    	  psmt.setInt(4,22);
	    	  psmt.setString(5,"Lafin");
	    	  
	    	  int r=psmt.executeUpdate();  // executeUpdate 0 and 1 value return kerta hai
	    	  
	    	  if(r>0) {           //r 0 se beda hai
	    		     System.out.println("Insert Success");
	    	  }else {
	    		     System.out.println("Insert Failed");
	    	  }
	       }catch(Exception e) {
	    	   System.out.println(e);
	       }
	}

}
```
## ➕ INSERT QUERY – Second Program (User Input)
```js
package Staff;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class Employee2 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Connection con;
	    PreparedStatement psmt;  //insert update delete
	       try {
	    	  String url="jdbc:postgresql://localhost:5432/your_database_name";
	    	   String user="your_username";
	    	   String pwd="YOUR_PASSWORD";
	    	   con=DriverManager.getConnection(url,user,pwd);
	    	  //con=DriverManager.getConnection("jdbc:postgresql://localhost:5432/your_database_name","your_username","YOUR_PASSWORD");
	    	   	    	   
	    	  System.out.println("Connection Successfull");  //connection check
	    	  
	    	  Scanner sc=new Scanner(System.in);
	    	  System.out.println("Enter your Name");
	    	  String nm=sc.next();
	    	  System.out.println("Enter Email");
	    	  String email=sc.next();
	    	  System.out.println("Enter Mobail Number");
	    	  String mobail=sc.next();
	    	  System.out.println("Enter Age");
	    	  int age=sc.nextInt();
	    	  System.out.println("Enter City");
	    	  String city=sc.next();
	    	  
	    	  psmt=con.prepareStatement("insert into contact(name,email,mob,age,city)values(?,?,?,?,?)");
	    	  psmt.setString(1,nm);
	    	  psmt.setString(2,email);
	    	  psmt.setString(3,mobail);
	    	  psmt.setInt(4,age);
	    	  psmt.setString(5,city);
	    	  
	    	  int r=psmt.executeUpdate();  // executeUpdate 0 and 1 value return kerta hai
	    	  if(r>0) {           //r 0 se beda hai
	    		     System.out.println("Insert Success");
	    	  }else {
	    		     System.out.println("Insert Failed");
	    	  }
	       }catch(Exception e) {
	    	   System.out.println(e);
	       }
	}

}
```
## ✏️ UPDATE QUERY – First Program (Fixed ID)
```js
package Staff;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class Employeeupdate {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Connection con;
	    PreparedStatement psmt;  //insert update delete
	       try {
	    	   String url="jdbc:postgresql://localhost:5432/your_database_name";
	    	   String user="your_username";
	    	   String pwd="YOUR_PASSWORD";
	    	   con=DriverManager.getConnection(url,user,pwd);
	    	  //con=DriverManager.getConnection("jdbc:postgresql://localhost:5432/your_database_name","your_username","YOUR_PASSWORD");

              System.out.println("Connection Successfull");  //connection check
	    	  
	    	  Scanner sc=new Scanner(System.in);
	    	  System.out.println("Enter your Name");
	    	  String nm=sc.next();
	    	  System.out.println("Enter Email");
	    	  String email=sc.next();
	    	  System.out.println("Enter Mobail Number");
	    	  String mobail=sc.next();
	    	  System.out.println("Enter Age");
	    	  int age=sc.nextInt();
	    	  System.out.println("Enter City");
	    	  String city=sc.next();
	    	  
	    	  psmt=con.prepareStatement("update contact set name=?,email=?,mob=?,age=?,city=? where id=8");
	    	  psmt.setString(1,nm);
	    	  psmt.setString(2,email);
	    	  psmt.setString(3,mobail);
	    	  psmt.setInt(4,age);
	    	  psmt.setString(5,city);
	    	  
	    	  int r=psmt.executeUpdate();  // executeUpdate 0 and 1 value return kerta hai
	    	  if(r>0) {           //r 0 se beda hai
	    		     System.out.println("Update Success");
	    	  }else {
	    		     System.out.println("Update Failed");
	    	  }
	       }catch(Exception e) {
	    	   System.out.println(e);
	       }
	}

}
```
## ✏️ UPDATE QUERY – Second Program (User Input ID)
```js
package Staff;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class Employeeupdate2 {

	 public static void main(String[] args) {

	        Connection con;
	        PreparedStatement psmt;

	        try {
	            String url="jdbc:postgresql://localhost:5432/your_database_name";
	    	   String user="your_username";
	    	   String pwd="YOUR_PASSWORD";

	            con = DriverManager.getConnection(url, user, pwd);

	            System.out.println("Connection Successful");

	            Scanner sc = new Scanner(System.in);

	            // Ask ID from user
	            System.out.print("Enter ID to update: ");
	            int id = sc.nextInt();

	            System.out.print("Enter Name: ");
	            String nm = sc.next();

	            System.out.print("Enter Email: ");
	            String email = sc.next();

	            System.out.print("Enter Mobile Number: ");
	            String mobile = sc.next();

	            System.out.print("Enter Age: ");
	            int age = sc.nextInt();

	            System.out.print("Enter City: ");
	            String city = sc.next();

	            // Update Query with user-input ID
	            String query = "UPDATE contact SET name=?, email=?, mob=?, age=?, city=? WHERE id=?";

	            psmt = con.prepareStatement(query);

	            psmt.setString(1, nm);
	            psmt.setString(2, email);
	            psmt.setString(3, mobile);
	            psmt.setInt(4, age);
	            psmt.setString(5, city);
	            psmt.setInt(6, id);  // ID last me set hoga

	            int r = psmt.executeUpdate();

	            if (r > 0) {
	                System.out.println("Update Successful");
	            } else {
	                System.out.println("No record found with this ID");
	            }

	        } catch (Exception e) {
	            System.out.println(e);
	        }
	    }
	}
```
## ❌ DELETE QUERY – First Program (Fixed ID)
```js
package Staff;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;

public class Employeedel {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		 Connection con;
	    PreparedStatement psmt;  //insert update delete
	       try {
	    	   String url="jdbc:postgresql://localhost:5432/your_database_name";
	    	   String user="your_username";
	    	   String pwd="YOUR_PASSWORD";
	    	   con=DriverManager.getConnection(url,user,pwd);
	    	  //con=DriverManager.getConnection("jdbc:postgresql://localhost:5432/your_database_name","your_username","YOUR_PASSWORD");

	    	  System.out.println("Connection Successfull");
	    	  
	    	// Execute Query
	    	  psmt=con.prepareStatement("delete from contact where id=9");
	    	  
	    	  int r=psmt.executeUpdate();  // executeUpdate 0 and 1 value return kerta hai
	    	  
	    	  if(r>0) {           //r 0 se beda hai
	    		     System.out.println("Delete Success");
	    	  }else {
	    		     System.out.println("Delete Failed");
	    	  }
	       }catch(Exception e) {
	    	   System.out.println(e);
	       }
	}

}
```
## ❌ DELETE QUERY – Second Program (User Input)
```js
package Staff;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.util.Scanner;

public class Employeedel2 {

	public static void main(String[] args) {

        Connection con;
        PreparedStatement psmt;

        try {
            // user se id input lena
            Scanner sc = new Scanner(System.in);
            System.out.print("Enter ID to delete: ");
            int id = sc.nextInt();

             String url="jdbc:postgresql://localhost:5432/your_database_name";
	    	   String user="your_username";
	    	   String pwd="YOUR_PASSWORD";

            con = DriverManager.getConnection(url, user, pwd);
            System.out.println("Connection Successful");

            // ? ka use → PreparedStatement (safe hota hai)
            psmt = con.prepareStatement("delete from contact where id = ?");
            psmt.setInt(1, id);

            int r = psmt.executeUpdate();

            if (r > 0) {
                System.out.println("Delete Success");
            } else {
                System.out.println("Delete Failed (ID not found)");
            }

            con.close();
            sc.close();

        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```
 ## 👤 Author
- Kumlesh Kurre
- Java | PostgreSQL | JDBC | Backend Enthusiast
