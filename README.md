# Priya
I am submitting the assignment for AsIndia  Innovations Pvt Ltd. for interview purpose
using System;
class Find_Missing_Number
    {
        static void Main(string[] args)
        {
            //array to find the missing number between 1 and 10
            // Simplicity, We will take number 1 to 10 i where Number 5 is missing in the sequence.
            int[] arr = { 1, 2, 3, 4, 6, 7, 8, 9, 10 };

            int missingNumber,Totalsum;
            // Accoreding to series rule, calculating sum of total numbers upto 10
            //sum of first n natutal numbers=n*(n+1)/2
            Totalsum = (arr.Length + 1) * (arr.Length + 2) / 2;

            // Missing number is calculating.
            foreach (int item in arr)
            {
                Totalsum = Totalsum - item;
            }
            missingNumber = Totalsum;

            Console.WriteLine("missing number  : {0}",missingNumber);
        }
    }

Output:-
Missing number =5


2.Create a simple login page where a user can sign in anf then there should be one page where user can rate as put comments on the movies .The averahe rating and comments should be visible besides the movie name?


First I use a web.xml in that i create a project Movieslogin.html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
<table>t
<tr>
<td><input type="text" name="Username"/></td>
</tr>
<tr>
<td>Password</td>
<td><input type="text" name="Password"/></td>
</tr>
<tr>
<td><input type="Submit" name="submit" value="login"/></td>
</tr>
</table>
</body>
</html>
And Next Stage I create MoviesList.Java file(Servlet) file(Controller)

package com.abc.Movieslist;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class Movieslist
 */
@WebServlet("/Movieslist")
public class Movieslist extends HttpServlet {
		protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

			String[] moviesList= {"Shiridisai","Ammoru","Manjunadha"};
			request.setAttribute("moviesList", moviesList);
			RequestDispatcher dispatcher = request.getRequestDispatcher("Movieslogin.html");
	dispatcher.forward(request,response);
		}

}

And in next stage I create MoviesDbUtil.Java(Model class)


package com.abc.Movieslist;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

public class MoviesDbUtil {
	public static List<Movies>getMovielist() throws SQLException
	{
		String url="jdbc:Oracle:thin:@//Localhost:1521/XE";
		String un="system";
		String pw="system";
		
		ArrayList<Movies> movies= new ArrayList<>();
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver");
		} catch (ClassNotFoundException e) {And in next 
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		System.out.println("Driver loaded sucessfully");
		Connection con=DriverManager.getConnection(url,un,pw);
		System.out.println("Connection Established sucessfully");
		Statement stmt=con.createStatement();
	ResultSet rs=	stmt.executeQuery("Select * from Movies");
	while(rs.next())
	{
		String title=rs.getString(1);
		int rating=rs.getInt(2);
		String comments=rs.getString(3);
		Movies m=new Movies(title,rating,comments);
	    movies.add(m);	
	}
	return movies;
	}
	

}

3. And in next stage I create a Movies.java(Oracle my sql connection)


package com.abc.Movieslist;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

public class MoviesDbUtil {
	public static List<Movies>getMovielist() throws SQLException
	{
		String url="jdbc:Oracle:thin:@//Localhost:1521/XE";
		String un="system";
		String pw="system";
		
		ArrayList<Movies> movies= new ArrayList<>();
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver");
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		System.out.println("Driver loaded sucessfully");
		Connection con=DriverManager.getConnection(url,un,pw);
		System.out.println("Connection Established sucessfully");
		Statement stmt=con.createStatement();
	ResultSet rs=	stmt.executeQuery("Select * from Movies");
	while(rs.next())
	{
		String title=rs.getString(1);
		int rating=rs.getInt(2);
		String comments=rs.getString(3);
		Movies m=new Movies(title,rating,comments);
	    movies.add(m);	
	}
	return movies;
	}
	

}
