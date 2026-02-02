## 🚀 Java JDBC CRUD Application with PostgreSQL
### 📌 Overview

This project demonstrates a Java JDBC-based CRUD application integrated with a PostgreSQL database.
It covers all core database operations  Create, Read, Update, and Delete — using Statement and PreparedStatement in a secure and efficient manner.

The project is designed as a console-based application and follows standard JDBC best practices, making it suitable for learning, interviews, and academic projects.

### 🔍 SELECT QUERY – First Program
```
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
	    	   String url="jdbc:postgresql://localhost:5432/kurrecomputers";
	    	   String user="postgres";
	    	   String pwd="8519";
	    	   con=DriverManager.getConnection(url,user,pwd);
	    	  //con=DriverManager.getConnection("jdbc:postgresql://localhost:5432/kurrecomputers","postgres","8519");
	    	   
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
```

}
